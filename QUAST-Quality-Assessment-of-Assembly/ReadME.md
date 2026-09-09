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
