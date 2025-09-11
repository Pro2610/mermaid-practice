"Sequence Diagram - Standalone POS Authorization Flow"
Merchant вводить суму на терміналі;
cardholder оплачує;
термінал надсилає авторизацію через gateway до provider;
відповідь повертається на термінал;
показ/чек


```mermaid
sequenceDiagram
    title Standalone POS — Authorization Flow (Terminal ↔ Provider)
    participant C as Cardholder
    participant M as Merchant
    participant T as Standalone POS Terminal
    participant G as Payment Gateway
    participant P as Provider

    rect rgb(245,245,245)
    note over M,T: Standalone Mode — merchant вводить суму та тип транзакції
    M->>T: Input amount + transaction type (sale/refund)
    T-->>M: Display amount for confirmation
    end

    C->>T: Tap/Insert/Swipe card (or mobile wallet)
    T->>T: Read PAN/EMV data & build auth request
    alt PIN required?
        T-->>C: Prompt for PIN
        C->>T: Enter PIN
        T->>T: Encrypt PIN block (CVM)
    else No PIN
        T->>T: CDCVM/Signature/No CVM
    end

    T->>G: Send authorization request
    G->>P: Forward for online authorization
    P-->>G: Authorization response (APPROVED/DECLINED + code)
    G-->>T: Map & return response

    alt APPROVED
        T-->>M: Show "Approved" + auth code
        T-->>C: Display approval / print receipt (optional)
        T->>T: Store transaction in batch
    else DECLINED
        T-->>M: Show "Declined" + reason
        T-->>C: Display decline message
        opt Retry?
            M->>T: Initiate retry / different method
        end
    end

    note over T: End of online authorization cycle

