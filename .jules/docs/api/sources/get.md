# Method: sources.get

Obtém uma única fonte (*source*).

---

## HTTP Request

```http
GET https://jules.googleapis.com/v1alpha/{name=sources/*}
```

A URL utiliza a sintaxe **gRPC Transcoding**.

---

## Path Parameters

| Parâmetro | Tipo | Descrição |
|------------|------|------------|
| **name** | `string` | Obrigatório. O nome do recurso da fonte a ser recuperada.<br>Formato: `sources/{source}`. |

---

## Request Body

O corpo da requisição deve estar **vazio**.

---

## Response Body

Se bem-sucedida, a resposta conterá uma instância de **Source**.

---

## Licenciamento

Exceto quando indicado de outra forma, o conteúdo desta página é licenciado sob a **Creative Commons Attribution 4.0 License**, e os exemplos de código sob a **Apache 2.0 License**.

© Google Developers, 2025.
