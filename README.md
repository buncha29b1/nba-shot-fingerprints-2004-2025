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

> I transform the raw season files into analytics-ready tables (league/team/player fingerprints) and export them as CSVs for Tableau. They can be found in the Data folder in this repository.
