# Task 01 - UI

## Problem

* **Design Requirement**: Needed a high-contrast, premium "Live" look to reduce decision-making uncertainty for stakeholders.
* **Visual Glitch**: The Annual Revenue KPI card displays a conflicting `+-` symbol for negative trends (e.g., `+-10.5%`).

## Approach

* **Theme**: Implemented a **Dark Mode** high-contrast CSS theme in `src/css/style.css`.
* **KPIs**: Designed premium cards with CSS animations (Pulse effect) for the "Live" status indicators.
* **Charts**: Integrated **Chart.js** with custom linear gradients and 0.4 tension for smooth, professional curves.
* **Pulse**: Connected all UI elements to an automatic refresh cycle for real-time data visibility.
* **Logic Correction**: Implemented conditional string interpolation in `src/js/app.js` to distinguish between positive and negative floats.

## Errors & Fixes

* **Error**: Chart flickered/re-animated every 5 seconds.
  * **Reason**: Default Chart.js update behavior resets animations on each data refresh.
  * **Fix**: Used `chart.update('none')` to ensure seamless "live" updates without distracting the user.

* **Error**: Trend displayed as `+-10.5%`.
  * **Reason**: Static prefixing of `+` in the template literal combined with `.toFixed(1)` which already includes a `-` for negative numbers.
  * **Fix**: Used `parseFloat(growth) >= 0 ? "+${growth}%" : "${growth}%"` to ensure clean prefixing.

## Root Cause

* **String Literal Mismanagement**: Hardcoded `+` prefix in the UI update loop without checking the mathematical sign of the growth value.

## Learning

* **UX Psychology**: Micro-animations (like the pulse dot) provide "Proof of Life" that reassures the user the data is current.
* **Performance**: High-frequency chart updates are more efficient when bypassing global transitions.
* **UI Resilience**: Visual symbols should be treated as data-driven elements, not static template parts.

## Improvements

* **Color Sync**: Future updates should sync the trend color (green/red) with the mathematical sign for better accessibility.
