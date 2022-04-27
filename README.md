# bisulfite-sequence-data-analysis-pipeline
### A pipeline to preprocess and analyze bisulfite sequence data.
## STEPS

As a prerequisite, conda (anaconda or miniconda) can be installed. Then the following steps can be run within a [virtual environment](https://uoa-eresearch.github.io/eresearch-cookbook/recipe/2014/11/20/conda/) created using conda.

#### 1) Configure the paths of the software libraries & packages used

The generic way to add paths to the `PATH` variable is as following:
```sh
export PATH=$PATH:/<PATH_TO_PACKAGE_OR_LIBRARY_FROM_ROOT_FOLDER>
```

#### 2) Download the required Sequence Read Archive (SRA) files & convert to FASTQ files (For this installing [sra-tools](https://anaconda.org/bioconda/sra-tools) is required).

Commonly these can be downloaded using Gene Expression Omnibus (GEO) or SRA in NCBI. Refer to [download_sra.pbs](https://github.com/UdithaM/bisulfite-sequence-data-analysis-pipeline/blob/main/download_sra.pbs) which is a sample bash script that can be used for this purpose. This will result in a pair of FASTQ files for each SRA file.

#### 3) Quality control using trim_galore software

After obtaining adapter sequences for both the forward and reverse reads, `trim_galore` which is a wrapper script can be used to automate quality and adapter trimming as well as quality control. 

This software automatically,
- removes base calls with a Phred score of 20 or lower (assuming Sanger encoding)
- removes any signs of the Illumina adapter sequence from the 3' end (AGATCGGAAGAGC)
- remove sequences that got shorter than 20 bp

Refer to [trim_galore.pbs](https://github.com/UdithaM/bisulfite-sequence-data-analysis-pipeline/blob/main/trim_galore.pbs) which is a sample bash script that can be used for this purpose.


## License

MIT

