# Datasheet for the NRCD Anonymized Dataset

This document follows the framework proposed in [Datasheets for Datasets](https://doi.org/10.1145/3458723) (Gebru et al., 2021). For file structure, field definitions, and usage instructions, see [`README.md`](README.md).

## At a Glance

| | |
|---|---|
| **Version** | v2.0.0 |
| **Last updated** | June 5, 2026 |
| **Data coverage** | 2004 – May 2026 |
| **Zenodo** | [zenodo.org/records/17917357](https://zenodo.org/records/17917357) |
| **License** | [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) |
| **Format** | UTF-8 CSV (9 relational tables + 1 denormalized export) |
| **Update cadence** | Yearly public exports as new meets are approved |
| **Related paper** | Karr et al., *NRCD: An Open Database of Collegiate Running with Unified Performance Standardization* — under review; arXiv preprint forthcoming |

**Scope of this release:** All approved results from **2004 through May 2026** across Cross Country, Indoor Track, Outdoor Track, and Road Race. The export includes both **comprehensive** data (meet date ≥ August 2023, richer metadata) and **historical** data (2004–July 2023, sparser metadata). Prior Zenodo releases (v1.0.0, v1.1.0) contained cross country only.

---

## Motivation

### For what purpose was the dataset created?

The National Running Club Database (NRCD) was created to provide a centralized, research-ready record of collegiate club running results in the United States. Existing platforms (Athletic.net, MileSplit, TFRRS) host results but do not support bulk relational export, limiting prior research to small hand-curated samples.

This anonymized release removes personal identifying information (PII) so that researchers can study collegiate running performance, team participation, course and weather conditions, and meet metadata at scale without exposing individual identities.

### Who created the dataset and on whose behalf?

| Role | Name | ORCID |
|------|------|-------|
| Data manager | Jonathan A. Karr Jr. | [0009-0000-1600-6122](https://orcid.org/0009-0000-1600-6122) |
| Data collector | Ben Darden | [0009-0008-3808-1375](https://orcid.org/0009-0008-3808-1375) |
| Data collector | Nicholas Pell | [0009-0001-1289-5054](https://orcid.org/0009-0001-1289-5054) |
| Data collector | Ryan M. Fryer | [0009-0008-3591-3877](https://orcid.org/0009-0008-3591-3877) |

Additional authors on the accompanying manuscript: Kayla Ambrose, Evan Hall, Ramzi K. Bualuan, and Nitesh V. Chawla.

The dataset is maintained on behalf of the [National Running Club Database](https://www.nationalrunningclubdatabase.com/).

### Who funded the creation of the dataset?

Community-contributed and maintained by NRCD volunteers and domain experts. No external grant funding is associated with this release.

### Any other comments?

This release is **v2.0.0** on the [official NRCD Zenodo record](https://zenodo.org/records/17917357). It expands prior cross-country-only releases (v1.0.0, v1.1.0) to all approved sports and seasons, spanning both comprehensive and historical eras (2004–May 2026). PII removal and public release were reviewed under University of Notre Dame IRB protocols (see Ethical Review).

---

## Composition

### What do the instances that comprise the dataset represent?

| File | Instance type |
|------|---------------|
| `result.csv` | An individual race result (or relay leg) at a meet |
| `meet.csv` | A meet or multi-day competition |
| `athlete.csv` | A unique athlete (anonymized) |
| `team.csv` | A collegiate running club or team |
| `athlete_team_association.csv` | An athlete's affiliation with a team |
| `course_details.csv` | Course and weather metadata for a meet/event combination |
| `running_event.csv` | A running event definition (e.g., 5K, 800m) |
| `sport.csv` | A sport category |
| `joined.csv` | Denormalized view combining result, athlete, meet, team, and course fields |

### How many instances are there in total?

**Table counts (v2.0.0):**

| File | Records |
|------|---------|
| `result.csv` | 128,963 |
| `meet.csv` | 1,336 |
| `athlete.csv` | 29,609 |
| `team.csv` | 187 |
| `athlete_team_association.csv` | 29,618 |
| `course_details.csv` | 939 |
| `running_event.csv` | 54 |
| `sport.csv` | 4 |
| `joined.csv` | 155,109 |

**Results by sport:**

| Sport | Results | Meets (approx.) |
|-------|---------|-----------------|
| Cross Country | 70,285 | — |
| Indoor Track | 22,809 | — |
| Outdoor Track | 33,689 | — |
| Road Race | 2,180 | — |
| **Total** | **128,963** | **1,336** |

**Results by gender:**

| Gender | Results | Share |
|--------|---------|-------|
| Women (F) | 46,757 | 36.3% |
| Men (M) | 82,206 | 63.7% |

**Coverage era (comprehensive and historical):**

Following the accompanying paper, results are split by meet date:

| Era | Date range | Description |
|-----|------------|-------------|
| **Historical** | 2004 – July 2023 | Approved results with partial metadata; sparser course, weather, and altitude fields |
| **Comprehensive** | August 2023 – May 2026 | Approved results with full metadata where available (course distance, elevation gain/loss, venue altitude, weather via OpenWeatherMap) |

Both eras are included in this release. Researchers should account for metadata availability when analyzing pre-2023 data.

**Results by sport and era:**

| Sport | Era | Results | Weather coverage* |
|-------|-----|---------|-------------------|
| Cross Country | Historical | 46,930 | 4.4% |
| Cross Country | Comprehensive | 23,355 | 97.7% |
| Indoor Track | Historical | 4,171 | 0.0% |
| Indoor Track | Comprehensive | 18,638 | 0.0% |
| Outdoor Track | Historical | 12,321 | 0.0% |
| Outdoor Track | Comprehensive | 21,368 | 36.9% |
| Road Race | Historical | 1,332 | 34.5% |
| Road Race | Comprehensive | 848 | 67.0% |
| **Total** | **Historical** | **64,754** | — |
| **Total** | **Comprehensive** | **64,209** | — |

\*Share of results in that sport/era with a non-null `weather_conditions` field in `course_details.csv`.

### Does the dataset contain all possible instances or is it a sample?

No — this is not a random sample. It includes **all approved** meets and results in the NRCD database at export time, with lookup tables trimmed to referenced entities only. Coverage reflects NIRCA-centric voluntary club competition; it is not a census of all U.S. collegiate running (NCAA, NAIA, etc. are largely outside scope).

### What data does each instance consist of?

Rows in UTF-8 CSV files. Key fields per table are listed in [`README.md`](README.md). Removed fields include names, user IDs, social links, media URLs, and relay teammate names (in `joined.csv`).

### Is there a label or target associated with each instance?

No single label. Common derived targets: `result_time`, placement (computed), team, sport, season, course distance, elevation, and weather variables.

### Are relationships between individual instances made explicit?

Yes. Foreign keys link tables: `athlete_id`, `team_id`, `meet_id`, `running_event_id`, `sport_id`. See the relationship diagram in [`README.md`](README.md).

### Are there recommended data splits?

No official splits. For longitudinal work, define splits by school year (August 1–July 31), meet date, or sport. Account for athletes appearing across multiple meets, seasons, and sports. **We recommend gender-stratified analysis** — do not pool raw or adjusted times across men's and women's events.

### Are there any errors, sources of noise, or redundancies?

| Issue | Detail |
|-------|--------|
| Historical sparsity | Pre-August 2023 rows often lack course/weather metadata |
| Entry errors | Results entered by contributors and reviewed by admins; transcription errors possible |
| Multi-team athletes | 9 athletes appear on multiple teams |
| Multi-sport athletes | Athletes may compete in more than one sport |
| Redundancy | `joined.csv` duplicates normalized tables for convenience |
| Weather gaps | Coverage varies; not all meets have `course_details` records |
| Pseudonymous IDs | Stable within this release; may change across major version updates |

### Is the dataset self-contained?

Yes. All files needed for analysis are included. No API access required. A non-anonymized source database is maintained separately by NRCD and is not publicly distributed.

### Does the dataset contain confidential data?

No direct identifiers. Pseudonymous integer IDs, gender, and grade at time of result are retained.

### Does the dataset contain offensive content?

No. Athletic performance records and meet metadata only.

---

## Collection Process

### How was the data associated with each instance acquired?

From officiated collegiate club running competitions, primarily those affiliated with [NIRCA](https://clubrunning.org/). Coaches, athletes, and volunteers submit meets to the NRCD platform; admins with domain expertise approve each meet against public result postings. Admins also proactively add meets from public sources nationwide.

### What mechanisms or procedures were used?

1. Community submission via [nationalrunningclubdatabase.com](https://www.nationalrunningclubdatabase.com/)
2. Expert review and approval (`approved = True`)
3. Athlete deduplication suggestions (name similarity) reviewed by admins
4. Weather data appended via OpenWeatherMap API where course records exist

### If the dataset is a sample from a larger set, what was the sampling strategy?

Not a sample. All approved records at export time are included.

### Who was involved in the data collection process?

NRCD maintainers, NIRCA community members, club coaches, athletes, and volunteers.

### Over what timeframe was the data collected?

Approved results from **2004 through May 2026**. The export contains both historical and comprehensive eras (see Coverage era above); it is not limited to post-2023 data.

### Were any ethical review processes conducted?

Yes. The removal of personally identifiable information and public release of this anonymized dataset was reviewed under protocols at the **Institutional Review Board (IRB), University of Notre Dame**. Source data consists of publicly posted meet results; no direct contact with athletes occurred for this export.

---

## Preprocessing / Cleaning / Labeling

### Was any preprocessing/cleaning/labeling done?

| Step | Description |
|------|-------------|
| Approval filter | Only `approved = True` meets and results retained |
| PII removal | Names, user IDs, hometowns, Strava links dropped |
| Field pruning | Media links, track-specific fields, relay teammate names removed |
| Referential trim | Lookup tables limited to entities referenced by filtered results |

### Was the "raw" data saved?

Yes. Unfiltered source records are retained by NRCD but are not part of this public release.

### Is the software used available?

Processing is documented in [`README.md`](README.md). Standardization code for the accompanying paper is at [github.com/National-Running-Club-Database/data_paper](https://github.com/National-Running-Club-Database/data_paper).

---

## Uses

### Has the dataset been used for any tasks already?

This release supports the following manuscript (under review; arXiv preprint forthcoming):

> Jonathan A. Karr Jr, Ryan M. Fryer, Ben Darden, Nicholas Pell, Kayla Ambrose, Evan Hall, Ramzi K. Bualuan, and Nitesh V. Chawla. 2026. **NRCD: An Open Database of Collegiate Running with Unified Performance Standardization.** *Under review.*

The paper describes community-governed curation, dataset composition, and a unified performance standardization framework (distance, elevation, heat, and venue adjustments).

### Is there a repository linking papers or systems?

- **Website:** [nationalrunningclubdatabase.com](https://www.nationalrunningclubdatabase.com/)
- **Zenodo:** [zenodo.org/records/17917357](https://zenodo.org/records/17917357)
- **Standardization code:** [github.com/National-Running-Club-Database/data_paper](https://github.com/National-Running-Club-Database/data_paper)

### What tasks could the dataset be used for?

- Longitudinal athlete performance modeling across seasons
- Environmental confounder analysis (weather, elevation, course distance)
- Gender-equity and participation research in club sports
- Team roster and geographic coverage studies
- Benchmarking sports-informatics methods on a large public corpus

### What might impact future uses?

- NIRCA-centric coverage; not representative of all collegiate running
- Club sports may under-represent certain institutions and regions
- Pseudonymous IDs may not persist across major version updates
- Combining with external data for re-identification is discouraged

### Are there tasks for which the dataset should not be used?

- Re-identification of athletes or other individuals
- Use without proper citation of the dataset and accompanying paper
- High-stakes individual decisions (e.g., recruiting rankings) without appropriate context and validation

---

## Distribution

### Will the dataset be distributed to third parties?

Yes. Intended for public research use under CC BY 4.0.

### How will the dataset be distributed?

Via [Zenodo](https://zenodo.org/records/17917357) and the [NRCD website](https://www.nationalrunningclubdatabase.com/).

### When will the dataset be distributed?

**v2.0.0** published June 5, 2026 (data through May 2026). New versions released yearly or when significant new data is approved.

### License

[Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/)

### Export controls

None known.

---

## Maintenance

### Who maintains the dataset?

The NRCD team — nationalrunningclubdatabase@gmail.com

### Contact

- Jonathan Karr: jkarr@nd.edu
- General: nationalrunningclubdatabase@gmail.com

### Will the dataset be updated?

Yes. Yearly public exports with semantic versioning on Zenodo. Corrections and new meets are incorporated as approved in the live database.

### Can others contribute?

Yes. Submit meet results and corrections through the NRCD platform.

---

## Citation

**Dataset (this release):**

> Karr, J., Darden, B., & Pell, N. (2026). *National Running Club Database — Public Anonymized Dataset* (Version 2.0.0) [Data set]. Zenodo. https://zenodo.org/records/17917357

**Paper (under review):**

> Karr, J. A., Jr, Fryer, R. M., Darden, B., Pell, N., Ambrose, K., Hall, E., Bualuan, R. K., & Chawla, N. V. (2026). NRCD: An Open Database of Collegiate Running with Unified Performance Standardization. *Under review.*

Replace with the assigned DOI after Zenodo upload if a new version-specific DOI is issued.

---

## Version History

| Version | Date | DOI / Record | Scope |
|---------|------|--------------|-------|
| v1.0.0 | 2025-07-31 | [10.5281/zenodo.16652626](https://doi.org/10.5281/zenodo.16652626) | Initial release; NIRCA cross country 2023–2024 |
| v1.1.0 | 2025-12-12 | [10.5281/zenodo.17917357](https://doi.org/10.5281/zenodo.17917357) | Added 2025 cross country season (2023–2025 XC) |
| v2.0.0 | 2026-06-06 | [zenodo.org/records/17917357](https://zenodo.org/records/17917357) | Full approved export (2004–May 2026): all sports, comprehensive + historical eras; 128,963 results, 29,609 athletes, 1,336 meets; accompanies paper (under review) |
