# CODE-HB NGS Parser

This repository contains a Jupyter Notebook used for parsing and mutation calling of sequencing reads analyzed in the CODE-HB study.


## File

- `NGS_parser_CODE-HB.ipynb` — Jupyter Notebook containing the parsing and mutation-calling workflow.

## Requirements

The notebook requires Python 3 and the following packages:

```bash
pip install biopython pandas
```

## Input

The notebook expects:

- a sequencing-read file in FASTA format
- a reference sequence in FASTA or GenBank format

The input filenames and analysis settings can be changed in the **User settings** cell near the beginning of the notebook.

Example:

```python
READS_FASTA = Path("reads.fasta")
REFERENCE_FILE = Path("reference.fasta")
OUTPUT_DIR = Path("output")
OUTPUT_PREFIX = "sample"
```

## Analysis workflow

The notebook performs the following steps:

1. Loads the reference sequence.
2. Reads and orients sequencing reads relative to the reference.
3. Collapses identical reads and counts their occurrences.
4. Filters reads by sequence length and minimum occurrence count.
5. Aligns retained unique reads to the reference.
6. Calls nucleotide substitutions, insertions, and deletions.
7. Optionally annotates single-nucleotide substitutions at the amino-acid level.
8. Generates summary tables and saves the results as CSV files.

## Output

The notebook produces the following files:

- `*_unique_reads.csv` — unique sequences, occurrence counts, and sequence lengths
- `*_mutant_sequences.csv` — mutation set associated with each retained unique sequence
- `*_mutation_calls.csv` — individual mutation calls for each sequence
- `*_mutation_summary.csv` — summarized occurrence count for each mutation

Nucleotide positions are reported using 1-based reference coordinates.
