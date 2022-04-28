# bisulfite-sequence-data-analysis-pipeline
### A pipeline to preprocess and analyze bisulfite sequence data.
## STEPS

As a prerequisite, conda (anaconda or miniconda) can be installed. Then the following steps can be run within a [virtual environment](https://uoa-eresearch.github.io/eresearch-cookbook/recipe/2014/11/20/conda/) created using conda.

### 1) Configure the paths of the software libraries & packages used

The generic way to add paths to the `PATH` variable is as following:
```sh
export PATH=$PATH:/<PATH_TO_PACKAGE_OR_LIBRARY_FROM_ROOT_FOLDER>
```

### 2) Download the required Sequence Read Archive (SRA) files & convert to FASTQ files (For this installing [sra-tools](https://anaconda.org/bioconda/sra-tools) is required).

Commonly these can be downloaded using Gene Expression Omnibus (GEO) or SRA in NCBI. Refer to [download_sra.pbs](https://github.com/UdithaM/bisulfite-sequence-data-analysis-pipeline/blob/main/download_sra.pbs) which is a sample bash script that can be used for this purpose. This will result in a pair of FASTQ files for each SRA file.

### 3) Quality control using trim_galore software (For this installing [trim-galore](https://anaconda.org/bioconda/trim-galore) is required).

After obtaining adapter sequences for both the forward and reverse reads, `trim_galore` which is a wrapper script can be used to automate quality and adapter trimming as well as quality control. 

This software automatically,
- removes base calls with a Phred score of 20 or lower (assuming Sanger encoding)
- removes any signs of the Illumina adapter sequence from the 3' end (AGATCGGAAGAGC)
- remove sequences that got shorter than 20 bp

Refer to [trim_galore.pbs](https://github.com/UdithaM/bisulfite-sequence-data-analysis-pipeline/blob/main/trim_galore.pbs) which is a sample bash script that can be used for this purpose.

### 4) Using Bismark to map to the reference genome (For this installing [bismark](https://anaconda.org/bioconda/bismark) & [bowtie2](https://anaconda.org/bioconda/bowtie2) are required).

#### 4.1) Prepare the new reference genome using bismark.

Refer to [prepare_ref.pbs](https://github.com/UdithaM/bisulfite-sequence-data-analysis-pipeline/blob/main/prepare_ref.pbs) which is a sample bash script that can be used for this purpose.

#### 4.2 Mapping reads to reference genome using Bismark

Description of the parameters used:

-q : The query input files (specified as , or are FASTQ files (usually having extension .fg or .fastq). This is the default.

--bowtie2 : Default: ON. Uses Bowtie 2 instead of Bowtie 1. Bismark limits Bowtie 2 to only perform end-to-end alignments, i.e. searches for alignments involving all read characters (also called untrimmed or unclipped alignments). Bismark assumes that raw sequence data is adapter and/or quality trimmed where appropriate. Both small (.bt2) and large (.bt2l) Bowtie 2 indexes are supported.

-p : This is an option to use parallelization in bowtie2

[genome folder] in this example, the path to the genome folder used by Jack is given.

-B : The base name of the .BAM file generated from the Bismark.

--multicore : this option works when -B is not specified. Use this to set the program to run in parallel.
-1: read 1 fastq file
-2: read 2 fastq file


#### NOTE: if you are planning to use bisSNP later, add the --rg_tag to bismark. The read groups will be tagged with some information about the sequecing for later use.

## License

MIT

