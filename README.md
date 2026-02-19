<img src="https://geoschem.github.io/img/GEOS-Chem_Logo_Light_Background.png" height="60%" width="60%" alt="GEOS-Chem Logo">

<p>
  <a href="https://github.com/geoschem/geos-chem/blob/main/LICENSE.txt"><img src="https://img.shields.io/badge/License-MIT-blue.svg"></a>
</p>

# GEOS-Chem Input Data

This repository has input data catalogs for GEOS-Chem. The catalog files are intended for downloading GEOS-Chem input data with the [bashdatacatalog](https://github.com/geoschem/bashdatacatalog). You can to obtain input data according to
- the GEOS-Chem versions you use (e.g., 13.2 + 13.4)
- the meteorology you use (e.g., MERRA2 2x2.5 + GEOS-FP 0.25x0.3125 NA nested)
- time spans of your simulation (e.g., 2019-01-01 to 2020-01-01)

## Instructions for users

Navigate to the top-level of your GEOS-Chem input data directory (the directory that has `HEMCO/`, `CHEM_INPUTS/`, etc. ). This directory is where you will put the catalog files you are actively using.

Clone this repository from GitHub:

```console
$ git clone https://github.com/geoschem/input-data-catalogs
$ cd input-data-catalogs
```
The main branch will contain the input data catalogs corresponding to the most recent GEOS-Chem release.  If you wish to obtain input data catalogs for an older GEOS-Chem version, follow these steps.

```console
$ git checkout tags/X.Y.Z    # X.Y.Z is the GEOS-Chem version number
$ git branch version_X.Y.Z
$ git checkout version_X.Y.Z
```

This is what `input-data-catalogs` should look like after you have followed the above steps:

```console
$ tree input-data-catalogs
input-data-catalogs/
├── ChemistryInputs.csv
├── EmissionsInputs.csv
├── InitialConditions.csv
├── MeteorologicalInputs.csv
└── README.md
```

Next, edit `MeteorologicalInputs.csv` so that the meteorological data collections you use are enabled (i.e., set column 3 to `1` for every collection you need,
and set it to `0` for collections you do not use).

Now you can run `bashdatacatalog` commands like
```console
$ bashdatacatalog MyCatalogs/**/*.csv list-missing url 2019-01-01 2020-01-01
```

**NOTE**: You should always run `bashdatacatalog` from the top-level of input data repository (i.e., `/ExtData` in my case).

## Instructions for the GCST

1. Make the appropriate changes to the catalog files on the `dev` branch.
2. Create a PR to the `main` branch and ask another GCST member to approve it.
3. Merge `dev` into `main` after the PR has been approved.
