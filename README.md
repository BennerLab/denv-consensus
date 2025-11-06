# Dengue virus analysis pipeline

## Requirements

- pandas
- multiqc
- snakemake
- bcftools
- iqtree
- mafft
- megahit
- minimap2
- samtools

These can be installed via conda with the following commands:

```
conda create -n denv-analysis pandas multiqc snakemake-minimal
conda activate denv-analysis
conda install bcftools iqtree mafft megahit minimap2 samtools
```

## Usage

### Sample sheet

To run the pipeline, a tab-separated file named *sample_sheet.txt* is required. This file must contain the following columns:
- **sample**: arbitrary name for this pair of files, e.g. `isolate_42`
- **r1**: path to first of the paired-end reads, e.g. `reads/XYZ_R1.fastq.gz`
- **r2**: path to the second of the paired-end reads

For example:
```
sample  r1  r2
isolate_42  reads/XYZ_R1.fastq.gz    reads/XYZ_R2.fastq.gz
```

### Executing the pipeline

Ensure that the appropriate conda environment is active.

```
snakemake -j 1 -s denv-assembly.snake
```

The -j parameter specifies the number of simultaneous jobs that can run. This can usually be scaled up to the number of CPU threads available on your machine and will allow the pipeline to finish more quickly.


## Output

The consensus sequences for the supplied samples are the main output of the pipeline and can be found at `consensus/{sample}.fasta`.

A summary report containing information on the individual steps of the pipeline (such as contig assembly and serotype identification) will be generated at `denv_report.html`. This file can be viewed in any web browser.

