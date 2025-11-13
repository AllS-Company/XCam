# Documentação do Core do Agente Jules

Este diretório (`.jules/core/`) armazena os arquivos fundamentais que definem o comportamento, o conhecimento e a estrutura operacional do agente de codificação Jules. São os componentes centrais que guiam a sua identidade e a sua capacidade de executar tarefas.

---

## Conteúdo do Diretório

### 1. `template_prompt_mestre.md`

Este arquivo Markdown é o **modelo mestre** ou a "cópia de ouro" para toda a engenharia de prompts do Jules. Ele não se destina ao uso direto para executar uma tarefa, but serve como o esqueleto padrão para a criação de novos arquivos de prompt de tarefa.

**Propósito:**

* **Padronização:** Garante que todas as tarefas delegadas ao Jules sigam uma estrutura consistente, incluindo seções cruciais como `Papel`, `Objetivo`, `Contexto`, `Requisitos`, `Critérios de Sucesso` e `Fluxo de Execução`.
* **Engenharia de Prompt:** Funciona como um guia para os desenvolvedores (ou outros agentes) sobre como formular prompts eficazes, detalhando quais informações são necessárias para que o Jules compreenda e execute uma tarefa com sucesso.
* **Meta-Prompting:** É a base do processo de "meta-prompting", onde o próprio agente pode ser instruído a criar novos prompts de tarefa, usando este template como referência.

Em suma, este arquivo é a chave para a consistência e a escalabilidade na delegação de trabalho ao Jules.

### 2. `JulesDb.json`

Este arquivo JSON é a **base de conhecimento interna e estruturada** do agente Jules. Funciona como um banco de dados de configuração que contém uma descrição detalhada e hierárquica de si mesmo.

**Propósito:**

* **Autoconhecimento:** Fornece ao agente uma fonte de verdade sobre sua própria identidade, arquitetura (motor de inteligência Gemini 2.5 Pro, ambiente de execução em VM), capacidades, funcionalidades avançadas (como *Critic-Augmented Generation* e memória), e limitações.
* **Biblioteca de Tarefas:** Contém uma lista de "tarefas" pré-definidas e estruturadas, como `Audit Repository`, `Fix and Refine`, e `Update Dependencies`. Cada tarefa é detalhada com seu objetivo, contexto, requisitos e entregáveis, servindo como uma biblioteca de capacidades que o agente pode consultar.
* **Guia de Documentação:** Inclui metadados e conteúdo para a geração de documentação, como guias de uso de prompts e de configuração de ambiente.

Essencialmente, o `JulesDb.json` é a "constituição" do agente, um documento que ele pode consultar para entender quem ele é, o que ele pode fazer e como ele deve operar.
