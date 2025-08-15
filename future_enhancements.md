# Future Model Enhancements

## Coaching & Roster Context Data

### Problem
Current trajectory models assume "everything else stays equal" but NFL rosters/coaching never do. Historical data misses critical context that could dramatically improve predictions.

### Missing Factors
1. **Coaching Changes**
   - New OC/HC hires completely alter offensive philosophy
   - Different play-calling tendencies (run/pass ratios, red zone usage)
   - Historical offensive stats from coach's previous teams

2. **Roster Composition Changes** 
   - Draft picks/FA signings at same position (RB1 → RB2 scenarios)
   - Departing players creating target share opportunities
   - O-line turnover affecting rushing/passing efficiency

3. **Scheme Transitions**
   - West Coast vs Air Raid vs Power Run philosophies  
   - Slot usage vs outside WR emphasis
   - TE-heavy vs 3+ WR sets

### Data Sources to Add
- **Coaching hire dates** + their historical offensive tendencies
- **Depth chart changes** (signings, departures, draft position)
- **Offensive line turnover** rates and quality metrics
- **Target share redistribution** when key players leave/arrive
- **Scheme indicators** from formation/play-calling data

### High-Impact Use Cases
- Players with new OCs (usage pattern shifts)
- Backups who became starters (opportunity increase)  
- Veterans with new competition (regression risk)
- Teams with major roster overhaul

### Implementation Ideas
1. Scrape coaching change announcements + their previous team stats
2. Track roster moves via NFL transactions
3. Build "scheme similarity" scores between old/new coaches
4. Weight historical data less when major changes occurred

### Expected Impact
Could significantly improve edge cases where pure trajectory fails:
- Breakout seasons from scheme fit
- Regression from increased competition
- Usage shifts from new coaching philosophy

---
*Captured during fantasy model development - return to this after core model is complete*