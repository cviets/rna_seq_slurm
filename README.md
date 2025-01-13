# rna_seq_slurm
Bash scripts and instructions for submitting RNA-seq alignment jobs to Slurm

## Prerequisites
Make sure STAR and SRA Toolkit modules are installed on your machine. If they are already installed, load the modules with `module load`. If they are not already installed, download and unzip them, and add the binaries to your .bashrc file.
```
wget https://github.com/alexdobin/STAR/archive/refs/tags/2.7.11b.tar.gz
wget https://ftp-trace.ncbi.nlm.nih.gov/sra/sdk/3.1.1/sratoolkit.3.1.1-centos_linux64.tar.gz
tar xzvf STAR-2.7.11b.tar.gz
tar xzvf sratoolkit.3.1.1-centos_linux64
```
Add the following lines to your .bashrc file.
```
export PATH="$PATH:/work/submit/viets/STAR-2.7.11b/bin/Linux_x86_64_static"
export PATH="$PATH:/work/submit/viets/sratoolkit.3.1.1-centos_linux64/bin"
```

## Step 1: Obtain genome reference files from UCSC genome database
First, make a new directory to store the genome reference files on your machine. Download the genome reference and annotation files from the UCSC database into this directory. At the time of writing, human genome 38 appears to be the most updated version. More information about hg38 files can be found at this link: https://hgdownload.soe.ucsc.edu/goldenPath/hg38/bigZips/

We want to download and unzip the genome reference and annotation files.
```
mkdir hg38_ref
cd hg38_ref

wget ftp://hgdownload.cse.ucsc.edu/goldenPath/hg38/bigZips/hg38.fa.gz
wget ftp://hgdownload.cse.ucsc.edu/goldenPath/hg38/bigZips/genes/hg38.refGene.gtf.gz
tar xzvf hg38.fa
tar xzvf hg38.refGene.gtf
```

Now download genomeassembly.sh to your machine.
```
wget ???
```

Open genomeassembly.sh in the text editor of your choice and change the -p (--partition) flag to your desired partition. Running Make a logs directory and submit your job to Slurm. 
