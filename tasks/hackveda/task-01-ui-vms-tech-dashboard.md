# Task 01 - UI

## Problem

* **Visual Glitch**: The Annual Revenue KPI card displays a conflicting `+-` symbol for negative trends (e.g., `+-10.5%`).
* **Impact**: Decreases dashboard professionalism and causes user confusion regarding data direction.

## Approach

* **File involved**: Modified `src/js/app.js` within the `updateUI` function.
* **Logic Correction**: Implemented conditional string interpolation to distinguish between positive and negative floats.

## Errors & Fixes

* **Error**: Trend displayed as `+-10.5%`.
  * **Reason**: Static prefixing of `+` in the template literal combined with `.toFixed(1)` which already includes a `-` for negative numbers.
  * **Fix**: Used `parseFloat(growth) >= 0 ? "+${growth}%" : "${growth}%"` to ensure clean prefixing.

## Root Cause

* **String Literal Mismanagement**: Hardcoded `+` prefix in the UI update loop without checking the mathematical sign of the growth value.

## Learning

* **Floating Point Accuracy**: Always cast string-formatted numbers (from `.toFixed()`) back to floats before performing logical comparisons.
* **UI Resilience**: Visual symbols should be treated as data-driven elements, not static template parts.

## Improvements

* **Color Sync**: Future updates should sync the trend color (green/red) with the mathematical sign for better accessibility.
