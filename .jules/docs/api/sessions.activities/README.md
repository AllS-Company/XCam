# REST Resource: v1alpha.sessions.activities

Recurso: **Activity**

Representa uma atividade dentro de uma sessão.

---

## Exemplo de Recurso

```json
{
  "name": "sessions/123/activities/456",
  "createTime": "2025-03-20T14:15:22.123Z",
  "completionTime": "2025-03-20T14:16:00.000Z",
  "state": "COMPLETED",
  "userMessage": {
    "content": "Gerar código Python para soma de números",
    "role": "USER"
  },
  "parts": [
    {
      "text": "Aqui está o código solicitado:",
      "codeExecution": {
        "code": "print(1+2)",
        "language": "python",
        "output": "3"
      }
    }
  ],
  "agent": {
    "name": "JulesCodeBot",
    "version": "v1.4.3"
  }
}
```

---

## Campos

| Nome | Tipo | Descrição |
|------|------|------------|
| **name** | `string` | Nome do recurso da atividade. |
| **createTime** | `string (timestamp)` | Momento em que a atividade foi criada. |
| **completionTime** | `string (timestamp)` | Momento em que a atividade foi concluída. |
| **state** | `enum (Activity.State)` | Estado atual da atividade. |
| **userMessage** | `object (UserMessage)` | Mensagem enviada pelo usuário que iniciou a atividade. |
| **parts[]** | `object (Part)` | Componentes que formam a atividade (texto, código, arquivos etc.). |
| **agent** | `object (Agent)` | Agente que executou a atividade. |

---

## Enum: Activity.State

| Valor | Descrição |
|--------|------------|
| **STATE_UNSPECIFIED** | Estado não especificado. |
| **RUNNING** | A atividade está em execução. |
| **COMPLETED** | A atividade foi concluída. |
| **FAILED** | A atividade falhou. |

---

## UserMessage

Representa uma mensagem do usuário.

### Estrutura

```json
{
  "content": "string",
  "role": "string"
}
```

| Campo | Tipo | Descrição |
|--------|------|------------|
| **content** | `string` | Conteúdo textual da mensagem. |
| **role** | `string` | Papel do remetente (ex.: `USER`). |

---

## Part

Um componente individual da atividade.

### Estrutura

```json
{
  "text": "string",
  "codeExecution": {
    "code": "string",
    "language": "string",
    "output": "string"
  },
  "fileOutput": {
    "fileName": "string",
    "uri": "string"
  }
}
```

| Campo | Tipo | Descrição |
|--------|------|------------|
| **text** | `string` | Texto gerado pela atividade. |
| **codeExecution** | `object (Part.CodeExecution)` | Bloco de código executado. |
| **fileOutput** | `object (Part.FileOutput)` | Saída gerada em arquivo, se aplicável. |

---

## Part.CodeExecution

Representa um trecho de código executado.

### Estrutura

```json
{
  "code": "string",
  "language": "string",
  "output": "string"
}
```

| Campo | Tipo | Descrição |
|--------|------|------------|
| **code** | `string` | Código-fonte executado. |
| **language** | `string` | Linguagem de programação utilizada. |
| **output** | `string` | Resultado ou saída do código. |

---

## Part.FileOutput

Representa um arquivo gerado pela atividade.

### Estrutura

```json
{
  "fileName": "string",
  "uri": "string"
}
```

| Campo | Tipo | Descrição |
|--------|------|------------|
| **fileName** | `string` | Nome do arquivo de saída. |
| **uri** | `string` | URI de acesso ao arquivo gerado. |

---

## Agent

Representa o agente responsável pela execução da atividade.

### Estrutura

```json
{
  "name": "string",
  "version": "string"
}
```

| Campo | Tipo | Descrição |
|--------|------|------------|
| **name** | `string` | Nome do agente (ex.: `JulesCodeBot`). |
| **version** | `string` | Versão do agente. |

---

## Licenciamento

Exceto quando indicado de outra forma, o conteúdo desta página é licenciado sob a **Creative Commons Attribution 4.0 License**, e os exemplos de código sob a **Apache 2.0 License**.

© Google Developers, 2025.
