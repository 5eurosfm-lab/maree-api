# French Tide Data API

A Next.js API that provides French tide data by scraping information from marine.meteoconsult.fr.

## Features

- 🌊 Get tide times and heights for French coastal locations
- 📍 Search for locations by name
- 📅 Retrieve data for specific months and years
- 🌙 Includes ephemeris data (moon phases, sunrise/sunset times)
- 📊 Tide coefficients
- 🗺️ Location coordinates

## API Endpoints

### 1. Get Tide Data
```
GET /api/data
```

**Parameters:**
- `location` (optional) - Location code (default: "nantes-chantenay-1018")
- `month` (optional) - French month name (default: current month)
- `year` (optional) - Year (default: current year)

**Example:**
```
GET /api/data?location=nantes-chantenay-1018&month=aout&year=2025
```

**Response:**
```json
{
  "success": true,
  "location": "nantes-chantenay-1018",
  "locationName": "Nantes (Chantenay)",
  "coordinates": {
    "longitude": "Longitude : 1°35'0'' W",
    "latitude": "Latitude : 47°12'0'' N"
  },
  "period": "aout-2025",
  "data": [
    {
      "date": "01/08/2025",
      "coefficients": [95, 92],
      "mb1": { "time": "06:15", "height": "1.20m" },
      "mh1": { "time": "12:30", "height": "5.80m" },
      "mb2": { "time": "18:45", "height": "1.10m" },
      "ephemeris": {
        "moon": { "phase": "Premier quartier" },
        "saint": "Saint Alphonse",
        "sun": {
          "sunrise": "06:35",
          "sunset": "21:25",
          "duration": "14h50",
          "durationChange": "+2min"
        }
      }
    }
  ],
  "totalEntries": 31
}
```

### 2. Search Locations
```
GET /api/q
```

**Parameters:**
- `q` (required) - Search query for location name

**Example:**
```
GET /api/q?q=nantes
```

**Response:**
```json
{
  "success": true,
  "type": "multiple",
  "locations": [
    {
      "name": "Nantes (Chantenay)",
      "code": "nantes-chantenay-1018"
    },
    {
      "name": "Nantes (Trentemoult)",
      "code": "nantes-trentemoult-1019"
    }
  ],
  "count": 2,
  "query": "nantes"
}
```

## French Month Names

Use these French month names in the `month` parameter:
- `janvier`, `fevrier`, `mars`, `avril`, `mai`, `juin`
- `juillet`, `aout`, `septembre`, `octobre`, `novembre`, `decembre`

## Data Format

- **Dates**: DD/MM/YYYY format (automatically generated)
- **Tides**: `mb1`, `mb2` (low tides), `mh1`, `mh2` (high tides)
- **Times**: 24-hour format
- **Heights**: Meters with "m" suffix
- **Coefficients**: Array of integers (20-120 range)

## CORS

Both endpoints support CORS and include appropriate headers for cross-origin requests.

## Getting Started

```bash
npm install
npm run dev
```

The API will be available at `[[http://localhost:3000/api/](https://maree-api-new.vercel.app/api/data)](https://maree-api-new.vercel.app/api/data)`

## Tech Stack

- Next.js 14
- Axios for HTTP requests  
- Cheerio for HTML parsing

## License

MIT
