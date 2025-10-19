🧩 Metadata
| Field                  | Description                      |
| ---------------------- | -------------------------------- |
| **Namespace prefixes** | `xmlns:cda="urn:hl7-org:v3"`     |
| **Source Template ID** | `2.16.840.1.113883.10.20.22.1.1` |
| **Target Template ID** | `2.16.840.1.113883.10.20.22.1.2` |
| **Version**            | v3.1 → v3.2                      |
| **Mapping Author**     | –                                |
| **Last Reviewed**      | –                                |
| **Status Legend**      | ✅ Mapped ⚠️ Needs review 🕐 Open |


🗂️ CDA → CDA Mapping Table
| # | Source.Path                                                                   | Target.Path                                                                   | Target.Cardinality | Datatype/Format   | Transform.Expression                        | ValueSet/CodeSystem.Map      | Conditions               | Default/NullFlavor | Multiplicity/JoinKey | Status          | Notes                       |
| - | ----------------------------------------------------------------------------- | ----------------------------------------------------------------------------- | ------------------ | ----------------- | ------------------------------------------- | ---------------------------- | ------------------------ | ------------------ | -------------------- | --------------- | --------------------------- |
| 1 | `/cda:ClinicalDocument/cda:recordTarget/cda:patientRole/cda:patient/cda:name` | `/cda:ClinicalDocument/cda:recordTarget/cda:patientRole/cda:patient/cda:name` | 1..1               | ST → ST           | `normalize-space(concat(given,' ',family))` | –                            | –                        | –                  | –                    | ✅ Mapped        | Naam direct kopiëren        |
| 2 | `//cda:observation[cda:code/@code='12345-6']/cda:value/@value`                | `//cda:observation[cda:code/@code='ABC']/cda:value/@value`                    | 0..1               | PQ → PQ           | `value * 0.001`                             | –                            | als `@unit='mg'`         | –                  | –                    | ✅ Mapped        | Eenheidsconversie mg→g      |
| 3 | `//cda:code/@code`                                                            | `//cda:code/@code`                                                            | 1..1               | CV → CV           | `mapCode(code)`                             | `SNOMED→LOINC (tbl:CodeMap)` | –                        | `UNK`              | –                    | ⚠️ Needs review | CodeMapping controleren     |
| 4 | `/cda:component/cda:structuredBody/cda:component/cda:section`                 | `/cda:component/cda:structuredBody/cda:component/cda:section`                 | 0..*               | Section → Section | `copySectionIfExists()`                     | –                            | alleen relevante secties | –                  | `section/@code`      | 🕐 Open         | Alleen opnemen als aanwezig |

📚 CodeMap Table

| Source.CodeSystem | Source.Code | Source.Display     | Target.CodeSystem | Target.Code | Target.Display            | Validity/Version | Notes      |
| ----------------- | ----------- | ------------------ | ----------------- | ----------- | ------------------------- | ---------------- | ---------- |
| SNOMED            | 12345       | “Body temperature” | LOINC             | 8310-5      | “Body temperature”        | v2025-03         | 1:1 match  |
| SNOMED            | 54321       | “Systolic BP”      | LOINC             | 8480-6      | “Systolic blood pressure” | v2025-03         | Unit check |

⚙️ Units Mapping
| Source.Unit | Target.Unit | Factor   | Rounding | Notes              |
| ----------- | ----------- | -------- | -------- | ------------------ |
| mg          | g           | 0.001    | 3        | milligram → gram   |
| mmHg        | kPa         | 0.133322 | 2        | bloeddrukconversie |


