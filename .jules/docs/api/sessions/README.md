# REST Resource: Sessions

**Endpoint Base:**
`https://api.jules.ai/v1/sessions`

**Metodos disponiveis:**

- `create`
- `get`
- `list`
- `delete`
- `update`

---

## Recurso: Session

Uma **Session** representa uma quantidade configuravel de trabalho dentro de um
mesmo contexto.

### Exemplo de Recurso

```json
{
  "name": "sessions/123456789",
  "create_time": "2024-03-25T10:23:45.123Z",
  "update_time": "2024-03-25T10:24:10.456Z",
  "state": "ACTIVE",
  "automation_mode": "MANUAL",
  "source_context": {
    "git_lab_repo_context": {
      "repo_url": "https://gitlab.com/example/repo"
    }
  },
  "output": {
    "pull_request": {
      "url": "https://gitlab.com/example/repo/-/merge_requests/1",
      "title": "Implementacao inicial da API de sessao",
      "description": "Criacao do endpoint de sessao"
    }
  }
}
```

---

## Campos de uma Session

|Nome|Tipo|Descricao|
|---|---|---|
|**name**|`string`|Nome do recurso da sessao.|
|**create_time**|`string`|Momento da criacao em ISO 8601.|
|**update_time**|`string`|Momento da ultima atualizacao (ISO 8601).|
|**state**|`enum`|Estado atual da sessao.|
|**automation_mode**|`enum`|Modo de automacao usado na sessao.|
|**source_context**|`object SourceContext`|Contexto-fonte usado pela sessao.|
|**output**|`object SessionOutput`|Resultado retornado pela sessao.|

---

## SourceContext

Contem os contextos nos quais uma sessao foi executada.

### Exemplo de SourceContext (JSON)

```json
{
  "source": "git_lab_repo_context",
  "git_lab_repo_context": {
    "repo_url": "https://gitlab.com/example/repo"
  }
}
```

### Campos de um SourceContext

|Nome|Tipo|Descricao|
|---|---|---|
|**source**|`string`|Tipo de contexto-fonte (ex.: `git_lab_repo_context`).|
|**git_lab_repo_context**|`object`|Contexto GitLab associado a sessao.|

---

## GitLabRepoContext

Contexto de um repositorio GitLab utilizado numa sessao.

### Exemplo de GitLabRepoContext (JSON)

```json
{
  "repo_url": "https://gitlab.com/example/repo"
}
```

### Campos de um GitLabRepoContext

|Nome|Tipo|Descricao|
|---|---|---|
|**repo_url**|`string`|URL do repositorio GitLab.|

---

## AutomationMode

Define o modo de automacao da sessao.

|Valor|Descricao|
|---|---|
|**AUTOMATION_MODE_UNSPECIFIED**|Modo nao especificado.|
|**MANUAL**|Sessao criada manualmente.|
|**AUTOMATED**|Sessao criada automaticamente por integracao ou agente.|

---

## State

Estado de uma sessao.

|Valor|Descricao|
|---|---|
|**STATE_UNSPECIFIED**|Estado nao especificado.|
|**PENDING**|Sessao criada e pendente.|
|**RUNNING**|Sessao em execucao.|
|**AWAITING_APPROVAL**|Sessao aguardando aprovacao.|
|**APPROVED**|Sessao aprovada.|
|**WAITING_FOR_FEEDBACK**|Sessao aguardando feedback.|
|**PAUSED**|Sessao pausada.|
|**FAILED**|Sessao falhou.|
|**SUCCEEDED**|Sessao concluida com sucesso.|

---

## SessionOutput

Um artefato de saida de uma sessao.

### Exemplo de SessionOutput (JSON)

```json
{
  "output": {
    "pull_request": {
      "url": "https://gitlab.com/example/repo/-/merge_requests/1",
      "title": "Nova funcionalidade de autenticacao",
      "description": "Implementa o fluxo OAuth 2.0"
    }
  }
}
```

### Campos de um SessionOutput

|Nome|Tipo|Descricao|
|---|---|---|
|**pull_request**|`object`|Pull Request associada a sessao, se houver.|

---

## PullRequest

Representa uma Pull Request.

### Exemplo de PullRequest (JSON)

```json
{
  "url": "https://gitlab.com/example/repo/-/merge_requests/1",
  "title": "Implementacao inicial da API de sessao",
  "description": "Criacao do endpoint de sessao"
}
```

### Campos de uma PullRequest

|Nome|Tipo|Descricao|
|---|---|---|
|**url**|`string`|URL da Pull Request.|
|**title**|`string`|Titulo da Pull Request.|
|**description**|`string`|Descricao da Pull Request.|
|**metadata**|`object`|Metadados adicionais da Pull Request.|

---

## Metadata (opcional)

Metadados adicionais aplicaveis a uma sessao.

|Campo|Tipo|Descricao|
|---|---|---|
|**agent_name**|`string`|Nome do agente envolvido na sessao.|
|**agent_version**|`string`|Versao do agente.|
|**session_type**|`string`|Tipo de sessao.|
|**trigger**|`string`|Evento que iniciou a sessao.|

---

## Licenciamento

Exceto quando indicado de outra forma, o conteudo desta pagina e licenciado
sob a **Creative Commons Attribution 4.0 License**.
O codigo de exemplo esta sob a **Apache 2.0 License**.

Copyright Google Developers, 2025.

<!-- @roadmap
- [P2] Padronizar a codificacao em UTF-8 para evitar simbolos de substituicao.
- [P3] Adicionar exemplos de SessionOutput com metadados opcionais.
-->
