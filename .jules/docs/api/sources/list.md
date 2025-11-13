# Method: sources.list

Lista as fontes disponíveis.

---

## HTTP Request

```http
GET https://jules.googleapis.com/v1alpha/sources
```

A URL utiliza a sintaxe **gRPC Transcoding**.

---

## Query Parameters

| Parâmetro | Tipo | Descrição |
|------------|------|------------|
| **filter** | `string` | Opcional. Expressão de filtro para listar fontes, baseada em *API-160*. Se não for definida, todas as fontes serão retornadas.<br>Atualmente, o filtro suporta apenas pesquisa por nome e pode ser usado para filtrar por uma ou mais fontes separadas por **OR**.<br>**Exemplo:** `filter="name=sources/source1 OR name=sources/source2"`. |
| **pageSize** | `integer` | Opcional. Número de fontes a serem retornadas. Deve estar entre 1 e 100 (inclusive). Se não definido, o valor padrão é 30. Valores maiores que 100 serão ajustados para 100. |
| **pageToken** | `string` | Opcional. Token de página recebido de uma chamada anterior a `sources.list`. |

---

## Request Body

O corpo da requisição deve estar **vazio**.

---

## Response Body

Mensagem de resposta para `sources.list`.

Se bem-sucedida, o corpo da resposta conterá dados com a seguinte estrutura:

```json
{
  "sources": [
    {
      "object (Source)"
    }
  ],
  "nextPageToken": "string"
}
```

### Campos

| Campo | Tipo | Descrição |
|--------|------|------------|
| **sources[]** | `object (Source)` | As fontes retornadas pela requisição. |
| **nextPageToken** | `string` | Um token que pode ser usado como `pageToken` para recuperar a próxima página. Se ausente, não há mais páginas subsequentes. |

---

## Licenciamento

Exceto quando indicado de outra forma, o conteúdo desta página é licenciado sob a **Creative Commons Attribution 4.0 License**, e os exemplos de código sob a **Apache 2.0 License**.

© Google Developers, 2025.
