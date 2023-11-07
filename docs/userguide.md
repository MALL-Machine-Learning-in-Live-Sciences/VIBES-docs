# VIBES User Guide

## Installation

The installation of `VIBES` is done via GitHub. For this you need to
install the `devtools` package via the function `install_github`. In
addition `VIBES` has dependencies via Bioconductor so it will be
necessary to install the associated `BiocManager` package. This will
allow you to install the `phyloseq` package.

``` r
# Installation requires devtools and bioconductor, please use the following commands
if (!requireNamespace("BiocManager"))
    install.packages("BiocManager")
BiocManager::install()
install.packages("devtools")
# Before installing VIBES, you need also to install the dependent package `phyloseq`
BiocManager::install("phyloseq")
# Install VIBES from github
devtools::install_github("DiegoFE94/VIBES")
```

## Usage

Before starting the demonstration, you need to load the following
packages:

``` r
require(phyloseq)
#> Loading required package: phyloseq
library(VIBES)
```

The package works with three types of input data: matrix, dataframe and phyloseq. The following example works with a phyloseq object from the PRJNA208535 cohort. In this case the phyloseq object is made up of the counts of 1657 microbiome profiles.

``` r
data("PRJNA208535")
# Load a pseq with 1657 samples 22 species and 7 taxonomic ranks
print(PRJNA208535)
#> phyloseq-class experiment-level object
#> otu_table()   OTU Table:         [ 6284 taxa and 1657 samples ]
#> sample_data() Sample Data:       [ 1657 samples by 25 sample variables ]
#> tax_table()   Taxonomy Table:    [ 6284 taxa by 7 taxonomic ranks ]
#> refseq()      DNAStringSet:      [ 6284 reference sequences ]
# Note that the otu table is made up of the counts
otu_table(PRJNA208535)[1:5,1:5]
#> OTU Table:          [5 taxa and 5 samples]
#>                      taxa are rows
#>      SRR902006 SRR902881 SRR903842 SRR903941 SRR903945
#> ASV1         0         0         0         0         0
#> ASV2    188890      3623         0         0         0
#> ASV3         0         0         0         0         0
#> ASV4         0         0      3345      1709       590
#> ASV5         0         0         0         0         0
tax_table(PRJNA208535)[1:5,6:7]
#> Taxonomy Table:     [5 taxa by 2 taxonomic ranks]:
#>      Genus           Species              
#> ASV1 "Lactobacillus" "Lactobacillus_iners"
#> ASV2 "Lactobacillus" "Lactobacillus_iners"
#> ASV3 "Lactobacillus" "Lactobacillus_iners"
#> ASV4 "Lactobacillus" "Lactobacillus_iners"
#> ASV5 "Lactobacillus" NA
```

Before running the package, the clinical data is made up of 25 variables, the last six are:

``` r
# Sample data has no info about clusters
sample_data(PRJNA208535)[1:5,20:25]
#>           VAG_ITCH VAG_BURN VAG_DIS MENSTRU1 MENSTRU2 MENSTRU3
#> SRR902006       NA       NA      NA       NA       NA       NA
#> SRR902881        0        0       0       NA       NA       NA
#> SRR903842        0        0       0       NA       NA       NA
#> SRR903941        0        0       0       NA       NA       NA
#> SRR903945        0        0       0       NA       NA       NA
```

The main function of `VIBES` is `get_VIBES`. This function has two parameters:

- object: 16S rRNA data in a phyloseq, matrix or a data frame. For matrix and data frames, samples in rows and species in columns.
- column: only for phyloseq objects. Column number occupied by the taxonomic rank _Species_. Default value is the last column.

``` r
# Compute clusterization
pseq_w_clusters <- get_VIBES(object = PRJNA208535)
#> Remember that the species names must be in the following format: Genus_species
```

`get_VIBES()` returns an object (`pseq_w_clusters`) of the same type as the input, but with 5 new columns.

## Interpreting the results

The object returned by the `get_VIBES()` function contains the probability (ranging from 0 to 1) of membership of each sample to each of the four clusters (`VCS.I`, `VCS.II`, `VCS.III` and `VCS.IV`), as well as a final column (`p_cluster`) with the assigned label.

``` r
# Check sample data of the new object 'pseq_w_clusters'
sample_data(pseq_w_clusters)[1:5,25:30]
#>           MENSTRU3        VCS.I    VCS.II      VCS.III       VCS.IV p_cluster
#> SRR902006       NA 2.883447e-18 0.9998651 3.257710e-06 1.315948e-04    VCS-II
#> SRR902881       NA 7.292814e-24 1.0000000 9.895719e-12 8.154546e-10    VCS-II
#> SRR903842       NA 2.211632e-20 1.0000000 3.602075e-10 1.755376e-08    VCS-II
#> SRR903941       NA 4.992614e-26 1.0000000 1.369296e-10 8.586513e-09    VCS-II
#> SRR903945       NA 3.820220e-24 0.9941218 1.527713e-07 5.878046e-03    VCS-II
```