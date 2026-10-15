# Unemployment and mental health country panel

Analysis code for **Unemployment and mental health across national income groups: a longitudinal country-level study, 1996–2020**.

The project examines associations between national unemployment and mental disorder prevalence using country and year fixed-effects models, income-group comparisons, dynamic panel models and sensitivity analyses.

## Download

Download [reproduction_bundle.zip](reproduction_bundle.zip) or clone this repository, then extract the analysis files:

```sh
python -m zipfile -e reproduction_bundle.zip analysis
cd analysis
```

## Data

Obtain the source data from the IHME GBD Results Tool, World Bank World Development Indicators, KOF Globalisation Index and PRS International Country Risk Guide. [DATA_SOURCES.md](DATA_SOURCES.md) lists the official websites, data releases, dimensions and local file paths. `required_inputs.json` records the 14 input files and their checksums. Access follows the respective providers' registration and access conditions.

`download_public_inputs.py` downloads the WDI series and KOF2025 workbook. Obtain the GBD export, ICRG workbooks and World Bank historical income classification workbook from their corresponding websites.

## Run

Use Python 3.14 and install the dependencies:

```sh
python -m pip install -r requirements.txt
python run_analysis.py --check-inputs
python run_analysis.py
```

The input check compares the supplied files with the recorded checksums. Use the documented data releases and matching input files to reproduce the reference results.

## Analyses

- Data cleaning, country mapping, sample selection and a five-component institutional PCA.
- Twelve country and year fixed-effects models, country-clustered standard errors, confidence intervals and Benjamini–Hochberg corrections.
- Joint and pairwise comparisons across national income groups.
- Nine dynamic panel models with specified instrument sets, Hansen tests and AR diagnostics.
- Sensitivity analyses for outcome age definition, study period, institutional indicators, income classification, additional controls and Driscoll–Kraay standard errors.
- Descriptive statistics, country coverage, missingness and model fit summaries.

The primary sample comprises 2,065 country-year observations from 131 countries. Dynamic models use 125 countries and 1,570 difference-equation observations; System GMM also uses 1,780 level-equation observations.

## Files and validation

| Location | Contents |
|---|---|
| `02_code/` | Analysis scripts, model specifications and pydynpd source |
| `required_inputs.json` | Input filenames, sizes and SHA256 checksums |
| `derived_results/` | Reference model outputs and summary statistics |
| `inclusion_keys/` | Country-year sample indices |
| `instrument_metadata/` | Dynamic-model commands and instrument definitions |
| `validation/` | Output comparisons and independent implementation checks |
| `TABLE_MAP.md` | Article tables and their analytical output files |

After the analysis, the verification script compares 18 reference tables and 27 sample-index files with the generated outputs. Run `python run_analysis.py --verify-only` to repeat this check. `REPRODUCTION_CHECK.json` records the validation results. Figure 1 uses the historical IHME/Our World in Data series cited in the article.

## License

Project code is provided under the MIT license. pydynpd has its own license at `02_code/vendor/pydynpd/LICENSE`. See `VENDOR_NOTES.md` for compatibility details. Source data follow their providers' terms.
