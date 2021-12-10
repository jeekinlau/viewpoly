---
title: "VIEWpoly: a visualization tool to integrate and explore results of polyploid genetic analysis"
author: "Cristiane Taniguti, Gabriel Gesteira, Jeekin Lau, Guilherme Pereira, David Byrne, Zhao-Bang Zeng, Oscar Riera-Lizarazu and Marcelo Mollinari"
date: '2021-12-10'
output:
  html_document:
    highlight: pygments
    keep_md: yes
    toc: yes
    toc_depth: '3'
    toc_float:
      collapsed: no
  md_document:
    variant: markdown_github
  pdf_document:
    highlight: pygments
    toc: yes
    toc_depth: '2'
  word_document:
    toc: yes
    toc_depth: '2'
linestretch: 1.2
bibliography: biblio.bib
---





# Introduction

`VIEWpoly` is a shiny app and R package for visualizing and exploring results from [polyploid computational tools](https://www.polyploids.org/) using an interactive graphical user interface. The package allows users to directly upload output files from [polymapR](https://cran.r-project.org/web/packages/polymapR/index.html) (@Bourke2018), [MAPpoly](https://cran.r-project.org/web/packages/mappoly/index.html) (@Mollinari2019), [polyqtlR](https://cran.r-project.org/web/packages/polyqtlR/index.html) (@Bourke2021), [QTLpoly](https://cran.r-project.org/web/packages/qtlpoly/index.html) (@Pereira2019), 
[diaQTL](https://github.com/jendelman/diaQTL) (@Amadeu2021) and genomic assembly, variants, annotation and alignment files. VIEWpoly uses [shiny](https://cran.r-project.org/web/packages/shiny/index.html), [golem](https://cran.r-project.org/web/packages/golem/index.html), [ggplot2](https://cran.r-project.org/web/packages/ggplot2/index.html), [plotly](https://cran.r-project.org/web/packages/plotly/index.html), and [JBrowseR](https://cran.r-project.org/web/packages/JBrowseR/index.html) libraries to graphically display the QTL profiles, positions, alleles estimated effects, progeny individuals containing specific haplotypes and their breeding values. It is also possible to access marker dosage and parental phase from the linkage map. If genomic information is available, the corresponding QTL positions are interactively explored using JBrowseR interface, allowing the search for candidate genes. It also provides features to download specific information into comprehensive tables and images for further analysis and presentation.

Check also our [tutorial video](https://www.youtube.com/watch?v=yqWX86uT5jM).

The app is organized into four modules: `Input data`, `VIEWqtl`, `VIEWgenome`, and `VIEWmap`.

# Install and run the app

Use the following code to install and run the app.


```r
devtools::install_github("mmollina/viewpoly")
viewpoly::run_app()
```

Each one of the modules here described can be accessed clicking in the top menu:

<br />

<img src="images/top_navbar.PNG" alt="drawing" width="1000"/>

<br />

# Input data

Use this module to select an example dataset or to upload your files. 

For uploading your dataset:

* Submit files for one linkage map building software or the standard format file in `Upload linkage map`. If you submit files for more than one option just the last one will be considered. Once you submit, the map-related features will be already available, you can access them in the `Map` tab.

* Submit files for one linkage map building software or the standard format file in `Upload linkage map`. If you submit files for more than one option just the last one will be considered. Once you submit, the QTL-related features will be already available, you can access them in the `QTL` tab. If you submit both linkage map and QTL analysis results, the submitted linkage map must be the same one used to perform the QTL analysis.

* Submit genome information files in `Upload Genome Browser files`. The FASTA file is the only one required to access the `Genome` tab features, the others (GFF3, VCF, BAM, WIG) are optional. All uploaded files' genome versions must be the same used to build the genetic map. The features in the `Genome` tab will only be displayed if linkage map information was also submitted through `Upload linkage map` or `Upload VIEWpoly dataset`.

The app will convert the uploaded files from `Upload linkage map` and `Upload QTL analysis` sessions into the VIEWpoly file format. You can download it using the `Download VIEWpoly dataset` session. Therefore, in future access to this app, you need to upload just a single file to access the QTL and Map modules app features for this dataset. VIEWpoly files can be uploaded in the `Upload VIEWpoly dataset`. You can also just load the VIEWpoly object in your R environment (code: `load("my_dataset.RData")`) that VIEWpoly will identify and list it in the `Upload VIEWpoly dataset` session. The VIEWpoly object does not store genome information, these files will need to be uploaded again.

### Available example datasets

The linkage map, QTL analysis results from previous studies on a tetraploid potato mapping population are available together with the package:

* [Tetraploid potato - Atlantic x B1829-5](https://www.nature.com/articles/s41437-021-00416-x)

To save space in the package repository, it contains the entire linkage map and QTL analysis but just a subset of individuals and the genome information (FASTA and GFF3).

<br />

<img src="images/available_datasets.PNG" alt="drawing" width="600"/>

<br />

You can access other example files [here](), which includes also data from a hexaploid sweetpotato mapping population:

* [Hexaploid sweet potato - Beauregard x Tanzania](https://academic.oup.com/genetics/article/215/3/579/5930535)


You can select one of them to explore the software features before uploading your data. By default, the app will display the tetraploid potato dataset. 

### Upload linkage map files

Click in the `+` on the right side of the `Upload linkage map files` box to open the options for uploading the linkage map information. 

<br />

<img src="images/uploads.PNG" alt="drawing" width="600"/>

<br />

You can choose to upload files for one of the three options: `MAPpoly`, `polymapR`, or standard formats.

<br />

#### Upload MAPpoly or polymapR output

Click in one the the `+` inside the box to open the description for the select option.

<br />

<img src="images/map_files.png" alt="drawing" width="500"/>

<br />

Once you open one of them, you can see instructions about how should be the files uploaded into this spot. In the example below, it is expected an RData file containing an R object of class `mappoly.map`. The provided link points to the MAPpoly tutorial, where you can find further information about all the procedures to build a linkage map and to obtain this specific object.

<br />

<img src="images/open_mappoly.png" alt="drawing" width="500"/>

<br />

Click in `Browse...` to search for the file on your computer and load it into the app.

<br />

<img src="images/upload_file.PNG" alt="drawing" width="500"/>

<br />

Wait for the upload be complete and click in the submit button (in this case:`submit MAPpoly`):

<br />

<img src="images/upload_complete.PNG" alt="drawing" width="600"/>

<br />

After clicking submit, if you want to change any of the uploaded files, you must click on the `reset` button before upload new files.

<br />

#### Upload linkage map files with stardard format (.csv, .tsv or tsv.gz)

If you choose to submit the linkage map files in standard formats you can download example files to set the right formats with your data:

<br />

<img src="images/map_standard.PNG" alt="drawing" width="500"/>

<br />

Select which of the example files you want to download: `dosages.tsv`, `genetic_map.tsv`, `phases.tsv`, and click in `Download`.

### Upload QTL analysis files

Upload files for one of the four options: `QTLpoly`, `diaQTL`, `polyqtlR`, or standard formats.

<br />

Pick one of the options and click on the `+` on the right side of the box to open the description of the required files.

<br />

<img src="images/qtl_inputs.PNG" alt="drawing" width="500"/>

<br />

#### Upload QTLpoly, diaQTL or polyqtlR output

From the QTL analysis, at least four files are required. The example code shows the functions the required object comes from. After loading all required files, click on `submit` button:

<br />

<img src="images/qtl_loaded.PNG" alt="drawing" width="500"/>

<br />

#### Upload QTL analysis results with standard format (.csv, .tsv or .tsv.gz)

If you choose to submit the QTL analysis files with standard formats you can download example files to set the right formats with your data:

<br />

<img src="images/qtl_standards.PNG" alt="drawing" width="500"/>

<br />

### Upload Genome Browser files 

Uploading files in this session will open access to the `Genome` tab features. The files are included as tracks into the [JBrowseR](https://gmod.github.io/JBrowseR/) tool. Only the assembly (FASTA) file is required to access the feature, the others are optional.

* Assembly 

You can compress the FASTA file using [bgzip](http://www.htslib.org/doc/bgzip.html) with:


```bash
bgzip NSP306_trifida_chr_v3.fa
```

You must submit also the indexes files generated by [samtools](https://samtools.github.io/). 


```bash
samtools faidx NSP306_trifida_chr_v3.fa.gz
```

After this, you can submit the three files at once in the app:

<br />

<img src="images/submit_assembly.png" alt="drawing" width="1000"/>

<br />

* Annotation 

You may need to sort your annotation file before uploading it. One way of doing it is using [gff3sort](https://github.com/billzt/gff3sort) tool:


```bash
gff3sort.pl --precise --chr_order natural NSP306_trifida_v3.hc.gene_models.gff3 | bgzip > NSP306_trifida_v3.hc.gene_models.sorted.gff3.gz 
```

And generated the indexes with [tabix](http://www.htslib.org/doc/tabix.html):


```bash
tabix -p gff NSP306_trifida_v3.hc.gene_models.sorted.gff3.gz
```

<br />

<img src="images/annotation.png" alt="drawing" width="500"/>

<br />

* Variants

The VCF file should also be tabixed: 


```bash
tabix -p variants.vcf
```

* Alignment

Alignment files BAM should be together with BAI or CSI files, and for CRAM files only CRAI is allowed.

For creating BAI index:


```bash
samtools index *.bam
```

* bigWig

No index files are required.

Check further information in [JBrowse documentation](https://jbrowse.org/jb2/docs/user_guide/).

<br />

### Download VIEWpoly dataset

Once you submitted the linkage map and QTL analysis results, VIEWpoly converts all files to a single R object of class `viewpoly`. It keeps only the information required for building the app graphics for QTL and linkage map analysis. You can set the name of the dataset R object using the box. Avoid using special characters or spaces. Click in `Download` to save as an RData object.

<br />

<img src="images/download_viewpoly.PNG" alt="drawing" width="500"/>

<br />

### Upload VIEWpoly dataset

Once you have a viewpoly object file, you can access VIEWpoly features for this dataset just submitting this single file in the `Upload VIEWpoly dataset` session:

<br />

<img src="images/upload_viewpoly.PNG" alt="drawing" width="500"/>

<br />

You can also load your VIEWpoly dataset in your R environment and it will be listed in this session.


```r
load("viewpoly.RData")
viewpoly::run_app()
```

<br />

<img src="images/choose_one.PNG" alt="drawing" width="500"/>

<br />

If you have more than one VIEWpoly dataset available in your R environment, all them will be listed:

<img src="images/choose_multi.PNG" alt="drawing" width="500"/>

Don't forget to press `submit` after uploading the file or choose the listed dataset. After, you can go back to `Upload Genome Browser files` to upload the genome information for this selected dataset.

<br />

# VIEWqtl: the QTL Browser

If you uploaded the QTL analysis information for any of the software options, you can access the features in the `QTL` tab. If you didn't upload anything, the tetraploid potato analysis example will be displayed.

<br />

### Select linkage groups and phenotypes

You can explore any of the linkage groups or the phenotypes together or separated. Select them using the two upper boxes:

<br />

<img src="images/qtl_select.PNG" alt="drawing" width="500"/>

<br />

### QTL profile

Once you selected the group and phenotypes, the QTL profile curve will be plotted. It shows a measure of statistical significance (that can be different according to software used)(y-axis) of the trait (colors) for each map position (x-axis). The triangles in the bottom part point to the peak of the significance and QTL position. The black line crossing the triangle defines the QTL confidence interval.

If you uploaded data from **QTLpoly** you will see a graphic like this:

<br />

<img src="images/qtl_profile.PNG" alt="drawing" width="700"/>

<br />

If you uploaded data from **diaQTL** you will see a graphic like this:

<br />

<img src="images/qtl_profile_diaQL.PNG" alt="drawing" width="700"/>

<br />

If you uploaded data from **polymapR** you will see a graphic like this:

<br />

<img src="images/qtl_profile_polyqtlR.PNG" alt="drawing" width="700"/>

<br />

You can download this figure and all other figures from VIEWpoly selecting the format in the `file type` field and pressing the `Download` button just on top of each figure.

For further information about this graphics, please check @Pereira2019, @Amadeu2021 and @Bourke2021 tutorials.

<br />

#### Effects

You can drag your mouse cursor to select the triangles at the bottom of the graphic to explore particular QTL effects progeny haplotypes, breeding values and to get the QTL summary table in the next sessions:

<br />

<img src="images/select_qtl.PNG" alt="drawing" width="700"/>

<br />

**WARNING**: If you want to change the linkage group or phenotype evaluated first deselect the triangles (single click any other location of the graphic). **Not doing this will crash the app**.

Click in the `+` in the right corner of the `Effects` session to see the graphics. By default, VIEWpoly displays the `bar` design:

<br />

* Additive (bar)

If you uploaded QTL data from **QTLpoly**, you will see something like this:

<br />

<img src="images/effects_bar.PNG" alt="drawing" width="700"/>

<br />

It displays the additive effect for each of the parent's alleles on the selected QTL positions. Colors emphasize the intensity of the effects.

If you uploaded QTL data from **diaQTL**, you will see something like this:

<br />

<img src="images/effects_bar_diaQTL.PNG" alt="drawing" width="700"/>

<br />

Similarly with QTLpoly, but includes a bayesian confidence interval for the effects.

If you uploaded QTL data from **polymapR**, you will see something like this:

<br />

<img src="images/effects_bar_polyqtlR.PNG" alt="drawing" width="700"/>

<br />

It plots the intensity of the effects across the entire linkage group for the selected QTL phenotype.

<br />

* Additive (circle)

Changing the `Design` to `Additive (circle)` the intensity of the effects is plotted in a circle graphic. The selected QTL from the same linkage group are plotted together in the same graphic. To be possible to compare the effects across different QTL and phenotypes, the values are standardized to be between -1 (center or circle) and 1. The dots colors are more intense close to the extreme values (-1 and 1) and their transparency increase when they are close to 0. 

This design is only available for **QTLpoly** and **diaQTL** software results.

<br />

<img src="images/qtl_circle_diaQTL.PNG" alt="drawing" width="800"/>

<br />

* Alleles combination

Changing the `Design` to `Alleles combination` a heatmap is plotted with the combined alleles (parents alleles x-axis x parents alleles y-axis) sum of additive and digenic effects in the upper diagonal and just the additive in the bottom diagonal. 

This design is only available for **QTLpoly** and **diaQTL** software results. 

If you uploaded QTL data from **QTLpoly**, you will see something like this:

<br />

<img src="images/allele_comb_qtlpoly.PNG" alt="drawing" width="900"/>

<br />

**QTLpoly** only considers additive effects.

If you uploaded QTL data from **diaQTL**, you will see something like this:

<br />

<img src="images/allele_comb_diaQTL.PNG" alt="drawing" width="900"/>


For further information about this graphics, please check @Pereira2019, @Amadeu2021 and @Bourke2021.

<br />

#### Progenies haplotypes

To access this feature, first set the `Design` to `Additive (bar)`. By now, it is only implemented for results coming from **QTLpoly**.

Click on `update available haplotypes` button and after in the right corner of the `Select haplotypes` gray box, a window will open presenting all possible parents alleles for the QTL selected in the QTL profile graphic. You can select any combination of alleles and, after clicking on `submit selected haplotypes`, VIEWpoly will search the individuals in the progeny that have a probability higher than 0.5 of having all the alleles selected.

<br />

<img src="images/haplotype.PNG" alt="drawing" width="700"/>

<br />

For example, here we selected the allele P1.1 and P2.2 in LG 5, position 0 referring to the QTL for trait ST08 (Trait:ST08_LG:5_Pos:0_homolog:P1.1; Trait:ST08_LG:5_Pos:0_homolog:P2.1), P1.2 in LG 5, position 28 referring to the QTL for trait NI08 (Trait:NI08_LG:5_Pos:28_homolog:P1.2) and P2.4 in LG 5, position 26 referring to the QTL for trait FM14 (Trait:FM14_LG:5_Pos:26_homolog:P2.3).

<br />

<img src="images/haplo_selected.PNG" alt="drawing" width="700"/>

<br />

VIEWpoly displays the genotype probability profile for each individual identified with the selected alleles. The QTL position are pointed by dashed vertical lines. If only one linkage group is selected, the graphic will split vertically the probabilities for each possible homolog:

<br />

<img src="images/haplo_split.PNG" alt="drawing" width="700"/>

<br />

In case we include the QTL for trait NS06 in chromosome 1 and try to find also individuals that have the allele P1.1 in this QTL position:

<br />

<img src="images/haplo_stack.PNG" alt="drawing" width="700"/>

<br />

Because two groups must be represented in this case, the graphic design change to a stacked version.

<br />

#### Breeding values

This feature is only available for software **QTLpoly**. Only the effects of the selected QTL in the QTL profile graphic are considered to estimate the breeding values.

<br />

<img src="images/breeding_values.PNG" alt="drawing" width="500"/>

<br />

You can download the tables in VIEWpoly by clicking on the top buttons. CSV, Excel and PDF formats are available. `Copy` will copy the table to your clipboard. 

<br />

#### QTL summary

VIEWpoly also provides a table with some of the main information about the selected QTL. This table also changes according to the software used to evaluate the QTL.

<br />

<img src="images/qtl_summary.PNG" alt="drawing" width="500"/>

<br />

# VIEWgenome: the Genome Browser

This module has the goal to relate the QTL position in the linkage map with the available genomic information. 

<br />

### Select phenotypes and linkage group

The visualization here is made defining a range in the `Map range (cM)` session by chromosome. Therefore, you can select only one chromosome to be visualized at the time. You can also select the phenotypes then the QTL positions and confidence interval are plotted just below the range. The QTL profile graphic will be also available in the `QTL profile` session.

<br />

<img src="images/select_pheno.PNG" alt="drawing" width="500"/>

<br />

### QTL profile

Click on the `+` on the right corner of the `QTL profile` session to access a plotly graphic with the QTL significance profile.  
<br />

<img src="images/qtl_profile_plotly.PNG" alt="drawing" width="700"/>

<br />

### Linkage Map x Physical 

A scatterplot of the genetic versus the physical positions is displayed to highlight the relationship
between the genetic map, the reference genome, the QTL positions and intervals, and the recombination rate along the chromosomes. 

<br />

<img src="images/pos_cm.PNG" alt="drawing" width="700"/>

<br />

### JBrowseR

If you uploaded the genome information in the `Input data` tab, you can click on `Open JBrowseR` to visualize the genome and all the tracks according to the files uploaded:

<br />

<img src="images/genome.PNG" alt="drawing" width="900"/>

<br />

The range in the genome is set from the position of the first marker e to the position of the last marker in the selected linkage map range. 

Changing the range:

<br />

<img src="images/genome2.PNG" alt="drawing" width="900"/>

<br />

You can also explore all the JBrowse features by clicking on the buttons inside the window. 

For example, zoom in:

<br />

<img src="images/zoom.PNG" alt="drawing" width="900"/>

<br />

Access the menu clicking in the upper left corner:

<br />

<img src="images/jbrowser.PNG" alt="drawing" width="900"/>

<br />

For further information about the JBrowseR features, please access [its documentation](https://jbrowse.org/jb2/docs/).

VIEWpoly creates a local server to host the genome files to JBrowseR to be able to access it. Before exiting the app or changing the genome file you must turn off the generated server by clicking on the button `Local server` session. If not, the server will only be off when you close or restart R.

<br />

<img src="images/server.PNG" alt="drawing" width="900"/>

<br />

### Annotation table

If you uploaded the GFF3 file in the `Input data` session, a table will be available with annotation information inside the range selected in the linkage map.

<br />

<img src="images/genes.PNG" alt="drawing" width="900"/>

<br />

# VIEWmap: the Map Browser

This module's goal is to provide tools to explore the linkage map proprieties. The sessions to select the phenotypes and the linkage group and to display the QTL profile are the same already described in the `QTL Browser`

<br />

### Map

In this session, it is plotted the parent's haplotypes and linkage map related to the range selected in the `map range (cM)`. If the reference and alternative alleles information are present in the uploaded linkage map files, the variants are represented with different colors for each nucleotide (A, T, C, and G) or indel (-). If this information is not present, red and white will differentiate the biallelic sites. The dots position and color represent the dosage number.

<br />

<img src="images/map.PNG" alt="drawing" width="900"/>

<br />

#### Parents haplotypes table

The parents haplotypes information used to build the graphic can be download in this session in table format:

<br />

<img src="images/parents_haplotypes.PNG" alt="drawing" width="900"/>

<br />

### Map summary

VIEWpoly also provides a table with the linkage map main characteristics:

<br />

<img src="images/map_table.PNG" alt="drawing" width="900"/>

<br />

And the linkage map draw:

<br />

<img src="images/map_draw.PNG" alt="drawing" width="900"/>

<br />

# Help us to improve

If you find issues using VIEWpoly, write to us in the issues tab in [VIEWpoly github page](https://github.com/mmollina/viewpoly) or through the email: chtaniguti@tamu.edu.

<br />

# References



