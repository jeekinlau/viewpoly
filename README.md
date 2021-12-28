# VIEWpoly <img src="https://user-images.githubusercontent.com/7572527/145726577-7b01d48b-ca1d-446b-b9c8-aff8c3c9877b.png" align="right" width="230"/>

`VIEWpoly` is a shiny app and R package for visualizing and exploring results from [polyploid computational tools](https://www.polyploids.org/) using an interactive graphical user interface. The package allows users to directly upload output files from [polymapR](https://CRAN.R-project.org/package=polymapR), [MAPpoly](https://CRAN.R-project.org/package=mappoly) , [polyqtlR](https://CRAN.R-project.org/package=polyqtlR), [QTLpoly](https://CRAN.R-project.org/package=qtlpoly), 
[diaQTL](https://github.com/jendelman/diaQTL) and genomic assembly, variants, annotation and alignment files. VIEWpoly uses [shiny](https://CRAN.R-project.org/package=shiny), [golem](https://CRAN.R-project.org/package=golem), [ggplot2](https://CRAN.R-project.org/package=ggplot2), [plotly](https://CRAN.R-project.org/package=plotly), and [JBrowseR]( https://CRAN.R-project.org/package=JBrowseR) libraries to graphically display the QTL profiles, positions, alleles estimated effects, progeny individuals containing specific haplotypes and their breeding values. It is also possible to access marker dosage and parental phase from the linkage map. If genomic information is available, the corresponding QTL positions are interactively explored using JBrowseR interface, allowing the search for candidate genes. It also provides features to download specific information into comprehensive tables and images for further analysis and presentation.

### Quick Start

You can run `VIEWpoly` locally installing the package and accessing the graphical interface through a web browser:

```{r}
# install.packages("devtools")
devtools::install_github("mmollina/viewpoly")
viewpoly::run_app()
```

The `Input data` tab has options for diverse types of inputs. You can upload directly outputs from:

* [MAPpoly](https://CRAN.R-project.org/package=mappoly)
* [polymapR](https://CRAN.R-project.org/package=polymapR)
* [polyqtlR](https://CRAN.R-project.org/package=polyqtlR)
* [QTLpoly](https://CRAN.R-project.org/package=qtlpoly)
* [diaQTL](https://github.com/jendelman/diaQTL)
* CSV, TSV or TSV.GZ standard formats

To relate the genetic maps and QTL analysis with genomic information, it is also required:

* FASTA reference genome

It is optional to upload also: 

* GFF3 annotation file
* BAM or CRAM alignment file
* VCF file
* bigWig file

### Documentation

Access the [tutorial](https://cristianetaniguti.github.io/viewpoly_vignettes/VIEWpoly_tutorial.html). 

We also presented the app main features in [this video](https://www.youtube.com/embed/yqWX86uT5jM)


