```mermaid
sequenceDiagram
    participant User
    participant CRM
    participant PaymentGateway
    participant Database

    Note over User,CRM: Початок процесу<br/>Користувач створює замовлення
    User->>CRM: Submit order

    CRM->>+PaymentGateway: Create payment
    Note right of PaymentGateway: Перевірка даних<br/>і маршрутизація

    PaymentGateway->>+Database: Log transaction
    Database-->>-PaymentGateway: OK
    PaymentGateway-->>-CRM: Payment Success

    CRM-->>User: Замовлення оплачене ✅
    Note left of User: Завершення процесу
