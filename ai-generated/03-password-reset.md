# AI-Generated Diagram — Password Reset Flow

Цей приклад був згенерований ШІ за текстовим описом процесу відновлення пароля.

**Сценарій:**  
Користувач запитує відновлення → CRM надсилає посилання на email → Користувач переходить за посиланням → CRM перевіряє токен → якщо валідний — користувач вводить новий пароль.

```mermaid
sequenceDiagram
    participant User as Користувач
    participant CRM as CRM Система
    participant Email as Email Service
    participant DB as База даних

    User->>CRM: Запитує відновлення пароля
    activate CRM
    
    CRM->>DB: Генерує та зберігає токен відновлення
    activate DB
    DB-->>CRM: Підтверджує збереження токена
    deactivate DB
    
    CRM->>Email: Надсилає посилання з токеном на email
    activate Email
    Email-->>User: Доставляє листа з посиланням
    deactivate Email
    
    User->>CRM: Переходить за посиланням (з токеном)
    
    CRM->>DB: Перевіряє валідність токена
    activate DB
    DB-->>CRM: Повертає результат перевірки
    deactivate DB
    
    alt Токен валідний
        CRM-->>User: Показує форму для нового пароля
        User->>CRM: Вводить новий пароль
        CRM->>DB: Оновлює пароль та видаляє токен
        activate DB
        DB-->>CRM: Підтверджує оновлення
        deactivate DB
        CRM-->>User: Підтвердження зміни пароля
    else Токен невалідний або прострочений
        CRM-->>User: Повідомлення про помилку
        Note over User, CRM: Токен недійсний або час дії вичерпано
    end
    
    deactivate CRM
