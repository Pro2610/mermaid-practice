Промпт 1 — Login process

Створи Mermaid sequence diagram для процесу авторизації користувача.
Учасники: User, CRM, Database.
Кроки:

User вводить логін і пароль.

CRM надсилає дані у Database.

Database перевіряє їх.

Якщо вірні → CRM надає доступ користувачу.

Якщо невірні → CRM показує помилку.
Використай конструкцію alt/else для успішного та невдалого сценарію.

```mermaid
sequenceDiagram
    participant User as User
    participant CRM as CRM
    participant Database as Database

    User->>CRM: Вводить логін і пароль
    activate CRM
    
    CRM->>Database: Надсилає дані для перевірки
    activate Database
    
    Database->>Database: Перевіряє логін і пароль
    
    Database-->>CRM: Повертає результат перевірки
    deactivate Database
    
    alt Дані вірні
        CRM-->>User: Надає доступ користувачу
    else Дані невірні
        CRM-->>User: Показує помилку
    end
    
    deactivate CRM
