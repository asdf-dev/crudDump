# crudDump - CS2 Smoke Lineup Database

## Disclamer
This readme was writting by AI

A community-driven database of Counter-Strike smoke grenade lineups with screenshots and position data for competitive maps.

## 📖 Table of Contents
- [Contributing New Smokes](#contributing-new-smokes)
- [Adding a New Map](#adding-a-new-map)
- [Data Structure](#data-structure)

## Contributing New Smokes

Follow this step-by-step guide to add smoke lineups to the database:

### Create a Feature Branch
```bash
git checkout -b add-smoke-<mapname>-<location>
# Example: git checkout -b add-smoke-mirage-jungle
```

### Capture Screenshots in CS:GO/CS2
Open Counter-Strike and capture two screenshots for your smoke lineup:

**Screenshot 1 - Throw Location:**
- Position yourself where the player should stand
- Make the positioning clear (use map features, corners, walls as reference)
- Take a screenshot showing the exact location

**Screenshot 2 - Crosshair Lineup:**
- From the same position, show where to aim
- Ensure crosshair and reference point are clearly visible
- Take a screenshot of the aim point

**Tip:** Use high resolution and disable unnecessary HUD elements for clearer screenshots.

### Name Your Screenshot Files
Use descriptive names with proper formatting:
```
✅ Good examples:
- ct_smoke_1.png / ct_smoke_2.png
- jungle_lineup.png / jungle_throw.png
- a_stairs_(1).png / a_stairs_(2).png

⚠️ Important:
- Spaces in filenames are okay, but will need %20 encoding in URLs
- Use underscores or hyphens for better compatibility
- Number pairs (1) and (2) for throw location and aim spot
```

### Upload Screenshots
Place your screenshots in the appropriate map folder:
```
maps/<mapname>/<your_screenshot>.png

Example:
maps/mirage/jungle_smoke_1.png
maps/mirage/jungle_smoke_2.png
```

### Update the Map JSON
Edit `maps/<mapname>/map.json` and add your smoke entry:

```json
{
  "name": "Jungle",
  "description": "One-way smoke from T spawn",
  "team": "T",
  "area": "A",
  "jumpThrow": true,
  "throwLocation": "https://raw.githubusercontent.com/asdf-dev/crudDump/refs/heads/main/maps/mirage/jungle_smoke_1.png",
  "aimSpot": "https://raw.githubusercontent.com/asdf-dev/crudDump/refs/heads/main/maps/mirage/jungle_smoke_2.png"
}
```

**Field Descriptions:**
- `name`: Target location name (e.g., "CT", "Stairs", "Window")
- `description`: Optional notes about execution or combo throws
- `team`: `"T"` (Terrorist) or `"CT"` (Counter-Terrorist)
- `area`: Map section - `"A"`, `"B"`, or `"Mid"`
- `jumpThrow`: `true` if requires jump-throw bind, `false` otherwise
- `throwLocation`: GitHub raw URL to throw position screenshot
- `aimSpot`: GitHub raw URL to crosshair lineup screenshot

### Format Image URLs Correctly

**Critical:** Use the correct URL format with proper encoding:

```
Base URL format:
https://raw.githubusercontent.com/asdf-dev/crudDump/refs/heads/main/maps/<mapname>/<filename>

Encoding rules:
- Spaces → %20
- Example: "ct smoke (1).png" → "ct%20smoke%20(1).png"

Full example:
https://raw.githubusercontent.com/asdf-dev/crudDump/refs/heads/main/maps/mirage/ct%20smoke%20(1).png
```

⚠️ **Important:** Always use `refs/heads/main` in URLs, not your feature branch name!

### Test Your JSON
Verify your JSON is valid:
- Check for proper comma placement
- Ensure all quotes are closed
- Validate at [jsonlint.com](https://jsonlint.com/)

### Commit and Create Pull Request
```bash
# Add your changes
git add maps/<mapname>/

# Commit with descriptive message
git commit -m "Add <location> smoke for <mapname>"

# Push to your fork
git push origin add-smoke-<mapname>-<location>

# Create a Pull Request on GitHub
```

## Adding a New Map

To add support for a completely new map:

###  Create Map Directory Structure
```bash
mkdir -p maps/<mapname>
```

###  Initialize Empty Map JSON
Create `maps/<mapname>/map.json` with an empty array:
```json
[]
```

###  Register Map in Base Index
Edit [maps/base.json](maps/base.json) and add your map entry:
```json
{
  "name": "Vertigo",
  "url": "https://raw.githubusercontent.com/asdf-dev/crudDump/refs/heads/main/maps/vertigo/map.json"
}
```

**Note:** Keep the list alphabetically sorted for maintainability.

###  Add Smoke Lineups
Follow the [Contributing New Smokes](#contributing-new-smokes) guide to add smoke data.

## Data Structure

### Repository Layout
```
crudDump/
├── maps/
│   ├── base.json          # Registry of all available maps
│   ├── version.json       # API version tracker
│   ├── mirage/
│   │   ├── map.json       # Smoke lineup data for Mirage
│   │   └── *.png          # Screenshot assets
│   ├── dust2/
│   │   ├── map.json
│   │   └── *.png
│   └── ...
└── baseurl.txt            # Base URL constant
```

### Smoke Entry Schema
```json
{
  "name": "string",           // Target location
  "description": "string",    // Optional execution notes
  "team": "T" | "CT",        // Which team uses this smoke
  "area": "A" | "B" | "Mid", // Map section
  "jumpThrow": boolean,       // Requires jump-throw bind
  "throwLocation": "url",     // Screenshot: where to stand
  "aimSpot": "url"           // Screenshot: where to aim
}
```

##  Supported Maps
- Ancient
- Anubis
- Dust2
- Inferno
- Mirage
- Nuke
- Overpass

##  Contributing Guidelines
- Use descriptive names for smoke locations
- Provide clear, high-quality screenshots
- Test lineups in-game before submitting
- One smoke per commit for easier review
- Follow existing naming conventions in the map folder

##  Links
- [Live Data Registry](https://raw.githubusercontent.com/asdf-dev/crudDump/refs/heads/main/maps/base.json)
- [Submit Issues](https://github.com/asdf-dev/crudDump/issues)

---
Made with 💚 for the CS community
