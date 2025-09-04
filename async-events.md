```mermaid
sequenceDiagram
    participant ERP
    participant PaymentGateway
    participant Queue
    participant CRM

    ERP->>PaymentGateway: POST /pay (sync)
    PaymentGateway-->>ERP: 202 Accepted (processing)

    PaymentGateway-->>Queue: PaymentConfirmed Event (async)
    Queue-->>CRM: Deliver event
    CRM-->>CRM: Update status = PAID
