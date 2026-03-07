# ScentMetric - Cologne Clone Database

## Project Structure
- `scentmetric-v4.html` - Main site (React 18 + Babel, single HTML file)
- `db.js` - Fragrance database (loaded via `<script src="db.js">`)
- `CLAUDE.md` - This file (project instructions for Claude Code)

## Database Schema (db.js)
The database is a JS array assigned to `window.__SM_DB`. Each entry:

```json
{
  "id": 1,           // Unique ID (auto-increment)
  "r": 1,            // Rank number
  "og": "Creed Aventus",  // Original fragrance name
  "h": "Creed",      // House/brand
  "p": 445,          // Retail price USD
  "fam": "Fruity Chypre",  // Scent family
  "notes": {
    "t": ["Pineapple", "Bergamot"],  // Top notes
    "m": ["Birch", "Jasmine"],       // Middle notes  
    "b": ["Musk", "Oakmoss"]         // Base notes
  },
  "dupes": [
    {
      "nm": "Armaf CDNIM EDP",  // Clone name
      "br": "Armaf",            // Clone brand
      "pr": 35,                 // Clone price USD
      "sim": 92,                // Similarity score (0-100)
      "perf": 88,               // Performance score (0-100)
      "proj": 85,               // Projection score (0-100)
      "lon": 8,                 // Longevity in hours
      "nt": ["Lemon", "Pineapple", "Birch"],  // Clone notes
      "vd": "Description text",  // Verdict/description
      "src": ["Reddit", "Fragrantica"]  // Source communities
    }
  ]
}
```

## How to Add New Entries

### Add a clone to an existing original:
Find the original by `"id"` in db.js, add to its `"dupes"` array.

### Add a new original + clones:
Append to the end of the array in db.js. Use next available ID.
Set `"r"` equal to `"id"`.

### Score formula:
`overall = sim*0.4 + perf*0.2 + proj*0.2 + lonNorm*0.2`
where `lonNorm = lon<=6 ? (lon/6*70) : (70+((lon-6)/6)*30)`

## Daily Update Task
Search Reddit (r/fragrance, r/fragranceclones), Fragrantica, and YouTube for:
1. New clone releases from ME brands (Lattafa, Armaf, Maison Alhambra, etc.)
2. Community ratings and comparisons
3. New original fragrances that clones target

Add 10 high-quality entries per day. Prioritize:
- Clones with community consensus (multiple sources agree)
- Brands: Lattafa, Armaf, Maison Alhambra, Afnan, Rasasi, Fragrance World, French Avenue, Zimaya, Khadlaj, Swiss Arabian, Nabeel, Sapil, Surrati
- Originals from: Tom Ford, Creed, PdM, MFK, Initio, Kilian, Nishane, Xerjoff, Amouage

## Deployment
- Hosted on Cloudflare Pages
- Git push to main branch auto-deploys
- Both `scentmetric-v4.html` and `db.js` must be in the repo root
