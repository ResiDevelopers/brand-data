# Location Data Schema

Each brand has a `locations.json` file under `data/{brand-slug}/`. Files are compiled automatically from the brand's Google Sheet via Apps Script and committed to this repository on a scheduled basis.

## File Path

```
data/{brand-slug}/locations.json
```

## GitHub Pages URL

```
https://{org}.github.io/resibrand-data/data/{brand-slug}/locations.json
```

## JSON Structure

```json
{
  "{brand-slug}": [
    {
      "slug": "austin",
      "name": "Austin",
      "owner_name": "Jane Smith",
      "phone": "(512) 555-0100",
      "working_days": "Mon-Sat:",
      "working_hours": "7:00am - 7:00pm",
      "time_zone": "CST",
      "lat": 30.2672,
      "lng": -97.7431,
      "zip_codes": ["78701", "78702", "78703"],
      "shortcodes": {
        "city": "Austin",
        "state": "Texas",
        "location": "Austin",
        "location_possessive": "Austin's",
        "state_possessive": "Texas'",
        "region": "Central",
        "service_area_1": "Downtown Austin",
        "service_area_2": "South Austin",
        "service_area_3": "North Austin"
      }
    }
  ]
}
```

## Field Reference

| Field | Type | Description |
|---|---|---|
| `slug` | string | Unique location identifier, matches the Google Sheet location ID |
| `name` | string | Human-readable location name |
| `owner_name` | string | Franchise owner name |
| `phone` | string | Location phone number |
| `working_days` | string | Days of operation |
| `working_hours` | string | Hours of operation |
| `time_zone` | string | Timezone abbreviation (e.g. CST, MST, EST) |
| `lat` | number \| null | Latitude of location center |
| `lng` | number \| null | Longitude of location center |
| `zip_codes` | string[] | ZIP codes served by this location — primary input for lead routing |
| `shortcodes` | object | Template variables injected into page content and SEO fields |

## Lead Routing

The lead server loads this file into memory at startup and uses `zip_codes` to route incoming leads to the correct location. See the lead server `ARCHITECTURE.md` for full routing algorithm details.

## Updating Data

Data is managed via each brand's Google Sheet. The Apps Script compiler commits updated JSON to this repository automatically. Do not edit JSON files directly — changes will be overwritten on the next compile.
