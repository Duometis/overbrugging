# eHDSI Medication Summary

Huidige en relevante vroegere medicatie: Relevante voorgeschreven geneesmiddelen waarvan de behandelperiode nog niet is verstreken, ongeacht of ze al zijn afgeleverd of niet, of geneesmiddelen die invloed hebben op de huidige gezondheidstoestand of relevant zijn voor een klinische beslissing.

Target: [Template  eHDSI Medication Summary](https://art-decor.ehdsi.eu/publication/epsos-html-20240422T073854/tmp-1.3.6.1.4.1.12559.11.10.1.3.1.2.3-2020-09-07T095657.html) -> [Template eHDSI Medication Item](https://art-decor.ehdsi.eu/publication/epsos-html-20240422T073854/tmp-1.3.6.1.4.1.12559.11.10.1.3.1.3.4-2024-01-25T135932.html)


Source: [MP HL7 Medicatieafspraken Organizer](https://decor.nictiz.nl/pub/medicatieproces/mp-html-20181220T121121/tmp-2.16.840.1.113883.2.4.3.11.60.20.77.10.9265-2018-12-13T000000.html) -> [MP CDA Medicatieafspraak](https://decor.nictiz.nl/pub/medicatieproces/mp-html-20181220T121121/tmp-2.16.840.1.113883.2.4.3.11.60.20.77.10.9235-2018-12-04T143321.html)

# gebruk van CDA Templates in eHDSI Medication Summary
```mermaid
flowchart LR
    1(eHDSI Medication Summary) --> 2(eHDSI Medication Item)
2(eHDSI Medication Item) --> 3(eHDSI PS Medication Information)
3(eHDSI PS Medication Information) --> 4(eHDSI PS Manufactured Material)
2(eHDSI Medication Item) --> 5(eHDSI Author Prescriber)
2(eHDSI Medication Item) --> 6(eHDSI Medication FulFillment Instructions)
```

| CDA Template| Omschrijving |
| ----------- | ----------- |
|eHDSI Medication Summary |De sectie "Medicatieoverzicht" moet een beschrijving bevatten van de medicatie van de patiënt als onderdeel van het patiëntoverzicht.|
|eHDSI Medication Item|Dit template maakt gebruik van de template voor het geneesmiddel en instructies voor de apotheker. Medicaties en hun voorschriften behoren wellicht tot de moeilijkste gegevenselementen om te modelleren, vanwege de grote variatie in de manier waarop medicijnen worden voorgeschreven.|
|eHDSI PS Medication Information|Dit beschrijft het gebruik van het geneesmiddel. Alle informatie over het geneesmiddel zelf wordt via de eHDSI PS Manufactured Material-template beschreven.|
|eHDSI PS Manufactured Material|Informatie over het geneesmiddel. Hier zit vooral het werk wat we nog moeten doen voor de G-standaard. het afleiden van de onderdelen die lost moeten worden gemapt op dit template omdat we an het geneesmiddel alleen de PRK-HPK en GPK krijgen uit de KEZO bouwsteen|
|eHDSI Author Prescriber| Hier gaat het over de voorschrijver en dat is een huisarts, specialist etc. Note: Een CDA-document moet minstens één auteur hebben. Auteurs kunnen zowel personen (assignedPerson) als apparaten (assignedAuthoringDevice) zijn. Wanneer er geen zorgverlener (persoon) is, maar de gegevens zijn samengesteld door een apparaat, bijvoorbeeld via samenvoegen door een ander systeem, wordt assignedAuthoringDevice gebruikt. Wanneer de gegevens afkomstig zijn uit verschillende bronnen en bestaande documenten die deel uitmaken van een groter systeem, is de organisatie die verantwoordelijk is voor die gegevensverzameling degene die het patiëntoverzicht (PS) “ondertekent” als verantwoordelijke.|
|eHDSI Medication FulFillment Instructions|Template voor aanvullende instructies aan de apotheker, bijvoorbeeld om aan te geven dat het etiket in het Spaans moet worden opgesteld, enzovoort.|



