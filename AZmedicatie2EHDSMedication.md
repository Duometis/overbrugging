# 🇳🇱 NL Medicatieproces CDA → 🇪🇺 eHDSI Medication Item CDA Mapping

## Metadata

- **Source template**: *MP CDA Medicatieafspraak inhoud* — `2.16.840.1.113883.2.4.3.11.60.20.77.10.9233`
- **Target template**: *eHDSI Medication Item* — `1.3.6.1.4.1.12559.11.10.1.3.1.3.4`
- **Namespaces**: `xmlns:cda="urn:hl7-org:v3"`
- **Scope**: identificatie, medicament, periode/timing, route, dosering, sterkte, auteur, reden.

---

## 1️⃣ Hoofd-mappingtabel

| # | Source.XPath (MP) | Target.XPath (eHDSI) | Target.Cardinality | Datatype/Format | Transform.Expression | ValueSet/CodeSystem.Map | Conditions | Default/NullFlavor | Multiplicity/JoinKey | Status | Notes |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 1 | `/cda:entry/cda:substanceAdministration/cda:templateId/@root='…9233'` | `/cda:entry/cda:substanceAdministration/cda:templateId/@root='…3.1.3.4'` | 1..1 | II→II | copy | – | – | – | – | ✅ Mapped | Template marker |
| 2 | `cda:id[@root and @extension]` | `cda:id[@root and @extension]` | 0..1 | II→II | copy | – | – | – | – | ✅ Mapped | Unieke entry ID |
| 3 | `cda:code[@code='16076005']` | `cda:code` | 1..1 | CD→CD | copy | SNOMED → ATC | – | – | – | ⚠️ Needs review | eHDSI gebruikt consumable voor medicament |
| 4 | `cda:text` | `cda:text/cda:reference/@value` | 0..1 | ED→TEL | set `#med-1` | – | narrative aanwezig | – | – | ✅ Mapped | Narrative anchor |
| 5 | `cda:statusCode/@code` | `cda:statusCode/@code` | 1..1 | CS→CS | copy | – | – | – | – | ✅ Mapped | status=completed |
| 6 | `cda:effectiveTime (low/high)` | `cda:effectiveTime (IVL_TS)` | 0..1 | TS→TS | normalize | – | – | – | – | ✅ Mapped | Start/stop-periode |
| 7 | `cda:effectiveTime (dosering)` | `cda:effectiveTime (PIVL_TS)` | 0..* | TS→TS | map pattern | – | – | – | – | ✅ Mapped | Frequentie/herhaling |
| 8 | `cda:routeCode` | `cda:routeCode` | 0..1 | CE→CE | map | NL→eHDSI route | – | – | – | ⚠️ Needs review | Routecodes afstemmen |
| 9 | `cda:consumable/.../manufacturedMaterial/cda:name` | `cda:consumable/.../manufacturedMaterial/cda:name` | 1..1 | ST→EN | copy | – | – | – | – | ✅ Mapped | Productnaam |
|10 | `.../manufacturedMaterial/cda:code` | `.../manufacturedMaterial/cda:code` | 0..1 | CD→CD | map | SNOMED → ATC | – | – | – | ⚠️ Needs review | Productcode |
|11 | `.../ingredient/.../code` | `.../ingredient/.../code` | 0..* | CD→CD | copy | SNOMED → ATC | – | – | key=code | ✅ Mapped | Ingrediënten |
|12 | `.../ingredient/.../quantity` | `.../ingredient/.../quantity` | 0..* | RTO/PQ | normalize ratio | UCUM | – | – | – | ✅ Mapped | Sterkte |
|13 | `entryRelationship[@typeCode='COMP']/Dosering` | `cda:doseQuantity` | 0..1 | PQ→PQ | extract value/unit | UCUM | – | – | – | ✅ Mapped | Dosering per inname |
|14 | `cda:author` | `cda:author` (Prescriber) | 0..1 | Participation | map | – | – | – | – | ✅ Mapped | Voorschrijver |
|15 | `entryRelationship[@typeCode='RSON']` | `Medication Reason Observation` | 0..1 | ActRef | link reason | – | – | – | – | 🕐 Open | Reden optioneel |

---

## 2️⃣ CodeMap

| Source.CodeSystem | Source.Code | Source.Display | Target.CodeSystem | Target.Code | Target.Display | Notes |
|---|---|---|---|---|---|---|
| SNOMED CT | 16076005 | Medicatieafspraak | – | – | – | Niet overnemen als productcode |
| NL Route | 8 | auriculair | eHDSI route VS | (tbd) | (tbd) | Route mapping vereist |
| SNOMED Product | (tbd) | (tbd) | ATC | (tbd) | (tbd) | Waar mogelijk ATC gebruiken |

---

## 3️⃣ Units / UCUM

| Source.Unit | Target (UCUM) | Factor | Rounding | Applies-to | Notes |
|---|---|---|---|---|---|
| mg | mg | 1 | – | doseQuantity, strength | UCUM gelijk |
| µg | ug | 1 | – | doseQuantity, strength | UCUM “ug” |
| mL | mL | 1 | – | volume | geen conversie nodig |

---

## 4️⃣ Aanvullende opmerkingen

- **effectiveTime**: eerste `IVL_TS` = start/stop; tweede = frequentie (PIVL/EIVL).  
- **Product**: eHDSI verwacht naam, code, ingrediënt en sterkte.  
- **Narrative**: gebruik `text/reference @value="#id"` conform eHDSI voorbeelden.  
- **Author**: mappen naar eHDSI Prescriber include.  
- **Reason**: optioneel; in sommige implementaties vervallen.

---

## 5️⃣ Metadata

| Field | Description |
|--------|--------------|
| **Source Template ID** | 2.16.840.1.113883.2.4.3.11.60.20.77.10.9233 |
| **Target Template ID** | 1.3.6.1.4.1.12559.11.10.1.3.1.3.4 |
| **Version** | 2018-12-04 → 2024-01-25 |
| **Mapping Author** | – |
| **Last Reviewed** | – |
| **Status Legend** | ✅ Mapped / ⚠️ Needs review / 🕐 Open |
