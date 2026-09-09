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

---

## Step 3 — Read Trimming and Filtering

### Tool: fastp

The raw paired-end reads were processed using **fastp** to remove adapter sequences and low-quality reads before genome assembly.

### Command

```bash
mkdir -p trimmed

```bash
fastp \
-i fastq/SRR36082397_1.fastq \
-I fastq/SRR36082397_2.fastq \
-o trimmed/SRR36082397_1_trimmed.fastq \
-O trimmed/SRR36082397_2_trimmed.fastq \
-h fastp_report.html \
-j fastp_report.json
```

### Output

The processed paired-end reads were saved as:

```text
trimmed/
├── SRR36082397_1_trimmed.fastq
└── SRR36082397_2_trimmed.fastq
```

The **fastp** quality-control reports were generated in HTML and JSON formats:

```text
fastp_report.html
fastp_report.json
```

---

## Step 4 — De novo Genome Assembly

### Tool: SPAdes

The quality-filtered paired-end reads were used for **de novo genome assembly** using **SPAdes**. The assembly was performed without using a reference genome.

### Command

```bash
spades.py \
-1 trimmed/SRR36082397_1_trimmed.fastq \
-2 trimmed/SRR36082397_2_trimmed.fastq \
-o spades_output
```

### Output

SPAdes generated the assembled genome in the `spades_output/` directory.

The main assembly files were:

```text
spades_output/
├── contigs.fasta
└── scaffolds.fasta
```

The primary assembly file used for downstream analysis was:

```text
spades_output/contigs.fasta
```

---

## Step 5 — Assembly Quality Assessment

### Tool: QUAST

The assembled contigs were evaluated using **QUAST** to assess the quality and continuity of the genome assembly.

### Command

```bash
quast spades_output/contigs.fasta \
-o quast_results

```


### Assembly Statistics

| Metric | Result |
|---|---:|
| Number of contigs | 582 |
| N50 | 28,549 bp |
| Largest contig | 105,244 bp |
| Total assembled size | 2,004,667 bp (~2.0 Mb) |

QUAST generated graphical and statistical summaries of the assembly, including GC content, coverage, cumulative length, and Nx-related statistics.

The results are available in:

```text
quast_results/
```

---

## Step 6 — Genome Annotation

### Tool: Prokka

The assembled contigs were annotated using **Prokka** to identify predicted coding sequences and other genomic features.

### Command

```bash
prokka spades_output/contigs.fasta \
--outdir prokka_output \
--prefix weblem6_annotation \
--force
```

Prokka generated annotation files describing the predicted genomic features.

### Main Annotation Outputs

| File | Description |
|---|---|
| `.gff` | Gene coordinates and annotations |
| `.faa` | Predicted protein sequences |
| `.ffn` | Predicted nucleotide coding sequences |
| `.gbk` | GenBank-format annotation |

### Annotation Summary

| Feature | Count |
|---|---:|
| CDS | 1,991 |
| tRNA | 61 |
| tmRNA | 1 |
| Contigs | 582 |
| Genome size | 2,091,153 bp |

The Prokka output is available in:

```text
prokka_output/
```

---

## Step 7 — Genome Feature Visualization

### Tool: Integrative Genomics Viewer (IGV)

The Prokka-generated annotation was visualized using **Integrative Genomics Viewer (IGV)** to inspect the genomic organization and predicted genomic features.

The following files were loaded into IGV:

### Genome

```text
spades_output/contigs.fasta
```

### Annotation Track

```text
prokka_output/weblem6_annotation.gff

```
<img width="1091" height="738" alt="igv-denovo" src="https://github.com/user-attachments/assets/2a85a494-61ce-4efc-b034-1cfcbfd7cf28" />


The visualization was used to inspect:

- Gene locations
- Gene orientation
- Coding regions
- Genomic organization

In the IGV visualization, blue arrows represent genes, and the arrow orientation indicates the genomic strand.

An example gene observed during visualization was:

```text
**pepQ **— Xaa-Pro dipeptidase
```
<img width="730" height="330" alt="image" src="https://github.com/user-attachments/assets/d52c24f1-ba75-440d-95cf-86844b9603bb" />

---

## Step 8 — Functional and Pathway Analysis

### Tool: KEGG / BlastKOALA

The predicted protein sequences generated by Prokka were used as input for functional annotation and pathway analysis.

### Input

```text
prokka_output/weblem6_annotation.faa
```

The protein FASTA file was submitted to **BlastKOALA** for functional annotation and **KEGG** pathway mapping.

### Major Metabolic Pathways Identified

- Glycolysis
- TCA cycle
- Oxidative phosphorylation
- Amino acid biosynthesis

---

## Author

**Taiba Shamim**  

