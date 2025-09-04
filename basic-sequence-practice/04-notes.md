Використання нотаток для пояснень.

```mermaid
sequenceDiagram
    participant User
    participant CRM

    Note over User,CRM: Початок процесу
    User->>CRM: Submit order
    CRM-->>User: Confirmation
    Note left of User: Завершення
