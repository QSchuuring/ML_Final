# Protein Property Analysis with UniProt, AlphaFold, and DSSP

This repository contains the code and data processing workflow for my final project in the Deep Learning course. I created a custom dataset of human proteins using data from UniProt, obtained their predicted 3D structures from AlphaFold, and extracted secondary structure information using DSSP. The resulting dataset supports both regression and classification tasks using deep learning models.

## Contents

- `Protein_Processing.ipynb`: Jupyter notebook containing the full preprocessing pipeline
- `uniprot_with_secondary.csv`: Final dataset with sequences, properties, and secondary structure annotations
- `uniprotkb.fasta`: Raw FASTA file of human protein sequences from UniProt
- `successful_downloads.csv`, `failed_downloads.csv`: Logs from AlphaFold structure downloads
- `dssp_failures.csv`: Logs of DSSP parsing failures
- `README.md`: Overview and project documentation

## Dataset Construction

### Step 1: Sequence Retrieval
- Human protein sequences were downloaded from [UniProt](https://www.uniprot.org/).
- Biopython was used to parse the FASTA file and extract sequence and accession ID information.

### Step 2: Feature Extraction
- Each sequence's length, molecular weight (MW), and isoelectric point (pI) were calculated using `Bio.SeqUtils.ProtParam.ProteinAnalysis`.

### Step 3: Structural Data
- Corresponding AlphaFold-predicted structures were downloaded using the accession IDs.
- Structures were obtained from the AlphaFold Protein Structure Database: [https://alphafold.ebi.ac.uk](https://alphafold.ebi.ac.uk).

### Step 4: Secondary Structure Assignment
- Biopython’s `PDBParser` was used to load the PDB files.
- DSSP was called via Biopython’s `DSSP` interface, using a manually set environment path to a locally installed `mkdssp` binary (installed via Homebrew on macOS).
- Secondary structure labels were simplified to a 3-class system: H (helix), E (sheet), and C (coil).
- A timeout mechanism was implemented to handle unresponsive or malformed files gracefully.

## Preprocessing Pipeline

All the code is written in Python and structured within a single Jupyter notebook.
- DSSP is invoked using a user-defined environment variable pointing to the local executable.
- Timeout and error handling ensure that the full pipeline runs robustly, even in the presence of incomplete data.

## References

- UniProt Consortium: https://www.uniprot.org
- AlphaFold Protein Structure Database: https://alphafold.ebi.ac.uk
- DSSP (Kabsch & Sander), accessed via Biopython with local installation

