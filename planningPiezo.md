# PIEZO – Programma Implementatie Europese Zorgdiensten

## Overzicht

Planning gebaseerd op de aangeleverde Gantt-chart.

---

# Mijlpalen

| Mijlpaal | Periode |
|---|---|
| PrePPT eP/eD | Q4 2027 |
| Freeze fase | Q1–Q2 2028 |
| Aanvraag Go-Live eP/eD | Q3 2028 |

## Freeze fase omvat

- Bevindingen verwerken
- Kleine aanpassingen
- Ketentesten
- Initial compliance check

---

# Planning

## PS-A Plateau 2 en verder

| Activiteit | Start | Eind |
|---|---|---|
| Voorbereiding en planning | Q1 2026 | Q2 2026 |
| Ontwerp | Q2 2026 | Q2 2027 |
| Realisatie en testen | Q2 2026 | Q4 2028 |
| Implementatie | Q1 2027 | Q4 2028 |
| In beheername | Q1 2027 | Q4 2028 |

---

## eP / eD A en B

| Activiteit | Start | Eind |
|---|---|---|
| Voorbereiding en planning | Q1 2026 | Q4 2026 |
| Ontwerp | Q2 2026 | Q2 2027 |
| Realisatie en testen | Q3 2026 | Q4 2028 |
| Implementatie | Q1 2027 | Q4 2028 |
| In beheername | Q1 2027 | Q4 2028 |

---

## PS-B Plateau 2 en verder

| Activiteit | Start | Eind |
|---|---|---|
| Voorbereiding en planning | Q1 2026 | Q2 2026 |
| Ontwerp | Q1 2026 | Q4 2026 |
| Realisatie en testen | Q2 2026 | Q2 2028 |
| Implementatie | Q2 2026 | Q4 2028 |
| In beheername | Q2 2027 | Q4 2028 |

---

## Programma Medicatieoverdracht

| Activiteit | Start | Eind |
|---|---|---|
| Kickstart Medicatie Overdracht | Q1 2026 | Q2 2027 |
| Opschaling Medicatie Overdracht | Q3 2027 | Q4 2028 |

---

## Programma Met Spoed Beschikbaar

| Activiteit | Start | Eind |
|---|---|---|
| Uitvoering Met Spoed Beschikbaar | Q1 2026 | Q4 2026 |

---

## Andere nationale ontwikkelingen (Wegiz etc.)

| Activiteit | Start | Eind |
|---|---|---|
| Implementatiewet Tranche 1 | Q1 2026 | Q1 2027 |
| Implementatiewet Tranche 2 | Q2 2026 | Q4 2028 |

---

## LDN / GF

| Activiteit | Start | Eind |
|---|---|---|
| Ontwerp / PvE | Q1 2026 | Q3 2026 |
| Technisch gereed | Q3 2026 | Q1 2027 |
| In praktijk in gebruik | Q1 2027 | Q4 2027 |

---

# Gantt Chart

```mermaid
gantt
    title PIEZO – Programma Implementatie Europese Zorgdiensten
    dateFormat  YYYY-MM-DD
    axisFormat  %Y-Q%q

    section PS-A Plateau 2+
    Voorbereiding en planning     :a1, 2026-01-01, 2026-06-30
    Ontwerp                       :a2, 2026-04-01, 2027-06-30
    Realisatie en testen          :a3, 2026-04-01, 2028-12-31
    Implementatie                 :a4, 2027-01-01, 2028-12-31
    In beheername                 :a5, 2027-01-01, 2028-12-31

    section eP/eD A en B
    Voorbereiding en planning     :b1, 2026-01-01, 2026-12-31
    Ontwerp                       :b2, 2026-04-01, 2027-06-30
    Realisatie en testen          :b3, 2026-07-01, 2028-12-31
    Implementatie                 :b4, 2027-01-01, 2028-12-31
    In beheername                 :b5, 2027-01-01, 2028-12-31

    section Belangrijke mijlpalen
    PrePPT eP/eD                  :milestone, m1, 2027-10-01, 1d
    Freeze fase                   :milestone, m2, 2028-03-01, 1d
    Aanvraag Go-Live eP/eD        :milestone, m3, 2028-09-01, 1d

    section PS-B Plateau 2+
    Voorbereiding en planning     :c1, 2026-01-01, 2026-06-30
    Ontwerp                       :c2, 2026-01-01, 2026-12-31
    Realisatie en testen          :c3, 2026-04-01, 2028-06-30
    Implementatie                 :c4, 2026-04-01, 2028-12-31
    In beheername                 :c5, 2027-04-01, 2028-12-31

    section Medicatieoverdracht
    Kickstart Medicatie Overdracht :d1, 2026-01-01, 2027-06-30
    Opschaling Medicatie Overdracht:d2, 2027-07-01, 2028-12-31

    section Met Spoed Beschikbaar
    Uitvoering                    :e1, 2026-01-01, 2026-12-31

    section Wegiz / Nationale ontwikkelingen
    Implementatiewet Tranche 1    :f1, 2026-01-01, 2027-03-31
    Implementatiewet Tranche 2    :f2, 2026-04-01, 2028-12-31

    section LDN / GF
    Ontwerp / PvE                 :g1, 2026-01-01, 2026-09-30
    Technisch gereed              :g2, 2026-07-01, 2027-03-31
    In praktijk in gebruik        :g3, 2027-01-01, 2027-12-31
```
