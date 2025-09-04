Ця діаграма показує сценарій оплати:
- Успішна транзакція 
- Помилка оплати (наприклад, відмова банку)

```mermaid
sequenceDiagram
    participant User
    participant CRM
    participant PaymentGateway

    User->>CRM: Create Order
    CRM->>PaymentGateway: POST /pay

    alt Success
        PaymentGateway-->>CRM: 200 OK
        CRM-->>User: Order Confirmed ✅
    else Failure
        PaymentGateway-x CRM: Error (Declined)
        CRM-->>User: Show error ❌
    end
