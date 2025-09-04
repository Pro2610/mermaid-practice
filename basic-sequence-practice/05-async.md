Асинхронна взаємодія через події.

```mermaid
sequenceDiagram
    participant ERP
    participant PaymentGateway
    participant Queue
    participant CRM

    ERP->>PaymentGateway: POST /pay (sync)
    PaymentGateway-->>ERP: 202 Accepted

    PaymentGateway-->>Queue: PaymentConfirmed (async)
    Queue-->>CRM: Deliver event
    CRM-->>CRM: Update status = PAID
