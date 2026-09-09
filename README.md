# De novo Genome Assembly and Functional Annotation of ***Limosilactobacillus fermentum***

# Dataset

SRA accession: SRR36082397

The raw sequencing reads are not included in this repository because of
file size. They can be retrieved using the SRA Toolkit.

The analysis uses paired-end FASTQ reads generated from the SRA dataset.


## Pipeline

<img width="1200" height="2000" alt="Gemini_Generated_Image_4la2d34la2d34la2" src="https://github.com/user-attachments/assets/f7786598-399e-4b5d-87f2-36f52875f88b" />

## Step 1 — Download and Convert SRA Data

### Download SRA Data

**Command:**

```bash
prefetch SRR36082397
```

### Convert SRA Data to Paired-End FASTQ

The downloaded SRA file was converted into paired-end FASTQ format using `fasterq-dump`.

**Command:**

```bash
fasterq-dump SRR36082397 -O fastq --split-files
```

This generated the following paired-end FASTQ files:

```text
fastq/
├── SRR36082397_1.fastq
└── SRR36082397_2.fastq
```

---

## Step 2 — Quality Control of Raw Reads

### Tool: FastQC

**FastQC** was used to evaluate the quality of the raw paired-end sequencing reads.

**Command:**

```bash
fastqc fastq/SRR36082397_1.fastq \
       fastq/SRR36082397_2.fastq \
       -o fastqc_reports
```

The FastQC reports were saved in the `fastqc_reports/` directory.
