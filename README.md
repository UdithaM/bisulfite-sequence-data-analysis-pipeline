# bisulfite-sequence-data-analysis-pipeline
### A pipeline to preprocess and analyze bisulfite sequence data.
## STEPS

#### 1) Configure the paths of the software libraries & packages used

The generic way to add paths to the `PATH` variable is as following:
```sh
export PATH=$PATH:/<PATH_TO_PACKAGE_OR_LIBRARY_FROM_ROOT_FOLDER>
```

#### 2) Download the required Sequence Read Archive (SRA) files

Commonly these can be downloaded using Gene Expression Omnibus (GEO) or SRA in NCBI. Refer to [download_sra.pbs](https://github.com/UdithaM/bisulfite-sequence-data-analysis-pipeline/download_sra.pbs) which is a sample bash script that can be used for this purpose.



## License

MIT

