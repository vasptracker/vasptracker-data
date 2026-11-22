# VASP Tracker Data: Crypto Licensing Deadlines Worldwide

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.23575353.svg)](https://doi.org/10.5281/zenodo.23575353)

Open data behind [VASP Tracker](https://vasptracker.com/): when crypto firms (virtual-asset service providers, VASPs / CASPs) must be licensed, country by country, and which platforms in Brazil appear in the Central Bank's authorisation data.

- **Global map:** https://vasptracker.com/ (78 jurisdictions)
- **Brazil hub (Central Bank, SPSAV):** https://vasptracker.com/pt/br/ · English: https://vasptracker.com/en/br/
- **Data page and data dictionary:** https://vasptracker.com/en/br/data/ · PT: https://vasptracker.com/pt/br/data/
- **Methodology:** https://vasptracker.com/en/br/methodology/
- **Press:** https://vasptracker.com/en/br/press/ · press@vasptracker.com

Snapshot in this repository: version **1.4.0**, built **21 Nov 2026**; Brazil Central Bank (BCB) reference date **31/10/2026**. The live files on vasptracker.com are refreshed on every run and are the canonical version.

## What's Inside

| File | Contents | Rows |
|---|---|---|
| `data/global/jurisdictions.csv` | One row per jurisdiction: region, regulator, regime, status (`upcoming`, `date_pending`, `in_force`), next or last key date, official register URL, sources | 78 |
| `data/global/deadlines.csv` / `.json` | Dated events per jurisdiction (application deadlines, transition ends, entry into force, rules, notices) with source URLs and source type | 209 |
| `data/br/platforms.csv` / `.json` | Platforms serving Brazil: BCB status, legal entities and CNPJ, BCB process numbers, public statements with source and source type | 170 |
| `data/br/spsav_processes.csv` / `.json` | Crypto-related authorisation processes in BCB open data (SPSAV segment + crypto-named processes with no segment stated) | 46 |
| `data/br/series.csv` | Counts per monthly BCB collection, Jan 2024 to Oct 2026 (no data for Aug 2024) | 33 |
| `data/br/changelog.csv` / `.json` | Detected changes between BCB snapshots | 74 |
| `data/br/stats.json`, `data/br/meta.json` | Headline counts and build metadata | — |
| `data/index.html` | Copy of the live open-data page (https://vasptracker.com/data/) at build time; it also lists per-country files that are not part of this repository | — |

All CSVs are UTF-8 and comma-separated; multi-value fields use `;` (Brazil) or ` | ` (global `source_urls`). The full Brazil data dictionary is at https://vasptracker.com/en/br/data/.

### Key Fields (Global)

- `jurisdiction_code`: ISO 3166-1 alpha-2 style code used in site URLs (`uk` for the United Kingdom, `eu` for EU-level rows)
- `status`: `upcoming` (a key date ahead), `date_pending` (regime set, date not set), `in_force` (in force or date passed)
- `event_type`: e.g. `application_deadline`, `transition_end`, `in_force`, `law_adopted`, `rules`, `notice`, `window_opens`
- `our_calculation`: `True` when a date is derived by VASP Tracker from a legal rule (for example "one year after commencement" or "N months from 30 December 2024"); most such rows also say "VASP Tracker calculation" in `description_en`. In this snapshot 9 event rows are calculated.
- `key_date_our_calculation` (jurisdictions.csv): the `our_calculation` flag of that row's key date; blank when there is no key date
- `source_type` / `source_types`: `official`, `company` or `press`
- `page_url`: the jurisdiction page on vasptracker.com

## Sources and Method

Official sources come first: laws, official gazettes, regulator notices and registers (including the ESMA interim MiCA register). Company statements come second. Press is used only as labelled secondary support and never as the only source for a date. Every row carries its source URL and source type.

For EU/EEA MiCA Art. 143(3) transitional periods, the length in months comes from ESMA's [list of grandfathering periods decided by Member States](https://www.esma.europa.eu/sites/default/files/2024-12/List_of_MiCA_grandfathering_periods_art._143_3.pdf), but each `transition_end` date is taken from national law or the national authority, and the first source URL of the row is that national source (its wording is quoted in `description_en`). Where no national text gives the day (for example a period described only as "up to 18 months", where the date is the 1 July 2026 cap in Art. 143(3)), `our_calculation` is `True`. Where the national law text could only be read in an unofficial consolidation (Greece, Hungary), that source is typed `press` and the row says so. `data/eu/member_states.csv` on the live site adds `end_our_calculation`, `end_source` and `end_note` per state.

Brazil data comes from Banco Central do Brasil open data ([authorisation processes](https://dadosabertos.bcb.gov.br/dataset/processos-de-autorizacao)) and BCB's lists of institutions in operation, matched by CNPJ root. Absence from the BCB dataset does not imply wrongdoing; see the [methodology](https://vasptracker.com/en/br/methodology/).

This is not legal or financial advice. VASP Tracker is an independent project and is not affiliated with Banco Central do Brasil, ESMA or any regulator.

## Changelog

### 1.4.0 (2026-11-22)

Changes since the previous published snapshot (1.3.0):

- Jurisdictions: 78 → 78.
- Dated events: 209 → 209 (0 added, 0 removed or re-dated). Added by jurisdiction: .
- Rows with `our_calculation` = True: 9 → 9.
- Brazil platforms: 170 → 170; `bcb_status` art22 5, denied 1, in_process 67, not_in_data 97 → art22 5, denied 1, in_process 67, not_in_data 97.
- BCB reference date 31/10/2026 → 31/10/2026; SPSAV processes 46 → 46; BCB change-log rows 74 → 74.

### 1.3.0 (2026-11-20)

Changes since the previous published snapshot (1.2.0):

- Jurisdictions: 78 → 78.
- Dated events: 209 → 209 (0 added, 0 removed or re-dated). Added by jurisdiction: .
- Rows with `our_calculation` = True: 9 → 9.
- Brazil platforms: 170 → 170; `bcb_status` art22 5, denied 1, in_process 67, not_in_data 97 → art22 5, denied 1, in_process 67, not_in_data 97.
- BCB reference date 31/10/2026 → 31/10/2026; SPSAV processes 46 → 46; BCB change-log rows 73 → 74.

### 1.2.0 (2026-11-18)

Changes since the previous published snapshot (1.1.0):

- EU/EEA MiCA Art. 143(3) transition_end dates now follow national law or the national authority, with the national source as the first `source_urls` entry and its wording quoted in `description_en`: Germany, Austria, Lithuania 2025-12-30 → 2025-12-31 (KMAG § 50(2) no. 3; § 23 MiCA-VVG; Bank of Lithuania); Belgium, Italy, Malta, Greece 2026-07-01 → 2026-06-30 (FSMA; art. 45 D.Lgs. 129/2024 as amended by DL 95/2025; MFSA / VFA Act art. 66; Law 5193/2025 art. 125 as amended by Law 5259/2025 art. 204); Slovenia 2025-06-30 → 2025-07-01 (ZIUTK art. 21, PISRS).
- Sweden keeps 2025-09-30, now cited to Act 2024:1159 transitional provision 4 and described as the statutory date for firms that had not applied (applicants could continue until decided; FI says that ran out at the end of June 2026). Poland keeps 2026-07-01, now cited to IAS Katowice (gov.pl) and explained (the 6 months notified to ESMA were never written into law). Portugal keeps 2026-07-01, now cited to Law 69/2025 art. 30(1). Norway keeps 2026-06-30 (Finanstilsynet extension) and notes that ESMA's list still shows 12 months.
- `our_calculation` corrected for transition_end rows: now False where national law or the regulator states the day (DE, AT, IE, LT, SK, SE, FI, LV, NL, SI); True for Denmark (no national day; 1 July 2026 Art. 143(3) cap) and Hungary (statute gives 1 July 2025 as the compliance date; last day derived). United Arab Emirates row now says "VASP Tracker calculation" to match its flag.
- New column `key_date_our_calculation` at the end of `data/global/jurisdictions.csv` (and in `deadlines.json` jurisdictions): the calculation flag of each jurisdiction's key date.
- Jurisdictions: 78 → 78.
- Jurisdiction status / key-date changes: Belgium: key date 2026-07-01 → 2026-06-30; Greece: key date 2026-07-01 → 2026-06-30; Italy: key date 2026-07-01 → 2026-06-30; Malta: key date 2026-07-01 → 2026-06-30; Germany: key date 2025-12-30 → 2025-12-31; Austria: key date 2025-12-30 → 2025-12-31; Lithuania: key date 2025-12-30 → 2025-12-31; Slovenia: key date 2025-06-30 → 2025-07-01.
- Dated events: 209 → 209 (8 added, 8 removed or re-dated). Added by jurisdiction: `be` 1, `gr` 1, `it` 1, `mt` 1, `de` 1, `at` 1, `lt` 1, `si` 1.
- Removed or re-dated events: `at` 2025-12-30 transition_end; `be` 2026-07-01 transition_end; `de` 2025-12-30 transition_end; `gr` 2026-07-01 transition_end; `it` 2026-07-01 transition_end; `lt` 2025-12-30 transition_end; `mt` 2026-07-01 transition_end; `si` 2025-06-30 transition_end.
- Rows with `our_calculation` = True: 18 → 9.
- Brazil platforms: 170 → 170; `bcb_status` art22 5, denied 1, in_process 67, not_in_data 97 → art22 5, denied 1, in_process 67, not_in_data 97.
- BCB reference date 31/10/2026 → 31/10/2026; SPSAV processes 46 → 46; BCB change-log rows 73 → 73.

### 1.1.0 (2026-11-18)

Changes since the previous published snapshot (2026-10-21):

- Jurisdictions: 74 → 78; added Barbados (`bb`), Jamaica (`jm`), Kyrgyzstan (`kg`), Philippines (`ph`).
- Jurisdiction status / key-date changes: Brazil: status upcoming → in_force; key date 2026-10-30 → 2026-11-06; Kenya: status upcoming → in_force; Australia: key date 2027-04-09 → 2027-04-08; Russia: key date 2027-07-01 → 2026-11-22; Argentina: key date 2025-12-31 → 2025-04-28; Nigeria: key date 2025-03-25 → 2026-11-05; South Korea: status in_force → upcoming; key date 2024-07-19 → 2026-11-30; Bermuda: key date 2018-09-17 → 2018-09-10; Thailand: status in_force → upcoming; key date 2018-05-14 → 2026-12-05.
- Dated events: 163 → 209 (48 added, 2 removed or re-dated). Added by jurisdiction: `ru` 8, `kr` 4, `pl` 4, `ph` 4, `bb` 3, `au` 3, `jm` 3, `th` 2, `ke` 2, `eu` 2, `kg` 2, `ar` 2, `bh` 2, `us` 1, `tw` 1, `tr` 1, `br` 1, `ng` 1, `gr` 1, `bm` 1.
- Removed or re-dated events: `ar` 2025-12-31 in_force; `au` 2027-04-09 in_force.
- Rows with `our_calculation` = True: 16 → 18.
- Brazil platforms: 170 → 170; `bcb_status` denied 1, in_process 7, not_in_data 162 → art22 5, denied 1, in_process 67, not_in_data 97. `art22` is a new status: institutions already authorised on BCB's art. 22 list (not counted as SPSAV).
- BCB reference date 30/09/2026 → 31/10/2026; SPSAV processes 8 → 46; BCB change-log rows 8 → 73.

### 2026-10-21

First public snapshot (built 21 Oct 2026; BCB reference date 30/09/2026).

## Licence

[CC BY 4.0](LICENSE). Credit "VASP Tracker (vasptracker.com)" with a link to https://vasptracker.com/.

## Citation

> VASP Tracker (2026). *Crypto licensing deadlines worldwide and Brazil SPSAV tracker* (Version 1.4.0) [Data set]. Zenodo. https://doi.org/10.5281/zenodo.23575353

See `CITATION.cff`. The DOI [10.5281/zenodo.23575353](https://doi.org/10.5281/zenodo.23575353) always resolves to the newest archived version.

## Corrections

Found an error? Open an issue with the source URL, or email press@vasptracker.com.
