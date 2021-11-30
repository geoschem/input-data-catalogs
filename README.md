# GEOS-Chem Input Data

This repository has input data catalogs for GEOS-Chem. The catalog files are intended for downloading GEOS-Chem input data with the 
[bashdatacatalog](https://github.com/LiamBindle/bashdatacatalog). You can to obtain input data according to
- the GEOS-Chem versions you use (e.g., 13.2 + 13.4)
- the meteorology you use (e.g., MERRA2 2x2.5 + GEOS-FP 0.25x0.3125 NA nested) 
- time spans of your simulation (e.g., 2019-01-01 to 2020-01-01)

## Instructions for users

Create a directory called `MyCatalogs/` in the top-level of your GEOS-Chem input data directory (the directory that has `HEMCO/`, `CHEM_INPUTS/`, etc. ).
This directory is where you will put the catalog files you are actively using.

```console
liam:~$ cd /ExtData  
liam:/ExtData$ mkdir MyCatalogs
```

Next, download the data catalogs for the GEOS-Chem versions you use from here: http://geoschemdata.wustl.edu/ExtData/DataCatalogs/. For example, 
I am going to use 13.2 and 13.4 so I am going to download the catalog files to `MyCatalogs/13.2` and `MyCatalogs/13.4`. Meteorological inputs do not change 
between GEOS-Chem versions so you can put `MeteorologicalInputs.csv` at `MyCatalogs/MeteorologicalInputs.csv`. Here is what `MyCatalogs`/` looks like after
downloading the catalog files.

```console  
liam:/ExtData$ tree MyCatalogs 
MyCatalogs
├── 13.2
│   ├── ChemistryInputs.csv
│   ├── EmissionsInputs.csv
│   └── InitialConditions.csv
├── 13.4
│   ├── ChemistryInputs.csv
│   ├── EmissionsInputs.csv
│   └── InitialConditions.csv
└── MeteorologicalInputs.csv

```

Next, edit `MeteorologicalInputs.csv` so that the meteorological data collections you use are enabled (i.e., set column 3 to `1` for every collection you need,
and set it to `0` for collections you do not use).

Now you can run `bashdatacatalog` commands like
```console
liam:/ExtData$ bashdatacatalog MyCatalogs/**/*.csv list-missing url 2019-01-01 2020-01-01 
```

## Update instructions for the GCST

*When a collection is added/removed* - Make the appropriate changes to the catalog files on the `dev` branch.

*When a new version of GEOS-Chem is released* - Tag `dev` with the new GEOS-Chem version number.
