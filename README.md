# Biodiversity Intactness Index Change in Phoenix, AZ

## About
This study aims to investigate the effects of urban expansion in Phoenix, AZ by analyzing the Biodiversity Intactness Index (BII).
- Accessing data using the SpatioTemporal Asset Catalog (STAC)
- Clipping raster data to the geometry of a shapefile
- Land cover statistics

## Repository Structure
```bash
bii-project
│   README.md
│   bii-phoenix.ipynb
│   .gitignore
│
└── data
    │
    └── tl_2020_04_cousub
        │
        └── tl_2020_04_cousub.shp
```

## Data
The TIGER/Line shapefile for Arizona, provided by the US Census Bureau, has been downloaded and stored in the data folder. It can be accessed within a separate folder named "tl_2020_04_cousub."

The Biodiversity Intactness Index (BII) Time Series, available through Microsoft Planetary Computer, can be accessed in the code. You can access the `io-biodiversity` collection from the Microsoft Planetary Computer STAC catalog.
```bash
catalog = pystac_client.Client.open("https://planetarycomputer.microsoft.com/api/stac/v1", modifier = planetary_computer.sign_inplace)
```

## References
2020 tiger/line® shapefiles: County+subdivisions. United States Census Bureau. (n.d.). https://www.census.gov/cgi-bin/geo/shapefiles/index.php?year=2020&layergroup=County%2BSubdivisions

Microsoft Planetary Computer. Planetary Computer. (n.d.). https://planetarycomputer.microsoft.com/dataset/io-biodiversity

## Acknowledgements
This repository was created as part of a final project for the course EDS 220 - Working with Environmental Datasets.