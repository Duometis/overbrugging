# 🧭 CDA → FHIR Mapping Template (R4)

## 1️⃣ Resource Emission Rules

| Resource | Create When (CDA scope) | Identity Strategy (id/fullUrl) | Profile (canonical) | Contained? | Reference Targets |
|---|---|---|---|---|---|
| Patient | recordTarget/patientRole | hash(OID+extension) | http://.../StructureDefinition/nl-core-Patient | No | Practitioner, Encounter, Composition.subject |
| Practitioner | author/performer aanwezig | hash(id/@root+@extension) | .../Practitioner | No | Observation.performer, Composition.author |
| Organization | custodian aanwezig | hash(oid) | .../Organization | No | Practitioner.organization, Composition.custodian |
| Composition | altijd 1 per document | new GUID | .../Composition | No | Sections → Composition.section |
| Observation | per CDA observation | hash(code+time+subject) | .../Observation | No | subject=Patient, performer=Practitioner |
| DocumentReference | hele CDA als bijlage | hash(document-id) | .../DocumentReference | No | relatesTo=Composition |

---

## 2️⃣ Main Mapping Table

| # | Source.XPath (CDA) | FHIR.Resource | FHIR.Path | FHIR.Type | Cardinality | Transform/Expression | Terminology Binding (system, code, display) | Unit/UCUM | Conditions | Reference/Linking | Create/Upsert | Status | Notes |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 1 | /recordTarget/patientRole/patient/name | Patient | name[0] | HumanName | 0..* | concat(given,' ',family) | – | – | – | – | Upsert | ✅ Mapped | Naam normaliseren |
| 2 | //observation[code/@code='8310-5']/value/@value | Observation | valueQuantity.value | Quantity | 0..1 | cast(decimal) | – | Cel | if @xsi:type='PQ' | subject=Patient | Create | ✅ Mapped | Lichaamstemperatuur |
| 3 | //cda:effectiveTime/@value | Observation | effectiveDateTime | dateTime | 0..1 | normalize(TS) | – | – | – | – | – | ⚠️ Needs review | Tijdzonebehoud controleren |
| 4 | /ClinicalDocument | DocumentReference | content.attachment | Attachment | 1..* | embed base64 van bron-CDA | – | – | – | relatesTo Composition | Create | ✅ Mapped | Volledige CDA als bijlage |

---

## 3️⃣ Terminology Mapping

| Source.CodeSystem | Source.Code | Source.Display | Target.system (URI) | Target.code | Target.display | Binding strength | Equivalence | Notes |
|---|---|---|---|---|---|---|---|---|
| LOINC | 8310-5 | Body temperature | http://loinc.org | 8310-5 | Body temperature | required | equivalent | Observation.code |
| SNOMED CT | 386661006 | Fever | http://snomed.info/sct | 386661006 | Fever | preferred | broader-than | – |

---

## 4️⃣ UCUM / Unit Mapping

| CDA Unit | UCUM | Factor | Rounding | Applies-to | Notes |
|---|---|---|---|---|---|
| mg | mg | 1 | – | Medication/Observation | identiek |
| °C | Cel | 1 | – | Temperature | CDA °C → UCUM Cel |
| mmHg | [mmHg] | 1 | – | Blood pressure | identiek |

---

## 5️⃣ Extensions Mapping

| Source.XPath | FHIR.Resource | Extension URL | FHIR.Path | Type | Transform | Notes |
|---|---|---|---|---|---|---|
| cda:patient/cda:birthTime/@value | Patient | http://hl7.org/fhir/StructureDefinition/patient-birthTime | extension.valueDateTime | dateTime | TS → xs:dateTime | alleen bij seconde-nauwkeurigheid |
| cda:confidentialityCode | Resource.meta | …/security-label | meta.security | Coding | code map v3→FHIR | security tagging |

---

## 6️⃣ Metadata

| Field | Description |
|---|---|
| **FHIR Release** | R4 |
| **Doelprofielen** | (bv. NL-Core, IPS) |
| **Terminology Policy** | SNOMED CT, LOINC, UCUM |
| **Id-strategie** | deterministic (hash) / GUID |
| **Review workflow** | 4-eyes, terminologie-review |
| **Status Legend** | ✅ Mapped / ⚠️ Needs review / 🕐 Open |
