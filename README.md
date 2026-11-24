# ACTRIS/EARLINET Level 3 aerosol profiling climatology

R code that produces the ACTRIS/EARLINET Level 3 aerosol profiling climatology from Level 2
lidar data. For each station it computes monthly, seasonal and annual statistics of the aerosol
optical profiles, of the integrated quantities and of the aerosol layers, and writes them as
NetCDF files that follow the ACTRIS conventions.

The code is valid from the 2000–2021 release onwards. The resulting dataset is published on
Zenodo: ACTRIS/EARLINET Level 3 2000–2021 climatological dataset,
[doi:10.57837/actris-ares/5snr-xv73](https://doi.org/10.57837/actris-ares/5snr-xv73).

## Requirements

- R, with the packages `isotone`, `ncdf4`, `radiant.data`, `dplyr` and `tidyr`.
- Tested on Ubuntu MATE 22.04; any system with R should work.

## Input data

The scripts read and write paths relative to the working directory, which is `r_script/`. It
must contain:

| Path | Content |
|---|---|
| `New/<station>/` | Level 2 NetCDF files of the station, from the ACTRIS/EARLINET data portal ([data.actris-ares.eu](https://data.actris-ares.eu)) or its [API](https://api.actris-ares.eu/api/swagger-ui/) |
| `Layers/<station>/` | NetCDF file with the geometrical properties of the aerosol layers of the station, e.g. `pot_geom_2000-01-01_2021-12-31.nc` |
| `station.csv` | Station metadata (included) |
| `Climatol2.log`, `Calipso2.log` | Lists used to select the climatological and CALIPSO measurements (included) |
| `Level3/Profiles/<station>/`, `Level3/Integrated/<station>/`, `Level3/Layers/<station>/` | Output folders, one per station: they must exist before the run |

## Usage

```sh
git clone https://github.com/actris-ares/actris-earlinet-level3-aerosol-profiling-climatology.git
cd actris-earlinet-level3-aerosol-profiling-climatology/r_script
```

Set the release period at the beginning of `Main.R`:

```r
release <- c(2000, 2021)
```

then run it from an R session started in `r_script/`:

```r
source("Main.R")
```

`Main.R` runs all the other scripts in sequence.

## Output

| Folder | Content |
|---|---|
| `Level3/Profiles/<station>/` | Monthly, seasonal and annual profiles of extinction, backscatter, lidar ratio, particle depolarization ratio, AOD and integrated backscatter |
| `Level3/Integrated/<station>/` | Monthly, seasonal and annual statistics of AOD, backscatter, lidar ratio, particle depolarization ratio and PBL height |
| `Level3/Layers/<station>/` | Monthly, seasonal and annual histograms of layer properties (base and top altitude, extinction, lidar ratio, ...) |

Each file includes time bounds, wavelength, statistical descriptors (mean, median, standard
deviation, ...) and references to the source files.

## Documentation

[docs/scripts.md](docs/scripts.md) describes each script: purpose, inputs, outputs and
processing steps.

## Authors

- Lucia Mona: scientific supervision, statistical analysis framework and methodology.
- Fabrizio Marra: R code for the Level 3 products, processing algorithms, statistical workflow
  and NetCDF output.
- Ermann Ripepi: repository setup, integration of the source code and maintenance.

All at Consiglio Nazionale delle Ricerche, Istituto di Metodologie Integrate per l'Osservazione
della Terra (CNR-IMIOT), C.da S. Loja - Zona Industriale, I-85050 Tito Scalo (Potenza), Italy,
within the ACTRIS ARES Data Centre unit.

## Citation

If you use this code, please cite it as described in [`CITATION.cff`](CITATION.cff) (GitHub
shows it under *Cite this repository*). If you use the climatology itself, cite the dataset:
[doi:10.57837/actris-ares/5snr-xv73](https://doi.org/10.57837/actris-ares/5snr-xv73).

## License

[GNU GPL v3.0](LICENSE).
