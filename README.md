# NRCD Data

This directory contains filtered cross country running data for the 2023-2024 season, processed to remove personal identifying information and focus on individual running events.

## Dataset Summary

This dataset contains cross country running results from the 2023-2024 season across multiple collegiate teams and meets. The data has been anonymized and filtered to focus on individual running performance while maintaining the integrity of race results and team affiliations.

**Key Statistics:**
- **Time Period**: August 2023 - December 2024
- **Sport Focus**: Cross country running only
- **Data Type**: Individual race results, team affiliations, course details, and weather conditions
- **Privacy**: All personal identifying information has been removed
- **Scope**: Collegiate cross country meets and events

**Dataset Size:**
- **Results**: 15,397 individual race results
- **Athletes**: 5,585 unique athletes
- **Meets**: 179 cross country meets
- **Course Details**: 192 course/weather records
- **Teams**: 121 collegiate teams
- **Athlete-Team Associations**: 5,589 team affiliations (4 athletes on multiple teams)

## Overview

The data in this directory has been filtered from the original dataset to:
- Include only cross country running events (2023-2024 season)
- Remove personal identifying information (names, user IDs)
- Focus on individual running events (no track and field or relay events)
- Remove unnecessary fields (links, photos, track-specific data)

## Data Files

### Core Data Files

| File | Description | Key Fields |
|------|-------------|------------|
| `athlete.csv` | Athlete information (PII removed) | `athlete_id`, `gender`, `grade` |
| `athlete_team_association.csv` | Athlete-team relationships | `athlete_id`, `team_id` |
| `course_details.csv` | Course and weather information | `meet_id`, `running_event_id`, `elevation_gain`, `weather_conditions` |
| `joined.csv` | Comprehensive view combining all data | All relevant fields from other tables |
| `meet.csv` | Meet information | `meet_id`, `meet_name`, `start_date`, `location` |
| `result.csv` | Individual race results | `athlete_id`, `meet_id`, `running_event_id`, `result_time` |
| `running_event.csv` | Event definitions (running only) | `running_event_id`, `event_name` |
| `sport.csv` | Sport information (cross country only) | `sport_id`, `sport_name` |
| `team.csv` | Team information (PII removed) | `team_id`, `team_name`, `region`, `city`, `state` |

### Data Filtering Applied

#### Removed Fields
- **Personal Information**: `first_name`, `last_name`, `user_id`
- **Links and Media**: `external_result_link`, `photo_link`, `team_logo`, `team_photo`, `website`, `instagram`
- **Track-Specific**: `track_distance`, `banked_track`
- **Relay Data**: 
  - Split times: `relay_split`, `relay_split_2`, `relay_split_3`
  - Relay teammate IDs: `athlete_id_2`, `athlete_id_3`, `athlete_id_4`
  - Relay teammate grades: `grade_2`, `grade_3`, `grade_4`
  - Relay teammate names: `athlete2_first_name`, `athlete2_last_name`, `athlete3_first_name`, `athlete3_last_name`, `athlete4_first_name`, `athlete4_last_name`
  - Relay teammate gender: `athlete2_gender`, `athlete3_gender`, `athlete4_gender`
- **Approval Status**: `approved` fields
- **Current Grade**: `current_grade` from athlete-team associations

**Note**: `athlete_id`, `team_id`, `meet_id`, and `running_event_id` are preserved to maintain data relationships across tables.

#### Event Filtering
- **Included**: Distance running events (55m to Marathon)
- **Excluded**: Hurdles, jumps, throws, pole vault, relays, and other track events

#### Time Period
- **Season**: August 1, 2023 to December 31, 2024
- **Sport**: Cross country only (`sport_id = 1`)

## Data Relationships

```
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

- All personal identifying information has been removed
- Only individual running events are included (no relays)
- Weather data is available for many events
- Course elevation and distance information is included where available
- Results are filtered to the specified time period and sport

## File Sizes and Records

The filtered dataset is significantly smaller than the original:
- Focused on cross country running only
- Removed track events and relays
- Eliminated PII and unnecessary fields
- Optimized for analysis and research purposes

## Contact

Authors and emails are anonymized for the review process.

For questions about this dataset or to report issues, please contact the data maintainers through the appropriate channels. This dataset is provided for research and analysis purposes only.

**Usage Terms:**
- This dataset is anonymized and suitable for public research
- Please cite appropriately if used in publications
- Report any data quality issues to the maintainers 