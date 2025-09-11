"Sequence Diagram - Managed POS Authorization Flow"

POS/каса: касир формує корзину і отримує суму;

Cardholder обирає спосіб оплати (Card/Cash);

якщо обрано картку — POS автоматично передає суму й тип транзакції на термінал;

cardholder оплачує на терміналі (PIN/CDCVM за потреби);

термінал надсилає авторизацію через gateway до provider; відповідь повертається на термінал і в POS;

POS закриває чек як PAID / або показує відмову; показ/чеки.


```mermaid
sequenceDiagram
    participant C as Cardholder
    participant M as Merchant
    participant POS as POS System (Cash Register)
    participant T as Managed POS Terminal
    participant G as Payment Gateway
    participant P as Provider

    rect rgb(245,245,245)
    note over M,POS: Managed Mode — касир працює в POS, який керує терміналом
    M->>POS: Scan items / finalize basket
    POS-->>M: Show total amount
    C-->>POS: Choose payment method (Card or Cash)
    end
    
    alt Payment method = Card
        POS->>T: Initiate payment (amount + transaction type)
        T-->>POS: Acknowledge / display amount

        C->>T: Tap/Insert/Swipe card (or mobile wallet)
        T->>T: Read PAN/EMV data & build auth request

        alt PIN required?
            T-->>C: Prompt for PIN
            C->>T: Enter PIN
            T->>T: Encrypt PIN block (CVM)
        else No PIN/CDCVM
            T->>T: Set CVM = CDCVM/Signature/None
        end

        rect rgba(255,230,150,.30)
        T->>G: Send authorization request (amount, currency, EMV tags, CVM)
        G->>P: Forward for authorization
        P-->>G: Auth response (APPROVED/DECLINED + codes)
        G-->>T: Map & return response
        end

        T-->>POS: Payment result (Approved/Declined + auth code/reason)

        alt Approved
            POS-->>M: Mark order as PAID
            T-->>C: Show approval / (optional) print card receipt
            POS-->>C: Print sales receipt (optional)
            T->>T: Store transaction in batch (for capture/settlement)
        else Declined
            POS-->>M: Show decline on POS
            T-->>C: Display decline message
            opt Retry or alternate tender?
                POS->>T: Retry payment / choose different tender
            end
        end

        note over T,P: End of online authorization cycle
    else Payment method = Cash
    
        POS-->>M: Handle cash tender (no terminal interaction)
    end

    
