
flowchart LR
  %% =======================
  %% Conceptual Architecture
  %% NL Sources -> Canonical ADA (v1, myHealth@EU-aligned) -> EU Targets
  %% with migration path to Canonical v2 (HL7 Europe EPS/MPD)
  %% Focus: Medication + Problems
  %% =======================

  %% -------- Sources --------
  subgraph NL_Sources["NL Sources (input)"]
    direction TB

    subgraph GP["GP systems"]
      direction TB
      GP_CDA["CDA statements\n(Acute Zorg / GP summary)"]
      GP_FHIR["FHIR NL R4 profiles\n(later / mixed)"]
    end

    subgraph HOSP["Hospital / other systems"]
      direction TB
      HOSP_CDA["CDA statements\n(BgZ, MP9)"]
      HOSP_FHIR["FHIR NL R4 profiles\n(later / mixed)"]
    end

    subgraph OTHER["Other sources"]
      direction TB
      LAB["Lab/LIS\n(various)"]
      REG["Registries\n(e.g., vaccinations)"]
    end
  end

  %% -------- Canonical v1 (ADA, myHealth@EU-first) --------
  subgraph CAN_V1["Canonical v1 (ADA / ART-DECOR)\nAligned to myHealth@EU datasets (Option B)"]
    direction TB

    subgraph CAN_MED_V1["Medication Canonical (v1)"]
      direction TB
      MED_COMMON["medication_common\n- id, status, period\n- product (G-standaard + EU code)\n- dosage (text/structured)\n- prescriber\n- translation fallback (NL→EN)"]
      MED_EP["ep_prescription_line\n+ dispense_request\n(quantity, repeats, substitution)"]
      MED_ED["ed_dispensation_line\n+ actual dispensed product/qty"]
      MED_PS["ps_medication_statement\n(summary / current meds)"]
      MED_COMMON --> MED_PS
      MED_COMMON --> MED_EP
      MED_COMMON --> MED_ED
    end

    subgraph CAN_PROB_V1["Problems Canonical (v1)"]
      direction TB
      PROB_COMMON["problem_common\n- id, status\n- code (SNOMED/ICPC/etc.)\n- onset/abatement\n- verification\n- recorder/source"]
      PROB_PS["ps_problem_entry\n(problem list in PS)"]
      PROB_COMMON --> PROB_PS
    end
  end

  %% -------- EU Targets (myHealth@EU / eHN) --------
  subgraph EU_Targets["EU Targets (output)\nmyHealth@EU / eHealth Network (CDA today)"]
    direction TB
    EU_PS["EU Patient Summary CDA\n- Medication section\n- Problems section\n(+ others over time)"]
    EU_EP["EU ePrescription CDA"]
    EU_ED["EU eDispensation CDA"]
  end

  %% -------- OpenNCP services / responsibilities --------
  subgraph OpenNCP["OpenNCP / NCPeH pipeline responsibilities"]
    direction TB
    TRANSCODE["Terminology transcoding (≈80%)\n- MVC mappings\n- G-standaard→EU identifiers\n- value-set transcoding"]
    UPLOAD["Mapping table upload cycle\n(per MVC release)"]
    TRANSLATE["NL→EN display translation fallback\n(mapping.xml curated by Nictiz)"]
  end

  %% -------- Canonical v2 (future) --------
  subgraph CAN_V2["Canonical v2 (future ~2 years)\nAligned to HL7 Europe EPS / MPD logical models"]
    direction TB
    V2_EPS["EPS-shaped canonical\n(Patient Summary concepts)"]
    V2_MPD["MPD-shaped canonical\n(Prescription & Dispense concepts)"]
  end

  %% =======================
  %% Flows: Sources -> Canonical v1
  %% =======================
  GP_CDA -->|"Adapter XSLT\n(CDA→ADA v1)"| MED_COMMON
  GP_FHIR -->|"Adapter mapping\n(FHIR→ADA v1)"| MED_COMMON
  HOSP_CDA -->|"Adapter XSLT\n(CDA→ADA v1)"| MED_COMMON
  HOSP_FHIR -->|"Adapter mapping\n(FHIR→ADA v1)"| MED_COMMON

  GP_CDA -->|"Adapter XSLT\n(CDA→ADA v1)"| PROB_COMMON
  GP_FHIR -->|"Adapter mapping\n(FHIR→ADA v1)"| PROB_COMMON
  HOSP_CDA -->|"Adapter XSLT\n(CDA→ADA v1)"| PROB_COMMON
  HOSP_FHIR -->|"Adapter mapping\n(FHIR→ADA v1)"| PROB_COMMON

  %% =======================
  %% OpenNCP interactions
  %% =======================
  MED_COMMON -.->|"code/value-set transcoding"| TRANSCODE
  PROB_COMMON -.->|"code/value-set transcoding"| TRANSCODE
  TRANSLATE -.->|"EN display when\nno MVC mapping"| MED_COMMON
  UPLOAD -.-> TRANSCODE

  %% =======================
  %% Canonical v1 -> EU outputs
  %% =======================
  MED_PS -->|"Generator XSLT\n(ADA v1→EU PS CDA)"| EU_PS
  PROB_PS -->|"Generator XSLT\n(ADA v1→EU PS CDA)"| EU_PS

  MED_EP -->|"Generator XSLT\n(ADA v1→EU eP CDA)"| EU_EP
  MED_ED -->|"Generator XSLT\n(ADA v1→EU eD CDA)"| EU_ED

  %% =======================
  %% Migration path: v1 -> v2
  %% =======================
  CAN_V1 -->|"Canonical-to-canonical mapping\n(v1 ADA→v2 ADA/FHIR-shaped)"| CAN_V2
  V2_EPS -.->|"Future outputs (FHIR-based)\nwhen adopted"| EU_PS
  V2_MPD -.->|"Future outputs (FHIR-based)\nwhen adopted"| EU_EP
  V2_MPD -.->|"Future outputs (FHIR-based)\nwhen adopted"| EU_ED

