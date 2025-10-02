# ePeD sequence diagram - high level

```mermaid
sequenceDiagram
    participant XIS
    participant LSP

  
    participant A as NCP country A
    participant B as NCP country B
    B->>A: request ePS
    A->>LSP: request SAZ
Note right of LSP: Acute Care buildingblocks
   
    LSP->>XIS: request SAZ
    XIS->>LSP: response SAZ
    XIS-->>LSP: response SAZ
     LSP->>A: response bundle SAZ

    A->>B: pivot ePS
    A->>B: original document(pdf)
