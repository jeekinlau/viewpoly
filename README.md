# VIEWpoly

R package to visualize genetic maps and QTL analysis.

### Quick Start

You can run `ViewPoly` locally installing the package and accessing the graphical interface through a web browser:

```{r}
devtools::install_github("mmollina/viewpoly")
viewpoly::run_app()
```

### For developers:

* Deploy package on RStudio running the file viewpoly/app.R

TODO:

* Fix the "Doses" label position (issue when high zoom is applied)
* Generate legend on-the-fly (for different ploidy levels)
* Set slide bar size to the selected LG length - ok
* Get number of available LG from dataset - ok
* Include tab for QTL + genome browsing - ok
* Add marker's positions and chromosome in prepare_map output
* Change app default colors
* Avoid using QTLpoly entire objects inside app