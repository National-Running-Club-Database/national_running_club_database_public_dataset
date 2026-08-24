# NRCD Data

This dataset contains the National Running Club Database with personal identifiable information (PII) removed.

**Version:** v2.1.0 — [Zenodo](https://zenodo.org/records/17917357) (prior releases: v1.0.0, v1.1.0 cross country only; v2.0.0 all sports through May 2026)  
**Data coverage:** 2003 – July 2026  
**Related paper:** Karr et al., *NRCD: An Open Database of Collegiate Running with Unified Performance Standardization* ([arXiv:2608.14776](https://arxiv.org/abs/2608.14776))  
**Update cadence:** Public exports are updated yearly

For structured metadata, provenance, and intended-use documentation, see [`DATASHEET.md`](DATASHEET.md) (following the [Datasheets for Datasets](https://doi.org/10.1145/3458723) framework).

Last updated: August 24, 2026

## Dataset Summary

This dataset contains collegiate running results across multiple sports and seasons from **2003 through July 2026**. It includes both **comprehensive** data (August 2023 onward, full metadata) and **historical** data (through July 2023, partial metadata). See [`DATASHEET.md`](DATASHEET.md) for era breakdown by sport.

**Key Statistics:**
- **Time Period**: Historical results through July 2023; comprehensive results with full metadata from August 2023 to July 2026
- **Sport Focus**: Cross Country, Indoor Track, Outdoor Track, and Road Race
- **Data Type**: Individual race results, team affiliations, meet series, course details, and weather conditions
- **Privacy**: All personal identifying information has been removed under IRB approval from the University of Notre Dame
- **Scope**: Approved meets and results across all sports and seasons (`approved` is applied as a filter and is not retained as a column)

**Dataset Size:**
- **Results**: 143,868 individual race results
- **Athletes**: 31,786 unique athletes
- **Meets**: 1,423 meets
- **Meet series**: 260 series (878 meet–series memberships)
- **Course Details**: 1,183 course/weather records
- **Teams**: 190 collegiate teams
- **Athlete-Team Associations**: 31,796 team affiliations (10 athletes on multiple teams)

## Overview

The data in this directory has been filtered from the original dataset to:
- Include all sports and seasons (no sport or date filtering)
- Keep only approved meets and results
- Remove personal identifying information (names, user IDs)
- Remove unnecessary fields (links, photos, track-specific data, `is_hidden`, `approved`)

## Data Files

### Core Data Files

| File | Description | Key Fields |
|------|-------------|------------|
| `athlete.csv` | Athlete information (PII removed) | `athlete_id`, `gender` |
| `athlete_team_association.csv` | Athlete-team relationships | `athlete_id`, `team_id` |
| `course_details.csv` | Course, weather, and venue metadata | `meet_id`, `running_event_id`, `elevation_gain`, `altitude`, `weather_conditions`, `temperature`, `dew_point` |
| `joined.csv` | Comprehensive view combining all data | All relevant fields from other tables |
| `meet.csv` | Meet information | `meet_id`, `meet_name`, `start_date`, `meet_city`, `meet_state`, `altitude` |
| `meet_series.csv` | Recurring meet series definitions | `series_id`, `display_name`, `sport_id` |
| `meet_series_member.csv` | Meet-to-series membership | `meet_id`, `series_id` |
| `result.csv` | Individual race results | `athlete_id`, `meet_id`, `running_event_id`, `result_time` |
| `running_event.csv` | Event definitions | `running_event_id`, `event_name` |
| `sport.csv` | Sport information | `sport_id`, `sport_name` |
| `team.csv` | Team information | `team_id`, `team_name`, `region`, `city`, `state` |

### Data Filtering Applied

#### Removed Fields
- **Personal Information**: `first_name`, `last_name`, `user_id`
- **Links and Media**: `external_result_link`, `photo_link`, `team_logo`, `team_photo`, `website`, `instagram`, contact/practice fields
- **Track-Specific**: `track_distance`, `banked_track`
- **Relay Teammate Names** (from `joined.csv` only): `athlete2_first_name`, `athlete2_last_name`, `athlete3_first_name`, `athlete3_last_name`, `athlete4_first_name`, `athlete4_last_name`, `athlete2_gender`, `athlete3_gender`, `athlete4_gender`
- **Platform-only**: `is_hidden`, pending-edit IDs, editor audit fields, `meet_series.created_at`
- **Approval Status**: `approved` (used only as an inclusion filter; all rows in this export are approved)
- **Current Grade**: `current_grade` from athlete-team associations

**Note**: `athlete_id`, `team_id`, `meet_id`, `series_id`, and `running_event_id` are preserved to maintain data relationships across tables.

#### Scope
- **Approved only**: Meets and results must have `approved = True` in the source
- **All sports**: Cross Country, Indoor Track, Outdoor Track, and Road Race
- **Complete coverage**: Full results and metadata from August 2023 onward
- **Historical coverage**: Partial results back to 2003

## Data Relationships

```
meet_series.csv (series_id)
    ↓
meet_series_member.csv (series_id, meet_id)
    ↓
meet.csv (meet_id)
    ↓
result.csv (meet_id, athlete_id, running_event_id)
    ↓
athlete.csv (athlete_id) ← athlete_team_association.csv (athlete_id, team_id) → team.csv (team_id)
    ↓
course_details.csv (meet_id, running_event_id)
    ↓
running_event.csv (running_event_id)
```

**Data Integrity**: All foreign key relationships are preserved to maintain referential integrity across the dataset.

## Data Quality Notes

- All personal identifying information has been removed under IRB approval from the University of Notre Dame
- Only approved meets and results are included
- Complete results with metadata from August 2023; historical results back to 2003 (both eras included)
- **`meet.altitude`** and **`course_details.altitude`** — venue altitude in meters
- Weather, course elevation gain/loss, and distance information included where available
- Related tables are trimmed to records referenced by the filtered results
- Meet series memberships are limited to approved meets present in this export

## File Sizes and Records

The filtered dataset is smaller than the original source files:
- Removed unapproved meets and results
- Eliminated PII and unnecessary fields
- Optimized for analysis and research purposes

## Contact

**Main Contact:** 
[![ORCID](https://img.shields.io/badge/Jonathan_A._Karr_Jr.-0009--0000--1600--6122-A6CE39?style=flat&logo=orcid&logoColor=white)](https://orcid.org/0009-0000-1600-6122) (jkarr@nd.edu)

**Other Authors:**
[![ORCID](https://img.shields.io/badge/Ben_Darden-0009--0008--3808--1375-A6CE39?style=flat&logo=orcid&logoColor=white)](https://orcid.org/0009-0008-3808-1375)
[![ORCID](https://img.shields.io/badge/Nicholas_Pell-0009--0001--1289--5054-A6CE39?style=flat&logo=orcid&logoColor=white)](https://orcid.org/0009-0001-1289-5054)
[![ORCID](https://img.shields.io/badge/Ryan_M._Fryer-0009--0008--3591--3877-A6CE39?style=flat&logo=orcid&logoColor=white)](https://orcid.org/0009-0008-3591-3877)

**General Inquiries:** nationalrunningclubdatabase@gmail.com

For questions about this dataset or to report issues, please contact the authors through the provided email addresses. This dataset is provided for research and analysis purposes only.

**Usage Terms:**
- This dataset is anonymized and suitable for public research
- Please cite appropriately if used in publications
- Report any data quality issues to the maintainers
