# total flowchart Use of codesystems HL7
```mermaid
flowchart TD
    1((start)) --> 2(check external codesystems and HL7 codesystems on terminology.hl7.org)
2 --> 3{Is there an external code system listed that you can use that scopes the need?}
3 -->|Yes| 4[the canonical CodeSystem URL SHALL be used]
4 --> 5{Are the desired codes within the scope of the existing HL7 code system?}
5 -->|Yes| 6((end))
5 -->|No| 7[E:Work with HTA to request new codes in the external code system]
3 -->|No| 8{Is there an HL7 internal code system in THO you can use that scopes the need?}
8 -->|Yes| 9[the canonical CodeSystem URL SHALL be used]
9 --> 10{Are the desired codes within the scope of the existing HL7 code system?}
10 -->|Yes|100((end))
10 -->|No| 11[Add the needed codes through the existing HL7 code system using UTG]
8 -->|No| 13{Is there an existing external code system NOT in THO that you want to use that scopes the need?}
13 -->|Yes| 14[Implementers SHALL follow the HTA defined process for validating and requesting identifyers for external codesystems and idenfifier systems to request one, if not already validated by HTA]
13 -->|No| 15{Is the concept so tightly tied to the structures or usage of the IG that it cannot evolve without a new publicaiton of the specification?}
15 -->|Yes| 16[seek TSMG approval via an email to the tsmg-cc@list.hl7.org]
16 --> 17[Define the codesystem within your own speification with a canonical URL specific to your specification]
13 -->|No| 18{will the concept ONLY be used to create a value set bound with Example binding strength?}
18 -->|yes| 19[the concept and code system is IG-specific and should never be used in production systems]
19 --> 20[Add the code and codesystem to your IG and do nog add to THO]
20 --> 21[If a new code system is created, then the name SHALL end in the string 'Example' to clarify that the code system is only to be used for example bindings]
18 -->|No| 22{Is there a demand for use of the code system outside of implementing the original IG?}
22 -->|Yes| 23[Build the required code system using UTG so that the final code system will be born in THO]
22 -->|No| 24[Create a new IG-internal THO code system: Create your own codesystem name and identifyer -URL- and it SHALL have an anchor of http://terminology.hl7.org/CodeSystem/
The canonical URL SHALL follow this pattern http://terminology.hl7.org/CodeSystem/XXXXX where XXXXX is a meaningfull text string. confirm that the resulting Namesystem resource does not have a conflict with an existing code system with the same URL]
24 --> 25[A NamingSystem resrouce for tracking the identifiers in terminology.hl7.org for your CodeSystem will be created]
25 --> 26[The CodeSystem resource content SHOULD be created and maintained via the initiating IG build process until stable enough to be moved to THO. Define concepts and codes for the codesystem within the IG until confident the concepts will nog change or when ready to seek approval/publish a FHIR IG at FMM3]
26 --> 27[when concepts will not change or when ready to seek approval/publish a FHIR IG at FMM3, move the codesystem to THO]

 


