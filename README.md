Readme · MD
# Sydney-sa2-analysis

Analysis of Greater Sydney SA2 regions using ABS NSW statistics and Points of Interest data, including data cleaning, POI extraction, and a well-resourced scoring model built with Python and PostgreSQL.
 
---
 
## Project Overview
 
The goal is to assess how "well-resourced" Statistical Area Level 2 (SA2) regions across Greater Sydney are, using publicly available ABS statistical data and the NSW Points of Interest (POI) API.
 
---
 
## Repository Structure
 
```
data2x01-sydney-sa2-analysis/
│
├── nsw_regional_data_cleaning_and_statistics.ipynb       # Task 1
├── sydney_city_inner_south_poi_extraction_and_scoring.ipynb  # Task 2 & 3
├── scores_vanessa.csv                                    # Computed SA2 scores
├── Region_summary_NSW.csv                                # Source ABS data (not included)
└── README.md
```
 
---
 
## Tasks
 
### Task 1 — NSW Regional Data Cleaning & Statistics
**Notebook:** `nsw_regional_data_cleaning_and_statistics.ipynb`
 
- Loads ABS NSW regional summary data (`Region_summary_NSW.csv`) using Pandas
- Performs data cleaning: drops sparse columns, melts wide-to-long format, standardises column names, removes duplicates, filters metrics with fewer than 3 years of data, and extracts units from metric names
- Derives 5 original statistics including a **Migration Dependency Index (MDI)**
### Task 2 — POI Extraction for Sydney - City and Inner South
**Notebook:** `sydney_city_inner_south_poi_extraction_and_scoring.ipynb`
 
- Loads SA2 and SA4 shapefiles and verifies all SA2s lie within the City and Inner South SA4 boundary
- Implements a paginated bounding-box query function against the **NSW POI API** to retrieve all Points of Interest per SA2 (handles the 1000-record API limit)
- Loops across all SA2s in the zone and stores results in a structured GeoDataFrame
- Ingests the final POI dataset into a **PostgreSQL** database with a well-defined schema
### Task 3 — Well-Resourced Scoring
**Notebook:** `sydney_city_inner_south_poi_extraction_and_scoring.ipynb`
 
- Computes a normalised POI-based score for each SA2 using a sigmoid function applied to the z-score of POI count
- SA2 regions with fewer than 100 residents are excluded
---
 
## Data Sources
 
| Source | Description |
|--------|-------------|
| [ABS Region Summary](https://dbr.abs.gov.au/region.html?lyr=ste&rgn=1) | NSW regional statistics |
| [ABS ASGS Shapefiles](https://www.abs.gov.au/statistics/standards/australian-statistical-geography-standard-asgs-edition-3/jul2021-jun2026) | SA2 and SA4 boundary polygons |
 
---
 



