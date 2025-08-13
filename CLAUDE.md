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
- ✅ Comprehensive player stats scraping (>90% success rate, ~5,200+ records)
- ✅ Player aggregation functions for season statistics
- ✅ Player profile interface with game logs and context
- ✅ Game analysis interface to view all players in specific games

## File Structure
```
/Users/zack/CS/Python/
├── schedule.ipynb          # Main notebook with full pipeline
├── nfl_2024_schedule.csv   # Parsed schedule with PFR URLs
├── nfl_2024_data/          # Player stats (4 tables, ~5,200 records)
├── teams.json              # Team name to PFR code mapping
├── facts.txt               # NFL facts for scraper entertainment
├── archive/                # Completed intermediate files
├── project_history/        # Completed documentation
├── NFL-Regular-season-*.pdf # Source PDFs
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

## Available Interfaces
```python
# Load data
tables = load_all_game_data()
schedule_df = pd.read_csv('nfl_2024_schedule.csv')

# Get season leaders
top_rushers = get_top_players_by_stat('Rush_Yds', 'basic_offense', tables)

# Create player profile with game context
player_profile = create_player_profile("Lamar Jackson", tables, schedule_df)

# Analyze specific game
game_analysis = analyze_game_performance('2024_001', tables, schedule_df)
```

## Next Steps
- Add player metadata scraper (height, weight, position, etc.)
- Build predictive models using the rich temporal and contextual features
- Add more seasons as needed by providing their first Sunday dates

## Technical Notes
- Uses uv for package management
- Requires: pandas, pdfplumber, requests, beautifulsoup4
- VSCode kernel: `.venv/bin/python`
- Respectful scraping with 15-45 second delays
- Comprehensive error handling and retry logic

## Usage
```python
# Parse single season
games_df = parse_nfl_schedule_pdf('NFL-Regular-season-2024.pdf', 2024, first_sunday_2024)

# Combine multiple seasons
all_games = pd.concat([games_2023, games_2024], ignore_index=True)
```

The data is now ready for joining with player stats DataFrames on `game_id` for comprehensive NFL analytics.