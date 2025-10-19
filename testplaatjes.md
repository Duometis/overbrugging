
flowchart LR
    A((Client)):::client -.-> B((API Gateway)):::edge
    B -.-> C((Auth Service)):::platform
    B -.-> D((Domain Logic)):::domain
    D -.-> E((Database)):::data

    classDef client fill:#e0f7fa,stroke:#00796b,stroke-dasharray:3 3,color:#004d40;
    classDef edge fill:#fffde7,stroke:#f57f17,stroke-dasharray:3 3,color:#795548;
    classDef platform fill:#fce4ec,stroke:#ad1457,stroke-dasharray:3 3,color:#880e4f;
    classDef domain fill:#e8f5e9,stroke:#2e7d32,stroke-dasharray:3 3,color:#1b5e20;
    classDef data fill:#ede7f6,stroke:#4527a0,stroke-dasharray:3 3,color:#311b92;
