# rna_seq_slurm
Bash scripts and instructions for submitting RNA-seq alignment jobs to Slurm

## Step 1: Obtain genome reference files from UCSC genome database
First, make a new directory to store the genome reference files on your machine. Download the genome reference and annotation files from the UCSC database into this directory. At the time of writing, human genome 38 appears to be the most updated version. More information about hg38 files can be found at this link: https://hgdownload.soe.ucsc.edu/goldenPath/hg38/bigZips/

We want the genome reference and annotation files.
```
wget ftp://hgdownload.cse.ucsc.edu/goldenPath/hg38/bigZips/hg38.fa.gz
wget ftp://hgdownload.cse.ucsc.edu/goldenPath/hg38/bigZips/genes/hg38.refGene.gtf.gz
```
