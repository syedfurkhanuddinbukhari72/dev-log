# Task 01 - API: VMS Techs Dashboard

### Problem
- Analysts needed a resilient way to fetch real-time data without the dashboard breaking during API outages.

### Approach
- **Fetcher Logic**: Built an `async/await` module in `src/api/fetcher.js`.
- **Fallback Layer**: Integrated `src/data/mockData.json` to take over instantly if `fetch()` fails.
- **Data Shape**: Extracted key metrics (Value, Growth, Period) from JSON response.

### Errors & Fixes
- **Error**: `fatal: refusing to merge unrelated histories`.
- **Reason**: Local and remote repositories had different initial commits.
- **Fix**: Used `--allow-unrelated-histories` and a force push to sync the structures.

### Learning
- **Resiliency**: Designing for "Offline First" (using mock data) makes the demo much more stable for presentations.
- **Async Pattern**: Sequential `try-catch` blocks are better than `Promise.all` when order of priority (Remote > Local) matters.
