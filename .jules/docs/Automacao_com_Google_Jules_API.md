# Guia Prático: Automação do Pipeline de Vídeo com a API Jules

Este documento serve como um guia prático e a fonte da verdade para a interação do nosso projeto com a API do Google Jules. O objetivo é detalhar como iniciamos nosso pipeline de processamento de vídeo (`pipeline.ipynb`) de forma programática.

## 1. Visão Geral do Fluxo

O processo é iniciado quando uma chamada é feita para o nosso endpoint de backend `POST /upload-complete`. Este endpoint, através da função `handleInitiateVideoProcessing`, constrói e envia uma requisição para a API do Jules, instruindo o agente a executar nosso notebook de pipeline.

A interação é assíncrona. Nós disparamos a execução e o agente Jules cuida do resto, incluindo o download do vídeo, a execução do `ffmpeg`, e o upload dos assets gerados de volta para o nosso backend.

## 2. Endpoint e Autenticação

- **Endpoint da API:** `https://jules.googleapis.com/v1alpha/sessions`
- **Método HTTP:** `POST`
- **Autenticação:** A requisição deve incluir um cabeçalho `Authorization: Bearer <token>`. O token de acesso é um JWT de curta duração, obtido através da função `getJulesAccessToken`, que usa as nossas credenciais de conta de serviço do Google Cloud para gerar o token.

## 3. Estrutura da Requisição (Payload)

A parte mais crítica da interação é a construção correta do payload da requisição. Nossa implementação usa a interface `JulesSessionRequest` para garantir a tipagem e a estrutura corretas.

Abaixo está um exemplo do payload exato que nosso sistema envia, seguido por uma explicação detalhada de cada campo.

### Exemplo de Payload

```json
{
  "sourceContext": {
    "source": "sources/github/SamuelPassamani/upload"
  },
  "execution": {
    "notebook": {
      "path": "pipeline.ipynb",
      "output_path_template": "output/output_{videoId}.ipynb",
      "parameters": {
        "VIDEO_ID": "{videoId}"
      }
    }
  },
  "environment": {
    "ASERIO_TOKEN": "{aserioToken}",
    "FIXED_TOKEN": "{fixedToken}"
  }
}
```

### Detalhamento dos Campos

#### `sourceContext`
- **`source`**: `string`
  - **Descrição:** Especifica o repositório de código-fonte onde o agente Jules irá operar. O agente fará um clone deste repositório para ter acesso a todos os arquivos necessários, incluindo o `pipeline.ipynb`.
  - **Nosso Valor:** `sources/github/SamuelPassamani/upload`

#### `execution`
Este objeto define o que o agente deve executar.
- **`notebook`**: `object`
  - **Descrição:** Contém as especificações para a execução de um notebook Jupyter.
  - **`path`**: `string`
    - **Descrição:** O caminho, a partir da raiz do repositório, para o arquivo do notebook a ser executado.
    - **Nosso Valor:** `pipeline.ipynb`
  - **`output_path_template`**: `string`
    - **Descrição:** Um modelo para nomear o arquivo do notebook de saída, que conterá os resultados e logs da execução. Podemos usar placeholders como `{videoId}` para gerar nomes de arquivo únicos.
    - **Nosso Valor:** `output/output_{videoId}.ipynb`
  - **`parameters`**: `object`
    - **Descrição:** Um dicionário de parâmetros que serão injetados no notebook pelo `papermill` antes da execução. As chaves deste objeto devem corresponder aos nomes das variáveis na célula marcada como "parameters" no notebook.
    - **Nosso Valor:** `{"VIDEO_ID": "{videoId}"}`. O `videoId` do arquivo recém-processado é injetado aqui.

#### `environment`
- **Descrição:** Um dicionário de variáveis de ambiente que serão definidas no ambiente de execução do agente Jules. Isso é crucial para passar segredos e configurações necessárias para o pipeline.
- **Nossos Valores:**
  - **`ASERIO_TOKEN`**: Passa o nosso token de API interno, permitindo que o notebook baixe o arquivo de vídeo original do nosso próprio sistema.
  - **`FIXED_TOKEN`**: Passa o token de autenticação fixo, permitindo que o notebook se autentique de volta com nosso backend ao fazer o upload dos assets gerados.

## 4. Conclusão

Esta documentação reflete a implementação exata encontrada em `src/drive/video_handlers.ts` e deve ser a referência principal para entender e manter a integração com a API Jules. Qualquer alteração na forma como chamamos a API deve ser refletida aqui.