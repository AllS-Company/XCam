# Method: sessions.list

Lista todas as sessões.

---

## HTTP Request

```http
GET https://jules.googleapis.com/v1alpha/sessions
```

A URL utiliza a sintaxe **gRPC Transcoding**.

---

## Query Parameters

| Parâmetro | Tipo | Descrição |
|------------|------|------------|
| **pageSize** | `integer` | Opcional. Número de sessões a serem retornadas. Deve estar entre 1 e 100 (inclusive). Se não definido, o padrão é 30. Valores maiores que 100 serão ajustados para 100. |
| **pageToken** | `string` | Opcional. Token de página recebido de uma chamada anterior a `sessions.list`. |

---

## Request Body

O corpo da requisição deve estar **vazio**.

---

## Response Body

Mensagem de resposta para `sessions.list`.

Se bem-sucedida, o corpo da resposta conterá dados com a seguinte estrutura:

```json
{
  "sessions": [
    {
      "object (Session)"
    }
  ],
  "nextPageToken": "string"
}
```

### Campos

| Campo | Tipo | Descrição |
|--------|------|------------|
| **sessions[]** | `object (Session)` | As sessões retornadas pela solicitação. |
| **nextPageToken** | `string` | Um token que pode ser enviado como `pageToken` para recuperar a próxima página. Se ausente, não há mais páginas subsequentes. |

---

## Licenciamento

Exceto quando indicado de outra forma, o conteúdo desta página é licenciado sob a **Creative Commons Attribution 4.0 License**, e os exemplos de código sob a **Apache 2.0 License**.

© Google Developers, 2025.
