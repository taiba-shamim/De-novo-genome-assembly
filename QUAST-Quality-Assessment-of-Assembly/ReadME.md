## Step 5 — Assembly Quality Assessment

### Tool: QUAST

The assembled contigs were evaluated using **QUAST** to assess the quality and continuity of the genome assembly.

### Command

```bash
quast spades_output/contigs.fasta \
-o quast_results

```


### Assembly Statistics

<img width="557" height="248" alt="image" src="https://github.com/user-attachments/assets/eadf6d3b-bda0-4621-a23f-9235da8913e2" />


QUAST generated graphical and statistical summaries of the assembly, including GC content, coverage, cumulative length, and Nx-related statistics.

The results are available in:

```text
quast_results/
```

---
