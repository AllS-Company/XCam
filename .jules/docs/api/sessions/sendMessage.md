# Method: sessions.sendMessage

Envia uma mensagem do usuário para uma sessão.

---

## HTTP Request

```http
POST https://jules.googleapis.com/v1alpha/{session=sessions/*}:sendMessage
```

A URL utiliza a sintaxe **gRPC Transcoding**.

---

## Path Parameters

| Parâmetro | Tipo | Descrição |
|------------|------|------------|
| **session** | `string` | Obrigatório. O nome do recurso da sessão para a qual a mensagem será enviada.<br>Formato: `sessions/{session}`. |

---

## Request Body

O corpo da requisição contém dados com a seguinte estrutura:

```json
{
  "prompt": "string"
}
```

### Campos

| Campo | Tipo | Descrição |
|--------|------|------------|
| **prompt** | `string` | Obrigatório. O *prompt* (mensagem) que o usuário deseja enviar para a sessão. |

---

## Response Body

Se bem-sucedida, a resposta estará **vazia**.

---

## Licenciamento

Exceto quando indicado de outra forma, o conteúdo desta página é licenciado sob a **Creative Commons Attribution 4.0 License**, e os exemplos de código sob a **Apache 2.0 License**.

© Google Developers, 2025.
