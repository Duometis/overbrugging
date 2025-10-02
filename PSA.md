```mermaid
sequenceDiagram
Note over HIS: GP system
    participant HIS
    participant LSP

  
    participant A as NCP country NL
    participant B as NCP country ES
    B->>A: request ePS
    A->>LSP: request SAZ
Note right of LSP: Acute Care buildingblocks
   
    LSP->>HIS: request SAZ
    HIS->>LSP: response SAZ
    HIS-->>LSP: response SAZ
     LSP->>A: response bundle SAZ

    A->>B: pivot ePS
    A->>B: original document(pdf)
