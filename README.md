# RNA-seq_Slurm
Bash scripts and instructions for submitting RNA-seq alignment jobs to Slurm

## Prerequisites
Make sure STAR and SRA Toolkit modules are installed on your machine. If they are already installed, load the modules with `module load`. If they are not already installed, download and unzip them.
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

Open genomeassembly.sh in the text editor of your choice and change the -p (--partition) flag to your desired partition. This script runs STAR to assemble the reference genome with the chosen annotation. Make a logs directory and submit your job to Slurm. 
```
mkdir logs
sbatch genomeassembly.sh
```

## Step 2: Obtain RNA-seq reads 
If obtaining RNA-seq reads from a publicly available dataset, go to NIH GEO database at this link: https://www.ncbi.nlm.nih.gov/gds/

Search for the title of your paper under "GEO DataSets".
<img width="1185" alt="image" src="https://github.com/user-attachments/assets/a59effb7-b145-4b7f-8840-56ec4cdcac5b" />
Select your paper, scroll all the way down and click the link to "SRA Run Selector". Click "Accession List" under "Total" to download SRR_Acc_List.txt. This file contains the names of the runs in the dataset, and we will move it from your computer to your machine soon. On the GEO dataset webpage, note the rough size (in bytes) of all of the read files. Make a directory on your machine where the reads will be stored, and be sure there is enough space to store all the reads. 
```
mkdir ~/reads
```

Now make a directory for the scripts to obtain the reads, and download get_ncbi_fastq_TEMPLATE.sh and batch_reads.sh.
```
mkdir ~/reads_obtain
cd ~/reads_obtain
wget ???
wget ???
```
Open get_ncbi_fastq_TEMPLATE.sh in the text editor of your choice and change the -p (--partition) flag to your desired partition. Also change the `cd` directory into the directory you created to store your reads. Copy SRR_Acc_List.txt from your computer into `reads_obtain` using `cp` or `scp`. Make a logs directory and batch submit your jobs to Slurm. 
```
mkdir logs
sbatch batch_reads.sh
```

## Step 3: Align and count reads using STAR
Somewhere on your machine with enough space to store
