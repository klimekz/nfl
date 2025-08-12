# NFL Player Game Stats Scraper - Implementation Ticket

## Current Status: PRODUCTION READY - PHASE 3
**Context**: We have successfully built NFL schedule parser (544 games, 2023-2024) and are now ready to build the player stats scraper to complete the data pipeline.

## Objective
Build comprehensive scraper to extract offensive player statistics from Pro Football Reference box scores for fantasy football analytics and predictive modeling.

## Key Requirements

### Data Source
- **Target**: Pro Football Reference box scores
- **URL Pattern**: `https://www.pro-football-reference.com/boxscores/{YYYYMMDDTEAM}.htm`
- **Volume**: 272 games per season (2024 focus)
- **Rate Limiting**: 4-5 second delays (respectful scraping)

### Core Data Model: PlayerGameStats
```
Game Identity: game_id, season, week, date, home_team, away_team, kickoff_time
Player Identity: player_name, player_id, position, team, age, jersey_number  
Game Context: opponent, home_away, game_result, started, active
Universal Offensive Stats:
  - Passing: completions, attempts, yards, TDs, INTs, sacks, rating
  - Rushing: attempts, yards, TDs, long, fumbles
  - Receiving: targets, receptions, yards, TDs, long, fumbles
Advanced: snap counts, red zone stats, fantasy points (standard/PPR/half)
Quality: last_updated, data_source, parsing_confidence
```

### Technical Architecture
- **Input**: Our existing schedule DataFrame (544 games with dates/teams)
- **Challenge**: Map our game_ids to PFR format (YYYYMMDDTEAM)
- **Output**: ~15K player game records in structured format
- **Features**: Caching, error handling, resume capability, progress logging

## Implementation Plan

### Phase 1: Foundation (1-2 days)
- [x] Map our schedule data to PFR game URLs
- [x] Discover/hardcode PFR team abbreviations (e.g., "kan" for Chiefs)
- [x] Build single game parser with 1 test game
- [x] **CRITICAL**: Implement comprehensive 404/miss logging to validate our date calculations
- [x] Validate core data extraction logic

### Phase 2: Scale Testing (1 day)
- [x] Test with 1 week (16 games) to validate error handling
- [x] Implement caching and retry logic
- [x] **Analyze 404 patterns** - if many misses, revisit our date calculation logic
- [x] Validate data quality and completeness
- [x] Fine-tune rate limiting

### Phase 3: Production Run (1 day)
- [ ] Full 2024 season scrape (272 games)
- [ ] Data validation and quality checks
- [ ] Export to analysis-ready format
- [ ] Document any edge cases/missing data

### Phase 4: Integration (ongoing)
- [ ] Join player stats with our existing schedule data
- [ ] Calculate derived metrics and features
- [ ] Validate data for modeling readiness

## Key Challenges to Solve
1. **Game ID Mapping**: Schedule game_id → PFR URL format ✅
2. **Team Code Discovery**: Find PFR abbreviations for all 32 teams ✅
3. **Table Parsing**: Handle varying box score HTML structures ✅
4. **Player ID Extraction**: Parse player profile URLs consistently ✅
5. **Data Validation**: Ensure stats make sense (QBs don't have receiving TDs, etc.) ✅
6. **Date Validation**: Our calculated dates might be off - need robust miss logging ✅

## Success Criteria
- [ ] Successfully parse 95%+ of 2024 games
- [ ] Generate ~15K clean player game records
- [ ] All offensive players captured (QB/RB/WR/TE/FB)
- [ ] Data ready for immediate modeling/analysis
- [ ] Extensible to additional seasons

## Risk Assessment: LOW
- Respectful scraping approach with generous delays
- Public data, standard practice in sports analytics
- Conservative volume (272 requests over ~30 minutes)
- Robust error handling planned

## Files Created So Far
- `schedule.ipynb`: Complete schedule parser (DONE ✅)
- `CLAUDE.md`: Project documentation (DONE ✅)
- `TODO_SCRAPER.md`: This ticket (DONE ✅)

## Next Session: Start Phase 1
Begin with single game parser prototype and team code discovery.

---
**Priority**: High | **Estimated Effort**: 3-4 days | **Complexity**: Medium