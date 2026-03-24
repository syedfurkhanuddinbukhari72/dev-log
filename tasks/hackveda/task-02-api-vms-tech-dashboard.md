# Task 02 - API & Data Resiliency

### Problem
*   **Data Hydration Error**: Dashboard appeared empty with `revenue: Array(0)` in the logs.
*   **Cause**: `mockData.json` had all 12 monthly entries restricted to the "North" region. Selecting any other region (South, West, East) resulted in 100% filtered-out data.
*   **Console Noise**: Tracking Prevention warnings from Chart.js CDN were cluttering the logs.

### Approach
*   **Regional Diversity**: Updated the local `mockData.json` schema to distribute data points across all four regions (North, South, East, West).
*   **Hybrid Strategy**: Implemented logic in `fetcher.js` to automatically prioritize local `mockData.json` on `localhost` to bypass CORS issues, while maintaining the Live Proxy for production.

### Fixes
*   **Data Fix**: Corrected the `region` field for months Apr-Dec in `src/data/mockData.json`.
*   **UI Resiliency**: Added deep-inspection logging in `app.js` to catch and report empty data arrays effectively.
*   **Dependency Note**: Verified that "Tracking Prevention" messages are non-breaking browser security measures.

### Learning
*   **Mock Hygiene**: An industry-ready mock must represent **all** possible UI states (all regions) to avoid false "No Data" bug reports.
*   **Environment Awareness**: Professional apps must handle `localhost` differently than `production` regarding CORS and Proxy tunnels.

---
*Status: Task-02 Data Layer Certified (Local).*
