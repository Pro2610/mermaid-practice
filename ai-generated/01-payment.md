# AI-Generated Diagram — Online Payment

Цей приклад був згенерований ШІ за текстовим описом процесу онлайн-платежу.

**Сценарій:**  
Користувач вводить дані картки → CRM надсилає їх у Payment Gateway → Gateway повертає результат (успіх або помилка) → CRM показує результат користувачу.

```mermaid
sequenceDiagram
    participant User as Користувач
    participant CRM as CRM Система
    participant PG as Payment Gateway

    User->>CRM: Вводить дані картки (номер, CVV, термін дії)
    activate CRM
    
    CRM->>PG: Надсилає запит на обробку платежу
    activate PG
    
    PG-->>CRM: Повертає результат (успіх або помилка)
    deactivate PG
    
    alt Успішний платіж
        CRM-->>User: Підтвердження успішного платежу
    else Помилка платежу
        CRM-->>User: Повідомлення про помилку
    end
    
   
