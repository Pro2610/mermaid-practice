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


Діаграма показує процес асинхронного повідомлення через чергу:

ERP надсилає синхронний запит на платіж до Payment Gateway
Payment Gateway негайно відповідає кодом 202 (прийнято до обробки), не чекаючи завершення
Payment Gateway асинхронно обробляє платіж у фоновому режимі
Після завершення обробки Payment Gateway надсилає подію про результат у Queue (використано -->> для асинхронної події)
Queue передає подію в CRM систему
CRM отримує подію і оновлює статус платежу в системі

Ключова особливість цієї діаграми — використання асинхронного підходу, де ERP не чекає на завершення обробки платежу, а отримує негайну відповідь про прийняття запиту, а фактичний результат приходить пізніше
через чергу повідомлень.
    
    
