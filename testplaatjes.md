flowchart LR
    %% Nodes
    A((Client)):::node -.-> B((API Gateway)):::node
    B -.-> C((Auth Service)):::node
    B -.-> D((Business Logic)):::node
    D -.-> E((Database)):::node

    %% Styles
    classDef node fill:none,stroke:#555,stroke-dasharray:3 3,stroke-width:2px,color:#222,font-weight:bold;
