# Base de Conhecimento Consolidada do Agente Jules

## 1. Arquitetura e Stack de Tecnologia

*   **Visão Geral**: O projeto é uma aplicação full-stack que consiste em um backend Cloudflare Workers (TypeScript) e um frontend (HTML/Tailwind/JS) servido diretamente do diretório `dist/`, sem uma etapa de compilação.
*   **Backend**:
    *   **Plataforma**: Cloudflare Workers.
    *   **Linguagem**: TypeScript.
    *   **Banco de Dados Principal**: Cloudflare D1.
    *   **Armazenamento Chave-Valor**: Cloudflare KV é usado para persistir o estado de uploads resumíveis do Google Drive (`AUTH_KV`, `LOGS`, `FILE_CACHE`).
*   **Frontend**:
    *   **Tecnologias**: HTML, Tailwind CSS e JavaScript vanilla.
    *   **Diretório**: Os arquivos são editados diretamente em `dist/`.
    *   **Build**: Não há processo de build ou compilação para o frontend.
    *   **Páginas de UI**: Para manter a consistência visual, páginas de erro ou de callback (como as do fluxo OAuth) são implementadas como arquivos HTML externos (ex: `src/drive/callback_error.html`) que herdam os estilos principais, em vez de serem HTML inline.
*   **Integrações e Serviços Externos**:
    *   **Google Drive**: A aplicação integra-se com o Google Drive para gerenciamento de arquivos. A autenticação é feita via fluxo OAuth 2.0 com refresh token, encapsulado na função `getAccessToken`.
    *   **WebTorrent**: O projeto utiliza a biblioteca WebTorrent para funcionalidades de rastreador de torrents.
    *   **Cloudflare Realtime (SFU)**: A integração com o SFU usa um Durable Object (`SwarmState`) para orquestrar "enxames" de vídeo, gerenciando um seeder persistente que serve chunks de vídeo a partir do Google Drive via DataChannels.
    *   **FFmpeg**: O pipeline de processamento de vídeo (`pipeline.ipynb`) tem uma dependência externa do `ffmpeg`, que precisa ser instalado no ambiente.

## 2. Ambiente de Desenvolvimento, Ferramentas e Deploy

*   **Configuração Inicial**: O script `scripts/setup.sh` prepara o ambiente, verificando e instalando dependências como `ffmpeg` e, crucialmente, criando o arquivo `.dev.vars` a partir do `env.example` se ele não existir.
*   **Variáveis de Ambiente e Segredos**:
    *   **Fonte da Verdade**: O arquivo `.dev.vars` é a fonte única para segredos e variáveis locais. Sua ausência é uma causa comum de falhas de autenticação.
    *   **Não Versionamento**: Este arquivo contém segredos e **não deve** ser versionado, estando corretamente listado no `.gitignore`.
    *   **Conflitos de Binding**: Um `secret` e uma `var` no `wrangler.jsonc` não podem ter o mesmo nome. Um erro `Binding not found [code: 10056]` ao usar `wrangler secret put` pode ser resolvido pré-declarando o nome do binding como uma variável de texto vazia na seção `vars` do `wrangler.jsonc`.
*   **Servidor de Desenvolvimento (`wrangler dev`)**:
    *   O comando `npm run dev` inicia o servidor local.
    *   O servidor pode se tornar instável. Remover o diretório `.wrangler/` pode resolver problemas ao limpar o estado local.
    *   O `wrangler dev` pode não injetar bindings (ex: `env.ASSETS`) de forma consistente, causando erros 500 no backend durante testes E2E.
*   **Processo de Deploy**:
    *   **Script Unificado**: O deploy deve ser feito exclusivamente através do script `scripts/deploy.mjs` (executado com `npm run deploy`). Ele orquestra a sincronização de segredos e a publicação do worker.
    *   **Validação de Segredos**: O script `deploy.mjs` contém uma lógica de validação que interrompe o deploy se segredos obrigatórios estiverem ausentes ou contiverem valores de placeholder no `.dev.vars`, prevenindo deploys mal configurados.
    *   **Autenticação em Ambientes Não-Interativos**: O `wrangler` pode falhar ao herdar variáveis de ambiente. O `deploy.mjs` contorna isso lendo as credenciais diretamente do `.dev.vars` e usando a API da Cloudflare.

