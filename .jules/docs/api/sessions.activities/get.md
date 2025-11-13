# Method: sessions.activities.get

Obtém uma única atividade.

---

## HTTP Request

```http
GET https://jules.googleapis.com/v1alpha/{name=sessions/*/activities/*}
```

A URL utiliza a sintaxe **gRPC Transcoding**.

---

## Path Parameters

| Parâmetro | Tipo | Descrição | Formato |
|------------|------|------------|--------|
| **name** | `string` | Obrigatório. O nome do recurso da atividade a ser recuperada. | `sessions/{session}/activities/{activity}`. |

---

## Request Body

O corpo da requisição deve estar **vazio**.

---

## Response Body

Se bem-sucedida, a resposta conterá uma instância de **Activity**.

---

## Licenciamento

Exceto quando indicado de outra forma, o conteúdo desta página é licenciado sob a **Creative Commons Attribution 4.0 License**, e os exemplos de código sob a **Apache 2.0 License**.

© Google Developers, 2025.
