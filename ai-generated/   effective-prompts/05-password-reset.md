Промпт 2 — Password reset

Створи Mermaid sequence diagram для процесу відновлення пароля.
Учасники: User, CRM, Email Service, Database.
Кроки:

User надсилає запит на відновлення.

CRM генерує токен і надсилає його через Email Service.

User отримує email і переходить за посиланням.

CRM перевіряє токен у Database.

Якщо токен валідний → User вводить новий пароль, CRM оновлює дані в Database.

Якщо токен невалідний → CRM показує помилку.
Використай alt/else для valid/invalid token.

```mermaid
sequenceDiagram
    participant User as User
    participant CRM as CRM
    participant Email as Email Service
    participant Database as Database

    User->>CRM: Надсилає запит на відновлення пароля
    activate CRM
    
    CRM->>CRM: Генерує токен відновлення
    
    CRM->>Database: Зберігає токен
    activate Database
    Database-->>CRM: Підтверджує збереження
    deactivate Database
    
    CRM->>Email: Надсилає токен через Email Service
    activate Email
    Email-->>User: Доставляє email з посиланням
    deactivate Email
    
    User->>CRM: Переходить за посиланням з токеном
    
    CRM->>Database: Перевіряє токен
    activate Database
    Database-->>CRM: Повертає результат перевірки
    deactivate Database
    
    alt Токен валідний
        CRM-->>User: Показує форму для нового пароля
        User->>CRM: Вводить новий пароль
        CRM->>Database: Оновлює пароль в Database
        activate Database
        Database-->>CRM: Підтверджує оновлення
        deactivate Database
        CRM-->>User: Підтверджує успішну зміну пароля
    else Токен невалідний
        CRM-->>User: Показує помилку
    end
    
    deactivate CRM
