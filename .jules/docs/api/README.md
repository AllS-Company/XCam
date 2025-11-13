# Jules API

Crie e acesse programaticamente suas tarefas assíncronas de codificação.

---

## Service: jules.googleapis.com

Para chamar este serviço, recomenda-se o uso das **client libraries** fornecidas pelo Google.
Se a sua aplicação precisar usar bibliotecas próprias para realizar chamadas à API, utilize as seguintes informações ao efetuar as requisições.

---

## Service Endpoint

Um **service endpoint** é uma URL base que especifica o endereço de rede de um serviço de API.
Um serviço pode ter múltiplos endpoints; este serviço possui o seguinte endpoint e todos os URIs abaixo são relativos a ele:

- `https://jules.googleapis.com`

---

## REST Resource: v1alpha.sessions

| Método | HTTP Request | Descrição |
|---------|---------------|-----------|
| **approvePlan** | `POST /v1alpha/{session=sessions/*}:approvePlan` | Aprova um plano em uma sessão. |
| **create** | `POST /v1alpha/sessions` | Cria uma nova sessão. |
| **get** | `GET /v1alpha/{name=sessions/*}` | Obtém uma sessão específica. |
| **list** | `GET /v1alpha/sessions` | Lista todas as sessões. |
| **sendMessage** | `POST /v1alpha/{session=sessions/*}:sendMessage` | Envia uma mensagem do usuário para uma sessão. |

---

## REST Resource: v1alpha.sessions.activities

| Método | HTTP Request | Descrição |
|---------|---------------|-----------|
| **get** | `GET /v1alpha/{name=sessions/*/activities/*}` | Obtém uma atividade específica. |
| **list** | `GET /v1alpha/{parent=sessions/*}/activities` | Lista atividades de uma sessão. |

---

## REST Resource: v1alpha.sources

| Método | HTTP Request | Descrição |
|---------|---------------|-----------|
| **get** | `GET /v1alpha/{name=sources/*}` | Obtém uma fonte específica. |
| **list** | `GET /v1alpha/sources` | Lista as fontes disponíveis. |

---

## Licenciamento

Exceto quando indicado de outra forma, o conteúdo desta página é licenciado sob a **Creative Commons Attribution 4.0 License**, e os exemplos de código sob a **Apache 2.0 License**.

© Google Developers, 2025.
