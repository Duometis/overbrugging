# eHDSI Medication Summary

Target: [Template  eHDSI Medication Summary](https://art-decor.ehdsi.eu/publication/epsos-html-20240422T073854/tmp-1.3.6.1.4.1.12559.11.10.1.3.1.2.3-2020-09-07T095657.html)

Target: 
- [eHDSI Medication Item](https://art-decor.ehdsi.eu/publication/epsos-html-20240422T073854/tmp-1.3.6.1.4.1.12559.11.10.1.3.1.3.4-2024-01-25T135932.html)
- [eHDSI PS Medication Information](https://art-decor.ehdsi.eu/publication/epsos-html-20240422T073854/tmp-1.3.6.1.4.1.12559.11.10.1.3.1.3.31-2022-01-11T164400.html)

- Current and relevant past medicines: Relevant prescribed medicines whose period of time indicated for the treatment has not yet expired whether it has been dispensed or not, or medicines that influence current health status or are relevant to a clinical decision.

Source: [MP HL7 Medicatieafspraken Organizer](https://decor.nictiz.nl/pub/medicatieproces/mp-html-20181220T121121/tmp-2.16.840.1.113883.2.4.3.11.60.20.77.10.9265-2018-12-13T000000.html)

Source MA: [MP CDA Medicatieafspraak](https://decor.nictiz.nl/pub/medicatieproces/mp-html-20181220T121121/tmp-2.16.840.1.113883.2.4.3.11.60.20.77.10.9235-2018-12-04T143321.html)


## template Medication Item
| name | description |
| ----------- | ----------- |
| Start and Stop Date | The date (and time if available) when the medication regimen began and is expected to finish. The first component of the <effectiveTime> encodes the lower and upper bounds over which the <substanceAdministration> occurs, and the start time is determined from the lower bound. If the medication has been known to be stopped, the high value must be present, but expressed as a flavor of null (e.g., Unknown)|
| Frequency | The frequency indicates how often the medication is to be administered. It is often expressed as the number of times per day, but which may also include information such as 1 hour before/after meals, or in the morning, or evening.The second <effectiveTime> element encodes the frequency. In cases where split or tapered doses are used, these may be found in subordinate <substanceAdministration> elements|
| Route |The route is a coded value, and indicates how the medication is received by the patient (by mouth, intravenously, topically, et cetera)|
| Dose | The amount of the medication given. This should be in some known and measurable unit, such as grams, milligrams, et cetera. It may be measured in "administration" units (such as tablets or each), for medications where the strength is relevant. In this case, only the unit count is specified , no units are specified. It may be a range|
| Product | The name of the substance or product. This should be sufficient for a provider to identify the kind of medication. It may be a trade name or a generic name. This information is required in all medication entries. If the name of the medication is unknown, the type, purpose or other description may be supplied. The name should not include packaging, strength or dosing information. Note: Due to restrictions of the CDA schema, there is no way to explicitly link the name to the narrative text |
| Strength | The strength of the medication is expressed as a the ratio of each active ingredient to a unit of medication. For example, the medication Percocet comes in a variety of strengths, which indicate specific amounts of two different medications being received in single tablet. Another example is eye-drops, where the medication is in a solution of a particular strength, and the dose quantity is some number of drops. Note: Due to restrictions of the CDA schema, there is no way to separately record the strength. The epSOS extension is used to provide this information. In order to be compliant with the IHE PCC template strength information should be also conveyed through the consumable/code/originalText element as reference to the narrative block |
| Ingredient Code | A code describing the active ingredient(s) of the product from a controlled vocabulary, such as ATC, for example |
| Instructions | A place to put free text comments to support additional relevant information, or to deal with specialized dosing instructions. For example, "take with food", or tapered dosing|
| Indication |	A link to supporting clinical information about the reason for providing the medication (e.g., a link to the relevant diagnosis)|


