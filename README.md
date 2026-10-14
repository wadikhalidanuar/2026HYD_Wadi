# 2026HYD_Wadi · Vibrant Taichung Base Map

Research data and interactive maps for the former Taichung City and the Shuinan Economic and Trade Park, prepared for #HackYourDistrict 2026.

Live site (GitHub Pages): https://wadikhalidanuar.github.io/2026HYD_Wadi/

## Outputs

### Former Taichung City Base Map (`index.html`)

An interactive, high-vibrancy cartographic map built with distinct chromatic palettes, full-color vector basemaps, and planning layers:

- **8 Districts & 214 Villages**: Complete administrative boundaries for Former Taichung City with distinct chromatic palettes for Central, East, South, West, North, Xitun, Nantun, and Beitun.
- **Vibrant Color Palettes**:
  - **Vibrant Chromatic**: Saturated, luminous jewel tones for each of the 8 districts
  - **Emerald & Waterways**: Lush botanical and river basin gradients celebrating Central Park & Green corridors
  - **Sunset Glow**: Warm terracotta, amber, coral and twilight violet palette
  - **Nordic Pastel**: Soft, sophisticated cartographic pastels with high visual clarity
  - **Cyberpunk Neon**: Electrifying neon highlighters tuned for presentation and dark mode
  - **HYD Program**: Sun-yellow old downtown with dynamic blue and teal context zones
  - **Original Deck**: Monochrome workshop deck grey ramp for before/after comparison
- **Multi-Mode Coloring**:
  - By District (8 distinct signature hues)
  - Choropleth by Area (Turbo/Viridis continuous rainbow spectrum by km²)
  - Old Downtown vs Outer Context Hubs
- **Interactive Basemaps**:
  - OpenFreeMap Liberty (Full-color vector tiles)
  - CartoDB Voyager (Vibrant modern cartography)
  - OpenStreetMap Standard
  - ESRI High-Resolution World Satellite Imagery
  - CartoDB Positron & Dark Matter
  - Live saturation and opacity sliders
- **Shuinan Detailed Plan**: Traced from Figure 7-1, georeferenced to OSM road networks with 12 vivid land-use zoning areas (Central Park green space, Cultural & Commercial, Innovation & R&D, Eco-Residential, etc.).
- **2026 Flagship Projects**: Numbered markers, mapped footprints, and status indicators (In Service vs In Progress).
- **Cartographic Elements**: DMS coordinate neatline grid, dynamic scale bar, north compass arrow, and bilingual search.

### Detailed Plan Overlay

`data/raw/Figure_7-1_Detailed_Plan_A3_English_CAD.dxf` is a trace drawn on an A3 sheet in millimetres and has no coordinate reference; its `$LATITUDE` / `$LONGITUDE` header values (37.795, -122.394) are AutoCAD San Francisco defaults. `scripts/georef_plan.py` places it on WGS84 with a similarity transform whose parameters come from fitting the traced blocks to OpenStreetMap road centrelines (`scripts/register_plan.py`):

| Parameter | Value | Basis |
|---|---|---|
| Scale | 12.52 m per drawing mm (about 1:12,500) | Road-network fit; matches the 12.24–12.87 m/mm derived from the zone areas |
| Rotation | 0.4° (almost exactly north-up) | Road-network fit; matches runway 18/36 of the former airport (175°–355°) |
| Translation | (-1927.9, -1848.6) m | Road-network fit (local plane origin 120.654°E, 24.185°N) |

The fit aligns block edges half a street from a road and keeps roads out of the blocks. The median distance from a block edge to the nearest road is 11 m and only 3% of block interiors touch a road, with errors within a few tens of metres. Two independent checks agree: the Green Museumbrary grounds in OpenStreetMap fall within about 55 m of the north end of the traced Central Park, and the OSM footprint of the dome site lines up with the traced Innovation R&D blocks.

Colour patches and zones: Ecological Residential, Cultural and Commercial, Innovation & R&D, Economic & Trade, and Cultural and Educational zones are matched by area against the plan land-use table (each within 7%); park, drainage and civic patches follow standard colour conventions.

### Major Projects on the Map

`scripts/locate_projects.py` places each project from `data/raw/shuinan_major_projects_2026.csv`, matching OpenStreetMap facilities, road junctions, and traced plan blocks:

| # | Project | Latitude | Longitude | Located from |
|---|---|---|---|---|
| 1 | Taichung Green Museumbrary | 24.19295°N | 120.65446°E | OSM way 485125572 (grounds) |
| 2 | Taichung International Exhibition Center | 24.19386°N | 120.65177°E | OSM way 1305878545 (building) |
| 3 | Shuinan Transfer Center | 24.19735°N | 120.65312°E | OSM way 1305878254 (bus station) |
| 4 | Taichung Pop Music and Film Center | 24.18184°N | 120.65766°E | OSM way 485125554 (site) |
| 5 | Taichung Dome Stadium | 24.18016°N | 120.65345°E | OSM ways 1391518117 and 1391518516 (BOT site, 10.6 ha mapped; city gives ~16.35 ha on Innovation R&D Zone 1) |
| 6 | Taichung Central Park | 24.18518°N | 120.65463°E | Largest park patch of the traced plan (53.7 ha) |
| 7 | MRT Green Line, Wenhua Senior High School Station | 24.17150°N | 120.66065°E | OSM node 4428067702 (station) |
| 8 | Parking Supply in the Park | – | – | Park-wide figure, not mapped |

