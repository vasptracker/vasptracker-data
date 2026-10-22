# VASP Tracker Data: Crypto Licensing Deadlines Worldwide

Open data behind [VASP Tracker](https://vasptracker.com/): when crypto firms (virtual-asset service providers, VASPs / CASPs) must be licensed, country by country, and which platforms in Brazil appear in the Central Bank's authorisation data.

- **Global map:** https://vasptracker.com/ (74 jurisdictions)
- **Brazil hub (Central Bank, SPSAV):** https://vasptracker.com/pt/br/ · English: https://vasptracker.com/en/br/
- **Data page and data dictionary:** https://vasptracker.com/en/br/data/ · PT: https://vasptracker.com/pt/br/data/
- **Methodology:** https://vasptracker.com/en/br/methodology/
- **Press:** https://vasptracker.com/en/br/press/ · press@vasptracker.com

Snapshot in this repository: built **21 Oct 2026**; Brazil Central Bank (BCB) reference date **30/09/2026**. The live files on vasptracker.com are refreshed on every run and are the canonical version.

## What's Inside

| File | Contents | Rows |
|---|---|---|
| `data/global/jurisdictions.csv` | One row per jurisdiction: region, regulator, regime, status (`upcoming`, `date_pending`, `in_force`), next or last key date, official register URL, sources | 74 |
| `data/global/deadlines.csv` / `.json` | Dated events per jurisdiction (application deadlines, transition ends, entry into force, rules, notices) with source URLs and source type | 163 |
| `data/br/platforms.csv` / `.json` | Platforms serving Brazil: BCB status, legal entities and CNPJ, BCB process numbers, public statements with source and source type | 170 |
| `data/br/spsav_processes.csv` / `.json` | Crypto-related authorisation processes in BCB open data (SPSAV segment + crypto-named processes with no segment stated) | 8 |
| `data/br/series.csv` | Counts per monthly BCB collection, Jan 2024 to Sep 2026 (no data for Aug 2024) | 33 |
| `data/br/changelog.csv` / `.json` | Detected changes between BCB snapshots | 8 |
| `data/br/stats.json`, `data/br/meta.json` | Headline counts and build metadata | — |

All CSVs are UTF-8 and comma-separated; multi-value fields use `;` (Brazil) or ` | ` (global `source_urls`). The full Brazil data dictionary is at https://vasptracker.com/en/br/data/.

### Key Fields (Global)

- `jurisdiction_code`: ISO 3166-1 alpha-2 style code used in site URLs (`uk` for the United Kingdom, `eu` for EU-level rows)
- `status`: `upcoming` (a key date ahead), `date_pending` (regime set, date not set), `in_force` (in force or date passed)
- `event_type`: e.g. `application_deadline`, `transition_end`, `in_force`, `law_adopted`, `rules`, `notice`, `window_opens`
- `our_calculation`: `True` when a date is derived by VASP Tracker from a legal rule (for example "one year after commencement")
- `source_type` / `source_types`: `official`, `company` or `press`
- `page_url`: the jurisdiction page on vasptracker.com

## Sources and Method

Official sources come first: laws, official gazettes, regulator notices and registers (including the ESMA interim MiCA register). Company statements come second. Press is used only as labelled secondary support and never as the only source for a date. Every row carries its source URL and source type.

Brazil data comes from Banco Central do Brasil open data ([authorisation processes](https://dadosabertos.bcb.gov.br/dataset/processos-de-autorizacao)) and BCB's lists of institutions in operation, matched by CNPJ root. Absence from the BCB dataset does not imply wrongdoing; see the [methodology](https://vasptracker.com/en/br/methodology/).

This is not legal or financial advice. VASP Tracker is an independent project and is not affiliated with Banco Central do Brasil, ESMA or any regulator.

## Licence

[CC BY 4.0](LICENSE). Credit "VASP Tracker (vasptracker.com)" with a link to https://vasptracker.com/.

## Citation

> VASP Tracker (2026). *Crypto licensing deadlines worldwide and Brazil SPSAV tracker* [Data set]. https://vasptracker.com/

See `CITATION.cff`. A DOI will be added here once the dataset is deposited on Zenodo.

## Corrections

Found an error? Open an issue with the source URL, or email press@vasptracker.com.
