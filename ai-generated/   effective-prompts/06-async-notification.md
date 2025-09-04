Промпт 3 — Async notification (черга)

Створи Mermaid sequence diagram для процесу асинхронного повідомлення через чергу.
Учасники: ERP, Payment Gateway, Queue, CRM.
Кроки:

ERP надсилає синхронний запит у Payment Gateway.

Payment Gateway відповідає кодом 202 (прийнято до обробки).

Після обробки Gateway надсилає подію у Queue.

CRM отримує подію з Queue і оновлює статус платежу.
Використай -->> для асинхронної події з Gateway у Queue.

```mermaid
sequenceDiagram
    participant ERP as ERP
    participant PG as Payment Gateway
    participant Queue as Queue
    participant CRM as CRM

    ERP->>PG: Надсилає синхронний запит на платіж
    activate PG
    
    PG-->>ERP: Відповідає кодом 202 (прийнято до обробки)
    
    Note over PG: Payment Gateway обробляє платіж асинхронно
    
    PG-->>Queue: Надсилає подію про результат платежу
    activate Queue
    deactivate PG
    
    Queue-->>CRM: Передає подію про платіж
    activate CRM
    deactivate Queue
    
    CRM->>CRM: Оновлює статус платежу
    
    Note over CRM: Статус платежу оновлено в системі
    
    deactivate CRM



