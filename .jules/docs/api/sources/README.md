# REST Resource: sources

Uma fonte de entrada de dados para uma sessão.

---

## Resource: Source

### Exemplo de Estrutura JSON

```json
{
  "name": "string",
  "id": "string",
  "gitHubRepo": {
    "object (GitHubRepo)"
  }
}
```

---

## Campos

| Nome | Tipo | Descrição |
|------|------|------------|
| **name** | `string` | Identificador. Nome completo do recurso (ex.: `sources/{source}`). |
| **id** | `string` | Somente leitura. O identificador da fonte, equivalente à parte `{source}` do nome completo do recurso. |
| **gitHubRepo** | `object (GitHubRepo)` | Um repositório GitHub associado à fonte. |

> O campo de união `source` pode conter apenas um dos seguintes tipos: `gitHubRepo`.

---

## GitHubRepo

Um repositório GitHub.

### Exemplo de Estrutura JSON

```json
{
  "owner": "string",
  "repo": "string",
  "isPrivate": false,
  "defaultBranch": {
    "object (GitHubBranch)"
  },
  "branches": [
    {
      "object (GitHubBranch)"
    }
  ]
}
```

---

### Campos

| Nome | Tipo | Descrição |
|------|------|------------|
| **owner** | `string` | Proprietário do repositório. Corresponde ao `<owner>` em `https://github.com/<owner>/<repo>`. |
| **repo** | `string` | Nome do repositório. Corresponde ao `<repo>` em `https://github.com/<owner>/<repo>`. |
| **isPrivate** | `boolean` | Indica se o repositório é privado. |
| **defaultBranch** | `object (GitHubBranch)` | A *branch* padrão do repositório. |
| **branches[]** | `object (GitHubBranch)` | Lista de *branches* ativas do repositório. |

---

## GitHubBranch

Uma *branch* GitHub.

### Exemplo de Estrutura JSON

```json
{
  "displayName": "string"
}
```

---

### Campos

| Nome | Tipo | Descrição |
|------|------|------------|
| **displayName** | `string` | Nome da *branch* GitHub. |

---

## Métodos

| Método | Descrição |
|---------|------------|
| **get** | Obtém uma única fonte. |
| **list** | Lista todas as fontes disponíveis. |

---

## Licenciamento

Exceto quando indicado de outra forma, o conteúdo desta página é licenciado sob a **Creative Commons Attribution 4.0 License**, e os exemplos de código sob a **Apache 2.0 License**.

© Google Developers, 2025.
