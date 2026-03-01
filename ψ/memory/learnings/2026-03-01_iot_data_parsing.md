# Handling Malformed IoT Data Streams

When consuming live, raw data streams from IoT devices (like Dustboy via MQTT), it is crucial to employ defensive programming techniques. Devices may send inconsistent keys (e.g., `pm25`, `pm2_5`, `pm2`) or occasionally drop non-JSON status messages (like `"offline"`) into a data topic. 

### Key Practices:
1. **Fuzzy Key Matching:** Instead of demanding exact key names, use `.includes()` or specific alias lists when parsing the JSON keys to find the target data.
2. **Pre-Parse Validation:** Before running `JSON.parse()`, check if the raw string is a known system message (like "offline" or "online") to avoid throwing unhandled syntax errors that crash the application's update loop.
3. **Graceful Fallbacks:** If a specific value cannot be found or parsed, default to a safe state (like `0` or `"N/A"`) rather than propagating `undefined` or `NaN` into the UI or calculation layers.