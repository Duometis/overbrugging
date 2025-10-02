# eP sequence diagram - high level

```mermaid
sequenceDiagram
    participant XIS
    participant LSP

  
    participant A as NCP country A
    participant B as NCP country B
    B->>A: request eP
    A->>LSP: request eP (active prescriptions)
   
    LSP->>XIS: request eP 
  XIS-->>LSP: response (AIS) ??
  XIS-->>LSP: response (HIS) ??
  XIS-->>LSP: response (EPD) ??
  XIS-->>LSP: response (EPD) ??
  LSP->>A: response bundle (active prescriptions)
    A->>A: transformation + transcoding
    A->>B: pivot eP
    A->>B: original document(pdf)
