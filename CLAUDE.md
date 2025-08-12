# NFL Schedule Parser Project

## Overview
This project parses NFL schedule PDFs to extract game data into structured DataFrames for analysis and modeling. We've successfully built a parser that handles both regular season schedules and extracts comprehensive game metadata.

## Current State
- ✅ Successfully parsing 2023 and 2024 NFL schedule PDFs
- ✅ Extracting all 272 games per season (544 total)
- ✅ Handling both "at" (regular) and "vs" (international) games
- ✅ Clean team name extraction
- ✅ Date calculation from first Sunday + week estimation
- ✅ Rich metadata extraction: times, networks, special info

## File Structure
```
/Users/zack/CS/Python/
├── schedule.ipynb          # Main parsing notebook
├── NFL-Regular-season-2023.pdf
├── NFL-Regular-season-2024.pdf
├── pyproject.toml         # uv project config
└── CLAUDE.md             # This file
```

## Key Functions in schedule.ipynb

### `parse_nfl_schedule_pdf(pdf_path, season_year, first_sunday)`
Main parser that extracts games from PDF and returns DataFrame with columns:
- `game_id`: Unique identifier (e.g., "2024_001") 
- `season`: Year
- `week`: Calculated week number
- `game_date`: Calculated actual date
- `day_of_week`: Thu/Sun/Mon etc.
- `away_team`, `home_team`: Clean team names
- `local_time`, `et_time`: Game times
- `timezone`: Time zone
- `tv_network`: Broadcasting network
- `special_info`: International locations, holidays
- `is_international`: Boolean for international games

### Season Start Dates
- 2023: First Sunday = September 10, 2023
- 2024: First Sunday = September 8, 2024

## Data Output
- 2023: 272 games
- 2024: 272 games  
- Total: 544 games across both seasons
- All 32 NFL teams represented with 17 games each

## Next Steps
- Join this game data with player performance stats using `game_id`
- Build predictive models using the rich temporal and contextual features
- Add more seasons as needed by providing their first Sunday dates

## Technical Notes
- Uses uv for package management
- Requires: pandas, PyPDF2, datetime
- VSCode kernel: `.venv/bin/python`
- Games calculated at ~16 per week for date estimation

## Usage
```python
# Parse single season
games_df = parse_nfl_schedule_pdf('NFL-Regular-season-2024.pdf', 2024, first_sunday_2024)

# Combine multiple seasons
all_games = pd.concat([games_2023, games_2024], ignore_index=True)
```

The data is now ready for joining with player stats DataFrames on `game_id` for comprehensive NFL analytics.