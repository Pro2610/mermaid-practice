Приклад з умовним сценарієм: успіх або помилка.

```mermaid
sequenceDiagram
    CRM->>PaymentGateway: POST /pay

    alt Success
        PaymentGateway-->>CRM: 200 OK
        CRM-->>CRM: Update status = PAID
    else Failure
        PaymentGateway-x CRM: Error ❌
        CRM-->>CRM: Update status = FAILED
    end
