# eHDSI Medication Summary

Target: [Template  eHDSI Medication Summary](https://art-decor.ehdsi.eu/publication/epsos-html-20240422T073854/tmp-1.3.6.1.4.1.12559.11.10.1.3.1.2.3-2020-09-07T095657.html)

Target: 
- [eHDSI Medication Item](https://art-decor.ehdsi.eu/publication/epsos-html-20240422T073854/tmp-1.3.6.1.4.1.12559.11.10.1.3.1.3.4-2024-01-25T135932.html)
- [eHDSI PS Medication Information](https://art-decor.ehdsi.eu/publication/epsos-html-20240422T073854/tmp-1.3.6.1.4.1.12559.11.10.1.3.1.3.31-2022-01-11T164400.html)

- Current and relevant past medicines: Relevant prescribed medicines whose period of time indicated for the treatment has not yet expired whether it has been dispensed or not, or medicines that influence current health status or are relevant to a clinical decision.

Source: [MP HL7 Medicatieafspraken Organizer](https://decor.nictiz.nl/pub/medicatieproces/mp-html-20181220T121121/tmp-2.16.840.1.113883.2.4.3.11.60.20.77.10.9265-2018-12-13T000000.html)

Source MA: [MP CDA Medicatieafspraak](https://decor.nictiz.nl/pub/medicatieproces/mp-html-20181220T121121/tmp-2.16.840.1.113883.2.4.3.11.60.20.77.10.9235-2018-12-04T143321.html)


## eHDSI dataelements eHDSI template Medication Item
| eHDSI data element | name | description | remarks |
| ----------- | ----------- |-----------  |----------- | 
| Duration of treatment + Date of onset of treatment + Medicine status  | Start and Stop Date | The date (and time if available) when the medication regimen began and is expected to finish. The first component of the <effectiveTime> encodes the lower and upper bounds over which the <substanceAdministration> occurs, and the start time is determined from the lower bound. If the medication has been known to be stopped, the high value must be present, but expressed as a flavor of null (e.g., Unknown)|
| Frequency of intakes | Frequency |
| Medication Item | Route |
| Medication Item | Dose |
| Medication Item | Product |
| Medication Item | Strength |
| Medication Item | Ingredient Code |
| Medication Item | Instructions |


