# Source files and acquisition

Keep the paths in `required_inputs.json` relative to the repository root. This manifest records the exact input hashes used for the analysis. The raw files and locally generated data are excluded by `.gitignore`.

| Source | Obtain from | Dimensions and required local location |
|---|---|---|
| IHME GBD2021 | https://gbd2021.healthdata.org/gbd-results/ | National estimates, 1996–2020, prevalence (5), both sexes (3), rate (3), all ages (22) and age-standardized (27). Modeled causes: mental disorders 558, depressive disorders 567 and anxiety disorders 571. The recorded export contains seven causes; the pipeline explicitly selects these three. Save the ZIP as `01_data/IHME-GBD_2021_DATA-a719e539-1.zip`. The audited export has 204 locations and retains `citation.txt`. Access follows IHME registration/access conditions. |
| World Bank WDI | https://data.worldbank.org/ and https://api.worldbank.org/v2/ | `countries_current.json` plus the seven series listed in `required_inputs.json`, 1996–2020. Use `download_public_inputs.py` or stage the recorded JSON responses at `01_data/raw/wdi/`. Current downloads can differ from the recorded vintage. |
| World Bank historical income groups | https://datahelpdesk.worldbank.org/knowledgebase/articles/906519-world-bank-country-and-lending-groups | Save `01_data/raw/wdi/historical_income_classification.xlsx`, sheet `Country Analytical History`. Primary groups use FY22/2020 GNI; historical annual classifications support sensitivity analysis. |
| KOF2025 | https://kof.ethz.ch/en/forecasts-and-indicators/indicators/kof-globalisation-index.html | Save `01_data/raw/kof/KOFGI_2025_public.xlsx`. The download utility uses the official 2025 workbook. |
| PRS ICRG2024 | https://www.prsgroup.com/explore-our-products/icrg/ and https://epub.prsgroup.com/prepared-icrg-datasets | Authorized Table 3B annual component workbook, Table 3Ba subcomponents and country-name dictionary. Place the three legacy XLS files at the exact paths in `required_inputs.json` under `01_data/sj200-ICRG数据库(1984-2023)/`. Five components are A, C, F, I and L. Table 3Ba supports the declared discrepancy-exclusion check. Provider registration and subscription/access conditions apply. |

Use the releases, dimensions, filenames and sheet names specified above. The input checker compares SHA256 hashes before estimation.