## 3. Testes e Qualidade de Código

*   **Testes Unitários**: O projeto utiliza `vitest`, executado com `npm test`.
    *   **Importação de HTML**: O Vitest não consegue importar arquivos `.html` nativamente. A solução é fazer o "mock" da importação diretamente no arquivo de teste usando `vi.mock('caminho/para/arquivo.html', () => ({ default: 'mock content' }));`.
*   **Testes End-to-End (E2E)**: São escritos com Pytest e Playwright.
    *   **Configuração**: Um arquivo `pytest.ini` na raiz é fundamental para definir a `baseURL`.
    *   **Estratégia de Autenticação**: A abordagem robusta é contornar a UI, injetando um token JWT no `localStorage` e interceptando a chamada à API de perfil para retornar um usuário simulado.
    *   **Limitações**: Dada a instabilidade do `wrangler dev`, os testes unitários são mais confiáveis.
*   **CI/CD**: Atualmente, não há um pipeline de CI/CD configurado.

## 4. Padrões, Diretrizes e Boas Práticas

*   **Idioma**: Toda a comunicação, documentação, comentários e código gerado devem estar em **Português (Brasil)**.
*   **Commits**: Devem ser atômicos e focados em uma única mudança lógica.
*   **Documentação**:
    *   **JSDoc**: Deve ser usado para todo o código TypeScript/JavaScript.
    *   **Markdown**: Deve seguir as regras do `docs/markdownlint/GUIA_MARKDOWN.md`.
    *   **Hierarquia**: `.jules/AGENTS.md` é a fonte de verdade de alto nível. A memória persistente (este arquivo) atua como um cache dinâmico de conhecimento específico do projeto.
*   **Depuração de Autenticação OAuth do Google**:
    *   **Erro `invalid_client`**: Indica que `GOOGLE_CLIENT_ID` ou `GOOGLE_CLIENT_SECRET` estão incorretos. A solução é obter as credenciais corretas no Google Cloud Console e atualizar os segredos.
    *   **Erro `invalid_grant`**: Indica que o `REFRESH_TOKEN` é inválido. A solução é forçar a re-autenticação do usuário (acessando `/api/oauth/login`) para gerar um novo `REFRESH_TOKEN`.

## 5. Conhecimentos Específicos da Aplicação

*   **Integração com Cloudflare SFU**:
    *   **Distinção de APIs e Tokens**: A integração exige dois tipos de credenciais: **Token de API da Conta** (`CLOUDFLARE_API_TOKEN`) para o `wrangler` e **Token da Aplicação** (`SFU_API_TOKEN`) para o código do worker.
    *   **Fluxo de Sinalização WebRTC**:
        *   Ao criar uma oferta, é crucial esperar a coleta de candidatos ICE ser concluída (`icegatheringstate` === `'complete'`) antes de enviar o SDP.
        *   A API do SFU não permite adicionar novas tracks a uma sessão imediatamente após sua criação; é preciso esperar a conexão do `RTCPeerConnection`.
*   **Operação do Agente (Jules)**:
    *   **Framework de Prompt**: As instruções devem seguir o padrão **I.I.I.F.** (Identidade, Instrução, Informação, Formato) detalhado em `.jules/AGENTS.md`.
    *   **Comunicação de Próximos Passos**: Conforme a diretiva C.2.4.5, a "Proposição Estratégica de Próximos Passos" e os "Prompts de Ação Rápida" devem ser obrigatoriamente apresentadas ao usuário diretamente na sessão de chat ao final de cada tarefa.

## 6. Meta-Operacional: Ambiente de Execução

*   **Instabilidade do Repositório Git**:
    *   **Sintoma**: O ambiente de execução pode realizar commits automáticos com mensagens genéricas (ex: "Apply patch..."). Isso faz com que `git status` reporte falsamente uma "árvore de trabalho limpa" e impede a criação de novos commits (`nothing to commit`).
    *   **Diagnóstico**: Utilizar `git log -1` para inspecionar a mensagem do último commit. Se for genérica, um commit automático indesejado ocorreu.
    *   **Solução**: Usar `git commit --amend -m "Sua mensagem de commit correta"` para corrigir a mensagem do último commit e incorporar as alterações. É recomendado encadear a verificação na mesma linha para evitar condições de corrida com o ambiente: `git commit --amend ... && git log -1`.
