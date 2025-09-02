# 🏀 NBA Shot Zone & FG Analysis (2004–2025)

**Author:** Khoi Van

**Tools:** SQL Server (SSMS) + Tableau

---

## 🔍 Overview
This project analyzes **NBA shot locations (2004–2025)** and reports team/player shooting behavior with **Tableau dashboards** backed by **SQL-derived metrics**.

- Dashboards: **Shot Zone Analysis** and **FG Analysis** (eFG%, PPS, rim rate, zone mix).
- SQL: rollups for league/team/player by zone; league benchmarks for “vs league” comparisons.
- **Data source:** season-by-season shot locations from  
  **DomSamangy/NBA_Shots_04_25** → <https://github.com/DomSamangy/NBA_Shots_04_25>  
  (fields include: `SEASON_1, TEAM_NAME, PLAYER_NAME, GAME_DATE, EVENT_TYPE, SHOT_MADE, SHOT_TYPE, BASIC_ZONE, ZONE_NAME, ZONE_RANGE, LOC_X, LOC_Y, SHOT_DISTANCE`, etc.)

> I transform the raw season files into analytics-ready tables (league/team/player fingerprints) and export them as CSVs for Tableau. They can be found in the `Data` folder in this repository.

---

## 🗂 Project & Structure
```
├── data/                                          # curated CSVs exported from SQL views
├── DashboardLink                                  # Link to Tableau Public Dashboard
├── FG Analysis.png                                # dashboard screenshot
├── Khoi Van - Tableau NBA Analysis Project.twbx   # packaged Tableau workbook (2 dashboards)
├── README.md                                      # this file
├── SQLAnalysis.sql                                # SQL view definitions & rollups used for Tableau
├── Shot Frequency Analysis.png                    # dashboard screenshot

```

---

## 🛠 Methodology
1. **Data Preparation (SQL)**
   - Import raw season CSVs (2003–04 → 2024–25) from the source repo into SQL Server.
   - Enrich each shot with derived metrics:
     - `FGA = 1` per row; `FGM` based on `SHOT_MADE/EVENT_TYPE`; `FG3M` when made & `SHOT_TYPE` is 3PT; `Points` = 2 or 3 when made.
   - Aggregate to **League × Season × Zone**, **Team × Season × Zone**, **Player × Season × Zone**.
   - Compute KPIs: **eFG% = (FGM + 0.5*FG3M)/FGA**, **PPS = Points/FGA**, **zone_share** within entity; join **league baselines** for “vs league”.

2. **Dashboard Design (Tableau)**
   - **Shot Zone Analysis**: zone frequency for a selected **Team** and **Player**, side-by-side with **League** for the same season.
   - **FG Analysis**: KPI tiles (Team & Player) and horizontal bars of **FG% / eFG%** by zone; filters for **Season/Team/Player**.

3. **Validation (SQL → Tableau)**
   - Cross-check dashboard numbers against SQL rollups (e.g., league zone shares, team PPS/eFG by zone).
   - Refresh/export CSVs when data update; republish the workbook.

---

## 🔁 Reproducibility

**A) Use the curated CSVs (fastest)**
1. Open the Tableau workbook `Khoi Van - Tableau NBA Analysis Project.twbx`.
2. Ensure the data connections point to the CSVs in `data/`.
3. Interact with filters (Season, Team, Player) and view the two dashboards.

**B) Rebuild from raw source (end-to-end)**
1. Download seasons from **DomSamangy/NBA_Shots_04_25**: <https://github.com/DomSamangy/NBA_Shots_04_25>.  
2. Import the raw CSVs into SQL Server (one table or per-season tables).  
3. Run `SQLAnalysis.sql` to create the views/rollups.  
4. Export the aggregated views to CSV → place in `data/`.  
5. Open the `.twbx` and refresh data sources.

---

## 📈 Result

**General dashboard guidelines**
- Global filters: **Season**, **Team**, **Player**.  
- **Shot Zone Analysis** page: zone frequency breakdown for **Team / League / Player** (same season).  
- **FG Analysis** page: KPI tiles (Team FG%, Rim Rate, eFG%, PPS; Player FG%, PPS, Rim Rate, eFG%) and per-zone bars.

**Screenshots**

**Shot Zone Analysis**  
![Shot Zone Analysis](Shot%20Frequency%20Analysis.png)

**FG Analysis**  
![FG Analysis](FG%20Analysis.png)

