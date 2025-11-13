# Method: sessions.activities.list

Lista as atividades de uma sessão.

---

## HTTP Request

```http
GET https://jules.googleapis.com/v1alpha/{parent=sessions/*}/activities
```

A URL utiliza a sintaxe **gRPC Transcoding**.

---

## Path Parameters

| Parâmetro | Tipo | Descrição |
|------------|------|------------|
| **parent** | `string` | Obrigatório. A sessão pai que contém a coleção de atividades.<br>Formato: `sessions/{session}`. |

---

## Query Parameters

| Parâmetro | Tipo | Descrição |
|------------|------|------------|
| **pageSize** | `integer` | Opcional. O número de atividades a serem retornadas. Deve estar entre 1 e 100 (inclusive). Se não definido, o valor padrão é 50. Valores maiores que 100 serão ajustados para 100. |
| **pageToken** | `string` | Opcional. Um token de página recebido de uma chamada anterior a `activities.list`. |

---

## Request Body

O corpo da requisição deve estar **vazio**.

---

## Response Body

Mensagem de resposta para `activities.list`.

Se bem-sucedida, o corpo da resposta conterá dados com a seguinte estrutura:

```json
{
  "activities": [
    {
      "object (Activity)"
    }
  ],
  "nextPageToken": "string"
}
```

### Campos

| Campo | Tipo | Descrição |
|--------|------|------------|
| **activities[]** | `object (Activity)` | As atividades retornadas pela sessão especificada. |
| **nextPageToken** | `string` | Um token que pode ser usado como `pageToken` para recuperar a próxima página. Se ausente, não há mais páginas subsequentes. |

---

## Licenciamento

Exceto quando indicado de outra forma, o conteúdo desta página é licenciado sob a **Creative Commons Attribution 4.0 License**, e os exemplos de código sob a **Apache 2.0 License**.

© Google Developers, 2025.
