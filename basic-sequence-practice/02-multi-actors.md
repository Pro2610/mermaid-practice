Діаграма з кількома учасниками.

```mermaid
sequenceDiagram
    User->>CRM: Створити замовлення
    CRM->>ERP: Передати дані
    ERP->>PaymentGateway: API call
    PaymentGateway-->>ERP: Success
    ERP-->>CRM: Статус OK
    CRM-->>User: Підтвердження
