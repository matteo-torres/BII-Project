# Biodiversity Intactness Index Change in Phoenix, AZ

## About
This study aims to investigate the effects of urban expansion in the Phoenix County subdivision area by analyzing the changes in the Biodiversity Intactness Index (BII) between 2017 and 2020.
- Accessing data with the SpatioTemporal Asset Catalog (STAC)
- Clipping raster data to match the geometry of a shapefile
- Analyzing land cover statistics

## Repository Structure
```bash
bii-project
├── README.md
├── .gitignore
├── bii-phoenix.ipynb
└── data
    └── tl_2020_04_cousub
        ├── tl_2020_04_cousub.cpg
        ├── tl_2020_04_cousub.dbf
        ├── tl_2020_04_cousub.prj
        ├── tl_2020_04_cousub.shp
        ├── tl_2020_04_cousub.shp.ea.iso.xml
        ├── tl_2020_04_cousub.shp.iso.xml
        └── tl_2020_04_cousub.shx
```

## Data
The 2020 TIGER/Line shapefile for Arizona, provided by the US Census Bureau, has been downloaded and saved in the data folder located in the repository. You can access it in a subfolder named "tl_2020_04_cousub" by using the `os` library for a reproducible file path and reading the shapefile with `geopandas`.
```bash
# Create a reproducible file path
fp = os.path.join("data", "tl_2020_04_cousub", "tl_2020_04_cousub.shp")

# Import and read Arizona shapefile
arizona = gpd.read_file(fp)
```

The Biodiversity Intactness Index (BII) dataset is available through the Microsoft Planetary Computer's (MPC) open-source cloud. You can access the catalog using the `pystac_client` library; however, you'll need to use a modifier from the `planetary_computer` library to access the data in the MPC catalog. Once you have obtained access, you can refine your catalog search by specifying a time range (2017-2020), an area of interest (Phoenix, AZ), and the collection name (io-biodiversity).
```bash
# Access MPC catalog
catalog = pystac_client.Client.open("https://planetarycomputer.microsoft.com/api/stac/v1",
                                    modifier = planetary_computer.sign_inplace)
                                    
# Catalog search
search = catalog.search(collections = ["io-biodiversity"],
                        bbox = bbox_of_interest,
                        datetime = time_range)
```
To complete your data collection, you need to gather one item for each year from 2017 to 2020. For each of these items, you will extract the BII raster data, which is located within the data asset. This can be done using the `rioxr` library, allowing you to analyze the biodiversity intactness data effectively.


## References
United States Census Bureau. (2021). 2020 TIGER/Line Shapefiles: County Subdivisions. https://www.census.gov/cgi-bin/geo/shapefiles/index.php?year=2020&layergroup=County+Subdivisions

Microsoft Open Source, Matt McFarland, Rob Emanuele, Dan Morris, & Tom Augspurger. (2022). microsoft/PlanetaryComputer: October 2022 (2022.10.28). Zenodo. https://doi.org/10.5281/zenodo.7261897

## Acknowledgements
This repository was created for a final project related to the course EDS 220: Working with Environmental Datasets.

This course is an academic requirement for the Master of Environmental Data Science (MEDS) program at the Bren School of Environmental Science & Management, University of California, Santa Barbara.