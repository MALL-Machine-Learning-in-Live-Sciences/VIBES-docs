# VIBES - VagInal Bacterial subtyping using machine learning for Enhanced classification of bacterial vaginosiS

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.10309596.svg)](https://doi.org/10.5281/zenodo.10309596)

The `VIBES` package computes clusters of biological significance from 20
species from vaginal microbiome.

The package works with three types of input data: matrix, dataframe and
phyloseq. In case the provided object is a phyloseq the package
automatically extracts the matrix of interest to execute the rest. In
case the object is a dataframe or a matrix the samples must be in the
rows and the species in the columns.

The 20 species used by the package are as follows, and regardless of the
object passed must be named as such (`Genus_species`):
Aerococcus_christensenii, Campylobacter_ureolyticus, Finegoldia_magna,
Lactobacillus_crispatus, Lactobacillus_gasseri, Porphyromonas_uenonis,
Prevotella_bivia, Prevotella_timonensis, Atopobium_vaginae,
Lactobacillus_iners, Prevotella_amnii, Prevotella_disiens,
Staphylococcus_haemolyticus, Veillonella_montpellierensis,
Alistipes_finegoldii, Gardnerella_vaginalis, Mycoplasma_hominis,
Mobiluncus_mulieris, Prevotella_buccalis and Sneathia_sanguinegens.

## Original data

`VIBES` used five different 16S rRNA cohorts from vaginal environment to find the clusters.

### Discovery cohort

- SRA022855: Vaginal bacterial communities of 396 North American women (Baltimore and Atlanta), between the ages of 12 and 45 (mean age: 30). Women included in the study self-identified as African American (n=104), White (n=98), Hispanic (n=97), and Asian (n=97). [Publication](http://dx.doi.org/10.1073/pnas.1002611107)

### Validation cohorts
 
- SRA051298: Vaginal bacterial communities of 220 North American women (Seattle), between the ages of 18 and 57 (mean age: 29). Women included in the study self-identified as African American (n=75), White (n=97), Asian (n=15), and Others (n=33). [Publication](https://doi.org/10.1371/journal.pone.0037818)
 
- PRJNA208535: Vaginal bacterial communities of 25 North American women (Birmingham) over 10 weeks (1657 16S raw samples on repo.), between the ages of 19 and 45 (mean age: 27). Women included in the study self-identified as African American (n=20), and White (n=5). [Publication](https://doi.org/10.1186/2049-2618-1-29)
 
- PRJNA797778: Vaginal bacterial communities of 39 North American women (Baltimore) over 10 weeks (220 16S raw samples on repo.), between the ages of 19 and 45. Women included in the study self-identified as African American (n=24), White (n=10), Hispanic (n=4), and Asian (n=1). [Publication](https://doi.org/10.1186/s13059-022-02635-9)
 
- PRJNA302078: Vaginal bacterial communities of 65 Chinese women (Beijing) over 3 time points: pretreatment, one week after treatment and one month after treatment with metronidazole (201 16S raw samples on repo.), between the ages of 18 and 53. [Publication](https://doi.org/10.1038/srep26674)


Moreover, we used PRJNA302078 to explore the relationship between our stratification methodology and the response to metronidazole antibiotic.

## Source code for the analyses conducted in the development of VIBES

The source code for the analyses is available [here](https://github.com/MALL-Machine-Learning-in-Live-Sciences/VIBES-analysis)