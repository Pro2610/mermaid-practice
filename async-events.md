Ця діаграма показує сценарій асинхронної взаємодії:  
- ERP робить синхронний виклик до Payment Gateway  
- Gateway підтверджує прийом запиту (202 Accepted)  
- Після обробки відправляє подію у чергу (Queue)  
- CRM отримує повідомлення з Queue і оновлює статус  

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
