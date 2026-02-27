# Project 5: Geocoding and Spatial Data Creation in Vancouver

[Github Repo](https://github.com/AgnessChisale/geocoding_and_spatial_data)

## Overview
This project focuses on converting non-spatial data into geospatial datasets using ArcGIS Pro. Street tree addresses from a Vancouver neighbourhood were geocoded using a custom address locator built from a regional road network. Park tree coordinates were converted from tabular data into a spatial layer, and tree density was calculated per park across the City of Vancouver. Results were visualized on a final map showing geocoded trees, park tree density, and road infrastructure.

---

## Objectives
- Download and prepare open data from the City of Vancouver Open Data Portal
- Build a custom address locator from a road network dataset
- Geocode a table of street tree addresses and evaluate match quality
- Convert tabular coordinate data into a spatial point layer
- Calculate tree density by park using spatial joins and field calculations

---

## Data Sources & Tools

**Data**
| Layer | Description | Source |
|-------|-------------|--------|
| `neighborhood_trees` | Street trees for a single Vancouver neighbourhood | [City of Vancouver Open Data Portal](https://opendata.vancouver.ca) |
| `parks_polygon_representation` | Park boundaries in Vancouver (polygon) | [City of Vancouver Open Data Portal](https://opendata.vancouver.ca) |
| `gvrd_roads` | Road network for the Greater Vancouver Regional District | UBC PostgreSQL Server (`geocode` database) |
| `parktrees` | Tabular dataset of trees in Vancouver parks with coordinates | UBC PostgreSQL Server (`geocode` database) |

**Tools**
| Tool | Purpose |
|------|---------|
| ArcGIS Pro | Geocoding, spatial joins, field calculations, mapping |
| City of Vancouver Open Data Portal | Downloading street tree and parks data |
| UBC PostgreSQL Server | Accessing road network and park tree data |

---

## Methods
Street tree data was downloaded for the neighbourhood with the highest tree count and an Address field was created by concatenating civic number and street name. A custom address locator was built from the GVRD road network and used to geocode the neighbourhood tree addresses. Match scores were reviewed to assess geocoding quality. Park tree data was loaded from the PostgreSQL server as a table with UTM coordinates and converted to a spatial point layer. A spatial join linked park trees to park polygons, and tree density (trees per hectare) was calculated for all parks over 1 ha in size.

📄 *For a detailed breakdown of the methodology, [click here](methodology.md)*

---

## Outputs

- `geocoding_map.pdf` — Map showing the neighbourhood, parks symbolized by tree density, geocoded and coordinate-created points, roads, and a satellite basemap

---

## Key Findings
- Geocoded addresses showed varying match scores, reflecting inconsistencies in address formatting in the source dataset
- Coordinate-based points and geocoded points showed spatial differences, illustrating the limitations of address-based location
- Tree density varied considerably across Vancouver parks, with some smaller parks having disproportionately high densities

---

## Skills Learned
- Downloading and filtering open data from a municipal open data portal
- Concatenating fields using Python expressions in ArcGIS Field Calculator
- Building a custom address locator from a road network
- Geocoding a table of addresses and evaluating match quality
- Converting tabular coordinate data (XY) into a spatial point layer
- Performing spatial joins to associate point counts with polygon features
- Calculating tree density using Select by Attributes and Calculate Field
- Symbolizing continuous data using unclassed graduated colours
