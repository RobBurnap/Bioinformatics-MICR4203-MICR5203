# Bioinformatics: Methods & Applications

## MICR 4203 / 5203 — Oklahoma State University

Instructor: Dr. Robert L. Burnap

This public repository is the distribution home for the course's Colab notebooks and small starter datasets. Canvas links students directly to a specific notebook in Google Colab. Each student then saves a personal copy in Google Drive, reads inputs from their `Data/` folders, and writes results to their `Outputs/` folders.

## Student workflow

```text
Canvas assignment
    → Open the assigned notebook in Colab
    → File → Save a copy in Drive
    → Read supplied/project inputs from Drive/Data
    → Save generated results in Drive/Outputs
    → Select evidence for Drive/Portfolio
```

## Repository structure

```text
Bioinformatics-MICR4203-MICR5203/
├── notebooks/              # Stable student-facing NB00–NB19 notebooks
├── data/                   # Small, public starter datasets and templates
├── canvas/                 # Direct Colab URLs and Canvas button guidance
├── legacy/notebooks/       # Earlier notebooks preserved for reference
├── docs/                   # GitHub Pages launch hub
├── index.qmd               # Editable source for the launch hub
├── _quarto.yml             # Optional Quarto site configuration
└── README.md
```

Student-generated output files are intentionally excluded from this public repository. The matching `Data/`, `Outputs/`, and `Portfolio/` working structure belongs in each student's Google Drive.

## Open the course launch hub

[Bioinformatics Colab Notebook Hub](https://robburnap.github.io/Bioinformatics-MICR4203-MICR5203/)

## Stable notebook identifiers

Notebook identifiers describe analytical stages and do not depend on lecture numbers. This lets lectures move in the calendar without breaking filenames or Canvas links.

- `NB00–NB03`: workspace, sequence foundations, BLASTP, and homolog acquisition
- `NB04–NB07`: pairwise alignment, scoring, MSA, and conservation
- `NB08–NB10`: phylogenetic preparation, inference, and interpretation
- `NB11–NB14`: domains, structure, conservation, and interactions
- `NB15–NB19`: genome assembly, annotation, comparative genomics, transcriptomics, and integration

Production links target a protected `fall-2026` branch. Course development should occur on feature branches and be merged into that branch only after validation.