### Shuinan Coordinates

| Place | Latitude | Longitude | Source |
|---|---|---|---|
| Centre of the traced detailed plan | 24.1860°N | 120.6510°E | Fitted model |
| Former Shuinan Airport reference point | 24.1863°N | 120.6540°E | OurAirports (RCLG) |
| Taichung Green Museumbrary (grounds) | 24.1929°N | 120.6545°E | OpenStreetMap |
| Taichung International Exhibition Center | 24.1939°N | 120.6518°E | OpenStreetMap |
| MRT Wenhua Senior High School Station | 24.1715°N | 120.6607°E | OpenStreetMap |

## Road Network and Basemap

- **Road Network**: Covers motorways down to tertiary roads, rail, and metro across the former Taichung City, plus local streets around Shuinan. Licensed under ODbL 1.0 (© OpenStreetMap contributors).
- **Basemap Vector Tiles**: Rendered via OpenFreeMap (`https://tiles.openfreemap.org/styles/liberty`) and MapLibre GL JS, featuring full-color styling and English labels (`name:en`).
- **Tile Fallback**: If vector rendering or WebGL is unavailable, the map gracefully falls back to raster tile layers or renders the standalone vector survey map.
- **Local Preview**: When viewing locally via `file://`, run a local static server:
  ```sh
  python3 -m http.server 8000
  # open http://localhost:8000
  ```

## Publishing to GitHub Pages

1. Open **Settings → Pages** in your GitHub repository (`wadikhalidanuar/2026HYD_Wadi`).
2. Under **Build and deployment → Source**, choose **Deploy from a branch**.
3. Select branch **`main`** and folder **`/ (root)`**, then click **Save**.
4. The site will be live at:
   `https://wadikhalidanuar.github.io/2026HYD_Wadi/`

## Rebuilding

After editing data or templates, rebuild using:
```sh
python3 scripts/build_map.py
```

## Data Inventory

| File | Contents | Source |
|---|---|---|
| `data/raw/former_city_8_districts.geojson` | 8 district boundaries of Former Taichung City | MOI & NLSC Open Government Data License v1.0 |
| `data/raw/former_city_villages.geojson` | 214 village boundaries | MOI & NLSC Open Government Data License v1.0 |
| `data/raw/former_city_villages.csv` | Village attribute table (214 rows) | MOI & NLSC Open Government Data License v1.0 |
| `data/raw/old_downtown_5_districts.geojson` | Old downtown: 5 district boundaries | Subset of former-city file |
| `data/raw/old_downtown_villages.geojson` | Old downtown: 108 village boundaries | Subset of former-city file |
| `data/raw/context_xitun_beitun_districts.geojson` | Xitun and Beitun district boundaries | Subset of former-city file |
| `data/raw/context_xitun_beitun_villages.geojson` | Xitun and Beitun: 81 village boundaries | Subset of former-city file |
| `data/raw/shuinan_zoning_areas_2024.csv` | Zone areas of Shuinan Airport site detailed plan | Urban Development Bureau, Taichung City Government (2024-02-01) |
| `data/raw/shuinan_major_projects_2026.csv` | Status of major projects in the park | Taichung City Government project reports (2025–2026) |
| `data/raw/Figure_7-1_Detailed_Plan_A3_English_CAD.dxf` | Detailed plan CAD reference | A3 sheet units |
| `data/raw/reference_points.csv` | Reference coordinates and sources | OpenStreetMap, Wikipedia, OurAirports |
| `data/derived/shuinan_detailed_plan_traced.geojson` | Detailed plan trace fitted to road network | Generated trace |
| `data/derived/roads_osm.geojson` | Road and rail network | OpenStreetMap, ODbL 1.0 |
| `data/derived/landmarks_osm.geojson` | Named landmarks near the site | OpenStreetMap, ODbL 1.0 |
| `data/derived/project_locations.geojson` | Major project locations with method and source | Generated locations |

### Precision & Cartographic Notes
- **Boundary Simplification**: Boundaries are simplified (~1,800 vertices across 214 villages) for smooth browser rendering. Areas are derived from official attribute records.
- **Coordinate System**: WGS84 latitude and longitude (CRS84 / EPSG:4326).
- **Futai Village**: Futai Village in East District (0.052 km²) lacks polygonal boundary geometry in source cadastral files; it is represented by an equivalent-area circle centered at its label coordinate.
