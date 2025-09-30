
# (draft) with G-standaard GPK-split in PS-A sequence diagram
```mermaid
sequenceDiagram

participant B as NCP country B
participant C as LSP
participant A as NCP country A (Netherlands)

B->>A: request for PS
A->>C: request for AZ-subset
C->>A: response bundle AZ-subset (using VWI and MITZ)
create participant XSLT
 
    A->>XSLT: response bundle AZ-subset

    A->>XSLT: params: id, setId
  
    XSLT->>XSLT: convert to ePS format
    XSLT->>XSLT : eHDSI friendly GPK-split
    XSLT->>XSLT: add translated valueset items

  create participant TS
    XSLT->>TS : eHDSI friendly + NEC/OTH + GPK-split
   TS->>TS: add CTS valueset items

    TS->>A: pivot
A->>A: create 'original document'

A->>B: pivot

A->>B: original document

B->>B: translation and transcoding pivot

