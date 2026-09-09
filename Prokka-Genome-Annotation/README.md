# Genome Annotation — Prokka

## Overview

This folder contains the results of **prokaryotic genome annotation** performed using **Prokka** on the de novo assembled genome of *Limosilactobacillus fermentum*.

The assembled contigs generated using SPAdes were used as the input for Prokka. The annotation workflow identified predicted coding sequences and RNA-associated genomic features and generated standard genome annotation files for downstream visualization and functional analysis.

---

## Input

The Prokka annotation was performed using the assembled contigs:

```text
spades_output/contigs.fasta
```

## Command

```bash
prokka spades_output/contigs.fasta \
--outdir prokka_output \
--prefix weblem6_annotation \
--force

```

| Parameter                     | Purpose                                        |
| ----------------------------- | ---------------------------------------------- |
| `spades_output/contigs.fasta` | Input assembled contigs                        |
| `--outdir`                    | Specifies the output directory                 |
| `--prefix`                    | Specifies the prefix for generated files       |
| `--force`                     | Allows existing output files to be overwritten |


## Output 

| File type | Description                                    |
| --------- | ---------------------------------------------- |
| `.gff`    | Genomic coordinates and functional annotations |
| `.faa`    | Predicted protein sequences                    |
| `.ffn`    | Predicted nucleotide coding sequences          |
| `.gbk`    | GenBank-format genome annotation               |
| `.txt`    | Annotation summary                             |


The main annotation files are generated with the prefix:

```text
weblem6_annotation

```

