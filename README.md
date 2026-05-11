# Detaljhandel — Budget vs Försäljning 2024

Interaktiv Power BI-dashboard för analys av försäljningsdata 
mot budget för en detaljhandelskedja med fyra butiker.

## Syfte

Visa hur rådata från ekonomiavdelningen — ofta rörig och 
pivoterad — kan transformeras och analyseras i Power BI 
med fokus på budget vs utfall per butik, region och kategori.

## Fokus: Data som utgångspunkt

Det mest tidskrävande steget i verklig analytisk leverans 
är sällan visualiseringen — det är att forma rådata till 
något analysvänligt. Det är vad detta projekt fokuserar på.

Råfilen från ekonomiavdelningen innehöll samtliga vanliga 
problem som analytiker möter i praktiken: skräprader, 
pivoterad struktur, inkonsistenta nyckelord och fragmenterad 
information spridd över flera tabeller. Ingen rad data 
laddades in i Power BI utan att först ha hanterats i 
Power Query.

Det är skillnaden mellan en dashboard som ser bra ut 
och en dashboard som faktiskt stämmer.

## Funktioner

- KPI-kort: Total försäljning, total budget, variance (SEK och %)
- Budget vs faktisk försäljningstrend per månad (combo chart)
- Försäljning per kategori (Elektronik, Kläder, Hem & Kök)
- Försäljning per region (Svealand, Sydsverige, Västsverige)
- Variance-tabell per butik med sortering
- Slicers för region, kategori och butiksnamn

## Databearbetning i Power Query

Rådata innehöll flera vanliga verklighetsproblem som 
löstes i Power Query innan analys:

- Skräprader och tomma rader i toppen av filen
- Månader som kolumner (pivoterad struktur) — unpivoterades
  till ett analysvänligt radformat
- Inkonsistenta butiksnamn (versaler, gemener, mellanslag)
- Butiksinformation i separat tabell — kopplades via Merge Queries
- Egen M-kod skriven manuellt för kolumntransformationer

## Datamodell

Star-schema med fyra tabeller:

- Försäljning_2024 — faktatabell (144 rader efter unpivot)
- Budget_2024 — budgetdata (144 rader efter unpivot)
- Butiksinformation — dimensionstabell (4 butiker)
- Calendar — dimensionstabell (12 unika månader)

Relationer: alla många-till-en, alla aktiva.

## DAX-measures

```dax
Total Försäljning = SUM('Försäljning_2024'[Försäljning])
Total Budget = SUM(Budget_2024[Budget])
Variance = [Total Försäljning] - [Total Budget]
Variance % = DIVIDE([Variance], [Total Budget], 0)
```

## Nyckeltal

- Total försäljning: 37.54M kr
- Total budget: 36.17M kr
- Variance: +1.36M kr (+3.77%)
- Starkaste region: Svealand
- Starkaste kategori: Hem & Kök

## Teknologi

- Power BI Desktop
- Power Query (M-språk)
- DAX
- Star-schema datamodellering

## Filer

- `Detaljhandel_PowerQuery.pbix` — Power BI-fil
- `Detaljhandel_RAW.xlsx` — rådata före transformation
- `dashboard_overview.png` — screenshot

## Portfolio

Detta är Mini-projekt 1 i en serie fokuserade Power BI-projekt för att skapa bättre förståelse för Power BI:

- Mini-projekt 1: Power Query & M-språk (detta projekt)
- Mini-projekt 2: Row-level Security (RLS)
- Mini-projekt 3: Drillthrough & Bookmarks
- Mini-projekt 4: SQL-koppling till Power BI
