# Measuring Food Insecurity in the Capital Area 

<img width="1610" height="688" alt="Screenshot 2025-10-22 132625" src="https://github.com/user-attachments/assets/0ef1426e-bf2c-4d91-9e3d-926e32ca9773" />
An Excel-based interactive dashboard to analyze **food need, distribution, coverage, and unmet pounds** for **DC, Maryland, and Virginia** (2014–2015). Includes state rollups, a Top-15 tracts view, KPI cards, a slicer, and a filled map.

---

## Data Source
- **Dataset:** Capital Area Food Bank–style hunger estimates (tract level, 2014–2015)  
- **Provided by:** **Downtown Evening Soup Kitchen (DESK), New Haven, CT**  
- **Geography:** DC, Maryland, Virginia  
> Note: The 2014 “Pounds Needed” field is **reconstructed** as `Distributed + Unmet` (not present in source).

---

## What’s Inside
- `CAFB_Dashboard.xlsx` – main Excel workbook  
- `Cover_Statement_DESK.docx` – one-page cover statement  
- `images/dashboard.png` – dashboard screenshot  
- `README.md` – this file

---

## Workbook Layout

### Sheets
- **Data** – imported tract-level data as an Excel Table named `Data`.
- **Calcs** – helper table `CalcsTbl` with computed fields:
  - `FI Rate (2014)`, `Pounds Distributed (2014)`, `Unmet Pounds (2014)`
  - `Pounds Needed (2014) = Distributed + Unmet`
  - `Coverage % (2014) = Distributed / Needed`
  - `FI Rate (2015)`, `FI People (2015)`, `Pounds Needed (2015)`, `Pounds Distributed (2015)`, `Unmet Pounds (2015)`
  - `Coverage % (2015) = Distributed / Needed`
  - `Unmet per Person (2015) = Unmet / FI People`
  - `State (Label)` via FIPS map (11→DC, 24→MD, 51→VA)
  - `State Clean` (UPPER/TRIM of `State (Label)`) for mapping
- **Pivots** – two PivotTables:
  - **`Pvt_State`** (Rows: State (Label); Values renamed for clarity)
    - `LB Needed 2015` (Sum)  
    - `LB Distributed 2015` (Sum)  
    - `LB Unmet 2015` (Sum)  
    - `FI People 2015` (Sum)  
    - `FI Rate 2015 (Avg)` (Average, %)  
    - `Coverage 2014 (Avg)` (Average, %)  
    - `Coverage 2015 (Avg)` (Average, %)
  - **`Pvt_TopTracts`** (Rows: Tract_ID; Values: `LB Unmet 2015` → Sort Desc → Filter **Top 15**)
- **Dashboard** – final visuals:
  1) **LB Needed vs LB Distributed — 2015 (by State)** (clustered column)  
  2) **Top 15 Tracts — LB Unmet (2015)** (clustered bar)  
  3) **Coverage by State — 2014 vs 2015** (clustered column)  
  4) **Coverage % (2015) by State** (filled map from a 3-row summary: DC/MD/VA)

**Slicer:** State (Label) connected to both pivots.  
**KPIs:** Avg FI Rate (2015), Total FI People (2015), Avg Coverage (2015), Total LB Unmet (2015).

---

## Quick Start
1. Open `CAFB_Dashboard.xlsx`.  
2. On **Dashboard**, use the **State** slicer (DC/MD/VA).  
3. Read the KPI cards, then review the four charts for gaps, trends, and hotspots.  
4. (Optional) Replace `images/dashboard.png` with a fresh screenshot.

---

## Methods (Light)
- Coverage is a service ratio: `Distributed / Needed`.  
- 2014 “Needed” is reconstructed: `Distributed + Unmet`.  
- State rollups use PivotTable **Sums** (pounds/people) and **Averages** (rates/coverage).  
- The map uses a tiny summary:
  - `District of Columbia = AVERAGEIFS(CalcsTbl[Coverage % (2015)], CalcsTbl[State Clean], "DC")`
  - `Maryland = AVERAGEIFS(..., "MD")`
  - `Virginia = AVERAGEIFS(..., "VA")`

---

## Credits
- **Data provided by:** Downtown Evening Soup Kitchen (DESK), New Haven, CT  
- **Tools:** Microsoft Excel (Tables, PivotTables, Slicers, Charts, Filled Map)
