# De novo Genome Assembly and Functional Annotation of Limosilactobacillus fermentum

# Dataset

SRA accession: SRR36082397

The raw sequencing reads are not included in this repository because of
file size. They can be retrieved using the SRA Toolkit.

The analysis uses paired-end FASTQ reads generated from the SRA dataset.


## Pipeline

Raw reads
    ↓
SRA Toolkit
    ↓
FastQC
    ↓
fastp
    ↓
SPAdes
    ↓
QUAST
    ↓
Prokka
    ↓
IGV
    ↓
KEGG / BlastKOALA
