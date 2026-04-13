sequenceDiagram
Note over XIS: GP system
    participant XIS
    participant LSP
    participant A as NCP country NL
    participant B as NCP country B
    B->>A: request ePS
    A->>LSP: ePS building blocks
Note right of LSP: Acute Care 4-5 KEZO building blocks
    LSP->>XIS: request ePS building blocks
    XIS->>LSP: response ePS building blocks
XIS-->>LSP: response ePS building blocks
Note right of XIS: in case there are multiple sources
    LSP->>A: response bundle ePS building blocks
Note right of LSP: all responses are bundled in one xml file
Note over A: transformation in NCPeH
A->>B: pivot ePS
    A->>B: original document(pdf)
