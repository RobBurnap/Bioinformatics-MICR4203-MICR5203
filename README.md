# Bioinformatics: Methods & Applications

## MICR 4203 / 5203 — Oklahoma State University

Instructor: Dr. Robert L. Burnap

This public repository distributes the course's current Colab notebooks and small starter datasets. Canvas is the source for assignment instructions and publication status. The numbered notebook filenames match the Canvas assignments that use Colab.

## Student workflow

Canvas assignment → open its Colab notebook → **File → Save a copy in Drive** → use the course Drive folders for inputs and outputs.

## Current Colab assignments

See [the Canvas assignment crosswalk](canvas/assignment_crosswalk.csv) for Canvas IDs, exact Dropbox HTML archive names, notebook filenames, Colab URLs, and publication status.

| Assignment | Notebook |
|---|---|
| 2 — Organizing Your Colab and Google Drive Workspace | [Open in Colab](https://colab.research.google.com/github/RobBurnap/Bioinformatics-MICR4203-MICR5203/blob/main/notebooks/Assignment_02_Organizing_Your_Colab_and_Google_Drive_Workspace.ipynb) |
| 3 — Dot Plots and Pairwise Sequence Alignment | [Open in Colab](https://colab.research.google.com/github/RobBurnap/Bioinformatics-MICR4203-MICR5203/blob/main/notebooks/Assignment_03_Dot_Plots_and_Pairwise_Sequence_Alignment.ipynb) |
| 7 — Python and AI in Colab: Building a FASTA Tool | [Open in Colab](https://colab.research.google.com/github/RobBurnap/Bioinformatics-MICR4203-MICR5203/blob/main/notebooks/Assignment_07_Python_and_AI_in_Colab_Building_a_FASTA_Tool.ipynb) |
| 10 — Clustering and Heatmaps in Colab | [Open in Colab](https://colab.research.google.com/github/RobBurnap/Bioinformatics-MICR4203-MICR5203/blob/main/notebooks/Assignment_10_Clustering_and_Heatmaps_in_Colab.ipynb) |
| 11 — R Gene Expression Analysis and Volcano Plots in Colab | [Open in Colab](https://colab.research.google.com/github/RobBurnap/Bioinformatics-MICR4203-MICR5203/blob/main/notebooks/Assignment_11_R_Gene_Expression_and_Volcano_Plots_in_Colab.ipynb) |

Assignments 10 and 11 are unpublished in Canvas. Their notebook files are public in this repository and can be opened by anyone with the direct link.

## Repository structure

- `notebooks/`: current student-facing Colab notebooks
- `data/`: small, public starter datasets and templates
- `canvas/`: assignment crosswalk and Canvas launch-link guidance
- `legacy/`: retired filenames and historical material preserved for compatibility
- `docs/` and `index.qmd`: public launch hub

## Optional bioinformatics tools

These tools are separate from the numbered assignments and have no assignment points or Canvas submission. The two Advanced Tools form a sequence: build the per-taxon proteome library first, then search it with BLAST. The ClipKIT utility trims an already aligned protein alignment before tree inference.

- [Advanced Tool 1 — Proteome Library Builder](https://colab.research.google.com/github/RobBurnap/Bioinformatics-MICR4203-MICR5203/blob/main/tools/Advanced_Tool_01_Proteome_Library_Builder.ipynb)
- [Advanced Tool 2 — Taxon-Directed BLAST Search](https://colab.research.google.com/github/RobBurnap/Bioinformatics-MICR4203-MICR5203/blob/main/tools/Advanced_Tool_02_Taxon_Directed_BLAST_Search.ipynb)
- [Tool — Protein Alignment Trimming with ClipKIT](https://colab.research.google.com/github/RobBurnap/Bioinformatics-MICR4203-MICR5203/blob/main/tools/Tool_Protein_Alignment_Trimming_with_ClipKIT.ipynb)

See the [Tools guide](tools/README.md) for setup, data layout, parameter guidance, and troubleshooting.

[Open the Bioinformatics Colab Notebook Hub](https://robburnap.github.io/Bioinformatics-MICR4203-MICR5203/)
