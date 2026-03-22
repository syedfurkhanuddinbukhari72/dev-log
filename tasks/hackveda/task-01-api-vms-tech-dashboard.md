# Task 01 - API

## Problem

* Total breakdown in data communication between frontend and backend.
* Dashboard KPI cards and line charts fail to populate, resulting in empty or broken UI states.

## Approach

* Analyzed browser console logs and network tab for `fetcher.js:8`.
* Investigated retry logic and error handling patterns during network outages.

## Errors & Fixes

* **Error**: `net::ERR_NAME_NOT_RESOLVED` for `api.vms-techs.com`.
    * **Reason**: The production API endpoint domain cannot be resolved by DNS, causing all fetch requests to fail immediately.
    * **Fix**: Verify DNS records for `api.vms-techs.com` or switch to a stable development/local IP environment.

* **Error**: `Cannot read properties of undefined (reading 'value')`.
    * **Reason**: Frontend logic tries to access nested properties of the API response before verifying the data object exists.
    * **Fix**: Implement optional chaining (`data?.revenue?.value`) and ensure the local `mockData.json` fallback triggers correctly.

* **Error**: `500 Internal Server Error`.
    * **Reason**: Backend service crash during retry attempts, indicating server-side instability.
    * **Fix**: Check server logs for memory leaks or unhandled exceptions in the API service.

## Root Cause

* **DNS Resolution Failure**: The primary API endpoint is unreachable at the network level, triggering secondary logic crashes in the frontend.

## Learning

* **Defensive Coding**: Never assume an API response will be populated; always provide default objects for the UI to consume.
* **Network Robustness**: DNS-level failures highlight why "Local Fallback" is the most critical feature of a production-ready dashboard.

## Improvements

* **Circuit Breaker**: Implement a mechanism that stops trying the production API after 3 consecutive DNS failures and stays on Mock Data until a manual reset.
* **Global Error Boundary**: Add a UI-level check that displays a "Maintenance Mode" banner instead of raw JavaScript console errors.
