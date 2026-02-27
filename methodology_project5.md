# Methodology: Project 5 — Geocoding and Spatial Data Creation in Vancouver

This document contains the detailed step-by-step methodology followed in Project 5.

---

## Task 1: Download and Prepare Data
- Searched the City of Vancouver Open Data Portal for the "Public Trees" dataset
- Filtered by neighbourhood to select the area with the highest tree count and downloaded it as a shapefile named `neighborhood_trees`
- Downloaded the "Parks - Polygon Representation" polygon dataset from the same portal

---

## Task 2: Prepare Data for Geocoding
- Reviewed the street trees metadata to understand field definitions
- Added a new text field called `Address` to the `neighborhood_trees` attribute table
- Used the ArcGIS Field Calculator with a Python expression to concatenate the civic number and street name fields into a single address string: `str(!civic_numb!)+" "+str(!std_street!)`

---

## Task 3: Geocoding a Table of Addresses
- Connected to the UBC PostgreSQL server (`geocode` database) and loaded the `gvrd_roads` layer
- Built a custom address locator (`GVRDaddresses`) using the Create Locator tool, mapping house number ranges, street name, and municipality fields from the GVRD road network
- Used the Address Inspector tool to test the locator against several Vancouver addresses
- Exported `neighborhood_trees` to a standalone table and geocoded it against `GVRDaddresses` using the Geocode Addresses tool with the `Address` field as the single line input
- Reviewed geocoding match scores and inspected unmatched or low-scoring records
- Compared the geocoded output visually against the original coordinate-based `neighborhood_trees` layer

---

## Task 4: Create a Shapefile from Tabular Data
- Connected to the UBC PostgreSQL server (`geocode` database) and loaded the `parktrees` table
- Used Make XY Event Layer to convert the tabular data to a spatial point layer, assigning the correct UTM coordinate columns and specifying NAD 1983 UTM Zone 10N as the coordinate system
- Exported the event layer as a permanent shapefile named `parktrees`
- Added `parks_polygon_representation` and a satellite basemap to the map
- Used the Spatial Join tool to join `parktrees` to `parks_polygon_representation`, retaining park area, name, and ID fields, producing `parks_numtrees` with a tree count per park
- Added a `treedensity` field (double data type) and used Select by Attributes to filter parks greater than or equal to 1 ha
- Calculated tree density (trees per hectare) for the selected parks using Calculate Field
- Symbolized `parks_numtrees` using unclassed graduated colours based on the `treedensity` field
- Produced a final map layout including the neighbourhood boundary, parks symbolized by tree density, geocoded and coordinate-based points, roads, and a satellite basemap

---

*Back to [README](README_project5.md)*
