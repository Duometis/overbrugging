# Use of codesystems HL7
```mermaid
flowchart TD
    A((start)) --> B(check external codesystems and HL7 codesystems on terminology.hl7.org)
B --> C{Is there an external code system listed that you can use that scopes the need?}
C -->|Yes| D[the canonical CodeSystem URL SHALL be used]
D --> E{Are the desired codes within the scope of the existing HL7 code system?}
E -->|Yes| F((end))
E -->|No| G[E:Work with HTA to request new codes in the external code system]
C -->|No| H{Is there an HL7 internal code system in THO you can use that scopes the need?}
H -->|Yes| I[the canonical CodeSystem URL SHALL be used]
I --> J{Are the desired codes within the scope of the existing HL7 code system?}
J -->|Yes| K((end))
J -->|No| L[Add the needed codes through the existing HL7 code system using UTG]
H -->|No| M{Is there an existing external code system NOT in THO that you want to use that scopes the need?}
M -->|Yes| N[Implementers SHALL follow the HTA defined process for validating and requesting identifyers for external codesystems and idenfifier systems to request one, if not already validated by HTA]
M -->|No| O[request new HL7 code system resource]
 


