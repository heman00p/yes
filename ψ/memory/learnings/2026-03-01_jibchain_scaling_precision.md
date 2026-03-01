# Lesson Learned: Critical Unit Scaling for JIBCHAIN IoT Data

**Date**: 2026-03-01
**Source**: Session /rrr
**Concept**: #Web3 #IoT #JIBCHAIN #Scaling #ViemJS

## The Problem
When reading sensor data stored in smart contracts (e.g., FloodBoy sensor stores), the values are often stored as integers with implicit decimal places (x100, x1000, x10000). Displaying these raw values without proper division leads to extreme inaccuracies (e.g., 3.02 meters showing as 30200 meters).

## The Insight
The `unit` string provided by the contract's `getAllFields` function is the source of truth for scaling. However, common AI patterns often default to dividing by 100 or 1000, missing the specific requirements for high-precision environmental sensors.

## The Strategy
1. **Dynamic Scaling Parser**: Implement a robust parser that checks for `x[NUMBER]` patterns in the unit string.
2. **x10000 Case**: Specifically handle `x10000` by dividing the raw value by `10000` to convert to base units (e.g., meters).
3. **Decimal Precision**:
   - Voltage (x100): Use 3 decimal places (e.g., `13.840 V`).
   - Depth/Height (x10000): Use 4 decimal places (e.g., `3.0200 m`).

## Example Implementation (Viem.js/JS):
```javascript
function processValue(value, unit) {
  if (unit.includes('x100')) return (Number(value) / 100).toFixed(3);
  if (unit.includes('x1000')) return (Number(value) / 1000).toFixed(3);
  if (unit.includes('x10000')) return (Number(value) / 10000).toFixed(4);
  return value;
}
```

## Impact
Accurate data representation is critical for flood monitoring and disaster response systems. Incorrect scaling can trigger false alarms or fail to detect real threats. Following this rule ensures the visualization reflects physical reality.
