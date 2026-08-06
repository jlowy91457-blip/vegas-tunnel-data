# Vegas Tunnel Guide — Live Data Feed

This repository hosts the live JSON data file for the **Vegas Tunnel Guide** app. The app fetches this file on every launch to get the latest station info, pricing, hours, and network stats.

**Data URL:** https://jlowy91457-blip.github.io/vegas-tunnel-data/vegas-tunnel-data.json

## How to Update App Data

You don't need to redeploy the app or release an app update. Just edit the JSON file here on GitHub:

1. Go to [vegas-tunnel-data.json](./vegas-tunnel-data.json)
2. Click the pencil icon (Edit) in the top right
3. Make your changes (add stations, update pricing, change hours, etc.)
4. Add a commit message like "Update pricing for 2026 holiday season"
5. Click "Commit changes"

Changes appear in the app within 5-10 minutes (GitHub Pages cache).

## JSON Structure

```json
{
  "version": "2026.08.06",          // Version label shown in app
  "lastUpdated": "2026-08-06",      // Date shown in app footer
  "stations": [...],                 // Array of station objects
  "network": {...},                  // Route graph (edges with times/costs)
  "pricing": [...],                  // Ticket pricing table rows
  "pricingNote": "...",              // Note below pricing table
  "hours": [...],                    // Operating hours rows
  "hoursNote": "...",                // Note below hours
  "stats": [...]                     // Network statistics rows
}
```

### Station Object Fields

| Field | Type | Description |
|---|---|---|
| `id` | string | Unique identifier (used in network graph) |
| `name` | string | Display name |
| `status` | string | "operational", "planned", or "construction" |
| `area` | string | Area category for filtering |
| `areaLabel` | string | Human-readable area name |
| `integration` | string | Hotel/venue partner |
| `notes` | string | Additional info shown in station details |
| `lat` | number | Latitude for map placement |
| `lng` | number | Longitude for map placement |
| `category` | string | "lvcc", "operational", "planned" (controls map marker color) |

### Network Edge Object

```json
"station-id": {
  "destination-id": {
    "type": "tunnel",     // "tunnel" or "surface"
    "time": 30,           // Travel time in seconds
    "cost": 0             // Cost in dollars (0 = free)
  }
}
```

## Important Notes

- Station IDs in the `network` object must match IDs in the `stations` array
- If the JSON fails validation, the app falls back to its bundled data
- Keep the `version` and `lastUpdated` fields current so users can see data freshness
- Test your JSON at [jsonlint.com](https://jsonlint.com/) before committing if you're unsure
