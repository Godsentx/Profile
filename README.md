Terrain Cross-Section Elevation Analysis

A Python-based workflow for generating and analyzing cross-section elevation profiles using GIS data and Digital Elevation Models (DEMs). This repository integrates GeoPandas, Rasterio, Shapely, Matplotlib, and Google Earth Engine to automate terrain profiling, visualization, and export.

---

Features:

- Load user-defined cross-section lines and paths from shapefiles.
- Generate perpendicular cross-sections at regular intervals along any path.
- Sample elevation values from DEMs (local raster or Google Earth Engine).
- Compute summary statistics (mean, min, max) for each cross-section.
- Export results as shapefiles and CSV files for GIS or further analysis.
- Interactive visualization using geemap and matplotlib.
- Fully reproducible workflow for coastal, hydrological, environmental, and infrastructure studies.

---

Tech Stack:

- Python Libraries: GeoPandas, Pandas, Rasterio, Shapely, Matplotlib, NumPy, geemap, ee
- GIS Data: Shapefiles, DEMs (SRTM or other raster sources)
- Cloud Integration: Google Earth Engine for global DEMs and interactive mapping

---

Installation:

1. Clone the repository:

git clone https://github.com/Godsentx/Profile
cd Profile

2. Create a virtual environment (optional but recommended):

python -m venv venv
source venv/bin/activate   # Linux/macOS
venv\Scripts\activate      # Windows

3. Install required packages:

pip install -r requirements.txt

4. Authenticate Google Earth Engine:

import ee
ee.Authenticate()
ee.Initialize()

---

Usage:

1. Load DEM and Cross-Section Lines

import geopandas as gpd
import rasterio

line = gpd.read_file("path/to/base_line.shp")
path = gpd.read_file("path/to/path.shp")
dem = rasterio.open("path/to/dem.tif")

2. Generate Perpendicular Cross-Sections

from shapely.geometry import LineString
from shapely.affinity import rotate
import numpy as np

# Generate cross-sections at fixed intervals along the path
# See example code in cross_section_generation.py

3. Sample Elevations

# Extract elevation values along each cross-section
# Supports both local raster DEM and GEE DEM

4. Export Results

# Export cross-sections with elevations to shapefile
sections_gdf.to_file("cross_sections_with_elevation.shp")

# Export raw elevation profiles to CSV
profiles_df.to_csv("cross_section_profiles.csv", index=False)

5. Visualize Profiles

import matplotlib.pyplot as plt
import numpy as np

# Plot elevation profiles for inspection
for idx, row in sections_gdf.iterrows():
    plt.plot(np.linspace(0, 1, len(row['elevations'])), row['elevations'])
    plt.title(f"Cross-section {idx}")
    plt.xlabel("Distance along cross-section")
    plt.ylabel("Elevation (m)")
    plt.show()

6. Optional: Interactive Map with GEE

import geemap

m = geemap.Map(center=(6.5, 3.6), zoom=12)
m.addLayer(sections_fc.style(color='red', width=3), {}, "Cross-section Lines")
m

---

Example Output:

Cross-section ID | Mean Elevation (m) | Min Elevation (m) | Max Elevation (m)
-----------------|------------------|-----------------|-----------------
1                | 45.2             | 42.0            | 50.5
2                | 48.7             | 44.1            | 53.2

- Shapefiles include geometry of each cross-section with elevation profiles attached.
- CSV files contain raw elevation points for further analysis.

---

Applications:

- Coastal and riverbank analysis
- Hydrological modeling and flood risk assessment
- Environmental and infrastructure planning
- Terrain visualization and reporting

---

Repository Structure:

terrain-cross-section-analysis/
│
├─ data/                 # Example DEMs and shapefiles
├─ notebooks/            # Jupyter notebooks demonstrating workflow
├─ scripts/              # Python scripts for automation
├─ cross_sections/       # Generated shapefiles and CSV outputs
├─ requirements.txt
└─ README.md

---

Contributing:

Contributions are welcome! Feel free to submit issues or pull requests to improve functionality or add new features.

---

License:

This project is licensed under the MIT License – see the LICENSE file for details.

---

Acknowledgements:

- Google Earth Engine (https://earthengine.google.com/) for global DEM datasets.
- Open-source Python GIS libraries: GeoPandas, Rasterio, Shapely, Matplotlib.

---
