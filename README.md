# Unemployment and mental health country panel

Reproducibility materials for the revised country-level study, 1996–2020.
Repository: https://github.com/keyan-shu/unemployment-mental-health-panel

The original analytical files were unavailable. These scripts implement the explicitly reconstructed analysis in the revised manuscript; they do not recover the original manuscript's numerical tables.

## Download and extract the code

The complete source tree, specifications, expected results and validation scripts are provided in **[reproduction_bundle.zip](reproduction_bundle.zip)**. Download this archive or clone the repository, then extract it into a new directory before running the commands below:

```sh
python -m zipfile -e reproduction_bundle.zip analysis
cd analysis
```

The archive preserves the original directory structure. Source data must be obtained separately; no provider credentials or restricted raw data are included. `REPRODUCTION_CHECK.json` records the successful isolated rebuild and comparisons performed before publication.

## Reproduce the revised results

Use Python 3.14. Install the recorded dependencies, obtain the source files described in [DATA_SOURCES.md](DATA_SOURCES.md), then run:

```sh
python -m pip install -r requirements.txt
python run_analysis.py --check-inputs
python run_analysis.py
```

The input check requires all 14 recorded files and their SHA256 hashes. It stops before estimation when inputs are missing or differ. Newly downloaded WDI releases can have revised values; a current release is not guaranteed to reproduce the recorded estimates. Source data are obtained separately from their providers. The repository does not include GBD source estimates, ICRG ratings or numerical instrument matrices.

`download_public_inputs.py` downloads the required WDI series and KOF2025 workbook and preserves existing files. The historical World Bank income workbook must be obtained separately. The older `02_code/02_download_public_sources.py` is retained as a historical acquisition utility; it also downloads exploratory sources not used in the final analysis and is not part of the reproduction command.

## What the pipeline reproduces

- Cleaning, country mapping, sample selection and five-component PCA with fixed orientation and scale.
- All 12 primary country/year fixed-effects models (72 slopes), country-clustered CR1 standard errors, confidence intervals and BH corrections.
- Formal income-group joint and pairwise contrasts.
- All nine declared exploratory GMM variants, including rejected diagnostics, lag rules, instrument counts, Hansen and AR tests. Instrument matrices are regenerated locally from source data.
- All-age outcomes, pre-2020 analysis, ICRG discrepancy exclusions, same-sample omission of INST, time-varying income groups, additional controls with matched baselines, and Driscoll–Kraay inference.
- Descriptive statistics, coverage and missingness used by the revised tables and appendices.

Primary sample: 2,065 country-years from 131 countries. Dynamic models: 125 countries, 1,570 difference-equation observations; System GMM additionally contains 1,780 level-equation observations. Unfavorable or nonsignificant results remain included.

## Files and verification

`02_code/` contains the analysis scripts, specifications and vendored pydynpd. `required_inputs.json` identifies essential inputs; `input_manifest.json` also lists archived acquisition files that are not all needed to run the pipeline. `derived_results/` contains audited expected outputs. `inclusion_keys/` contains country/year keys without source values. `instrument_metadata/` records commands and instrument rules. [TABLE_MAP.md](TABLE_MAP.md) connects the manuscript tables to outputs.

After rebuilding, `validation/verify_outputs.py` compares 18 expected tables and 27 sample-key files with regenerated outputs. It uses numerical tolerances and exact country/year membership. `validation/reproduction_report.json` records the result locally. `python run_analysis.py --verify-only` repeats this comparison without refitting. The independent NumPy GMM and FWL sensitivity implementations under `validation/independent/` are optional audit checks after the main run; they are not prerequisites for generating manuscript results.

Figure 1 is retained historical context from the cited IHME/Our World in Data source. It is not generated from the age-standardized outcome panel and is not presented as a regenerated analytical figure. Manuscript/reply DOCX files and internal correspondence are excluded.

## License

The author's existing MIT LICENSE applies to original repository code. Vendored pydynpd retains its own license at `02_code/vendor/pydynpd/LICENSE`; see `VENDOR_NOTES.md`. Provider terms govern third-party source data; the code license does not relicense those data.
