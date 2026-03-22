# Task 01 - API

## Problem

* **System Failure**: Dashboard remains empty or crashes because it attempts to fetch data from an unreachable endpoint.
* **Impact**: The "Annual Revenue" card and charts fail to render because the "Waiter" (API) never returns from the "Kitchen" (Database).

## Approach

* **Diagnostic**: Analyzed the communication gap between the frontend and backend using the **Restaurant Analogy**.
* **Files involved**: Modified `src/api/fetcher.js` to investigate the handshake process.

## Errors & Fixes

* **Error**: `ERR_NAME_NOT_RESOLVED`.
  * **Reason**: Using a "fake" production address (`api.vms-techs.com`) that hasn't been registered on the internet.
  * **Fix**: Implement a "Temporary Waiter" using Mocky.io to provide a real, reachable URL.

* **Error**: `Cannot read properties of undefined (reading 'value')`.
  * **Reason**: The fetcher fails to find the address, leaving the data variable empty/undefined.
  * **Fix**: Ensure the API returns a valid JSON package before the frontend attempts to "draw" the charts.

## Root Cause

* **Endpoint Absence**: The single most critical issue is the lack of a reachable DNS-mapped URL to act as the middleman for data flow.

## Learning

* **API Middleware**: The API is not just a link; it's the specific "Waiter" that packages raw database info into JSON for the dashboard to consume.
* **The Handshake**: A dashboard's visual "Glow" is entirely dependent on a successful request-response cycle.
* **Integration Strategy**: Using Mocky.io allows for "Production Simulation" when the primary backend is under maintenance or unregistered.

## Improvements

* **Transition Plan**: Move from static `mockData.json` to a **Live Mocky URL** to practice real-world HTTP header handling and async timing.
