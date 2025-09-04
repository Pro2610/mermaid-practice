# AI-Generated Diagram — Login Process

Цей приклад був згенерований ШІ за текстовим описом процесу входу в систему.

**Сценарій:**  
Користувач вводить логін і пароль → CRM перевіряє дані у базі → якщо правильні — доступ надано, якщо ні — показується повідомлення про помилку.

```mermaid
sequenceDiagram
    participant User as Користувач
    participant CRM as CRM Система
    participant DB as База даних

    User->>CRM: Вводить логін і пароль
    activate CRM
    
    CRM->>DB: Перевіряє облікові дані
    activate DB
    
    DB-->>CRM: Повертає результат перевірки
    deactivate DB
    
    alt Правильні дані
        CRM-->>User: Доступ надано (успішна авторизація)
        Note over User, CRM: Користувач отримує доступ до системи
    else Неправильні дані
        CRM-->>User: Повідомлення про помилку
        Note over User, CRM: Доступ заборонено
    end
    
    deactivate CRM
