# Use of codesystems HL7
```mermaid
flowchart TD
    A((start)) --> B(check external codesystems and HL7 codesystems on terminology.hl7.org)
B --> C{Is er een bruikbaar external codesystem?}
C -->|Ja| D[gebruik deze]
D --> E{bevat dit codesystem alle values die je nodig hebt?}
E -->|Ja| F((klaar))
E -->|Nee| G[vraag nieuwe codes aan bij externe codesystem]
C -->|Nee| H{is er een HL7 internal THO codesystem dat je kan gebruiken?}
H -->|Ja| I[gebruik deze]
I --> J{bevat dit codesystem alle values die je nodig hebt?}
J -->|ja| K((Klaar))
J -->|nee| L[volg het proces deze toe te voegen UTG]
H -->|Nee| M{is er een bestaand external codesystem die toegevoegd kan worden aan THO?}
M -->|Ja| N[volg het proces om een dit externe codesystem toe te voegen]
M -->|Nee| O[volg het proces om een nieuwe HL7 code system resource toe te voegen]
 


