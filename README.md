# Bioinformatics: Methods & Applications  
### MICR 4203 / 5203 — Oklahoma State University  
**Instructor:** Dr. Robert L. Burnap  
**Repository:** [Bioinformatics-MICR4203-MICR5203](https://github.com/RobBurnap/Bioinformatics-MICR4203-MICR5203)

---

## 📘 Overview
This repository hosts course materials, Jupyter notebooks, and supporting resources for *Bioinformatics: Methods & Applications*, an upper-division and graduate-level course designed to integrate computational biology, molecular genetics, and systems analysis.

The repository doubles as a **Quarto book**, which organizes all lecture notebooks into thematic modules covering sequence analysis, phylogenetics, genomics, structural bioinformatics, and systems biology.

---

## 🧭 Repository Structure
Bioinformatics-MICR4203-MICR5203/
│
├─ notebooks/
│  ├─ 01_Foundations/
│  ├─ 02_Sequence_Alignment/
│  ├─ 03_Phylogenetics/
│  ├─ 04_Genomics_Annotation/
│  ├─ 05_Gene_Expression/
│  ├─ 06_Structure/
│  ├─ 07_Systems_Biology/
│  ├─ 08_Machine_Learning/
│  ├─ 09_Applications/
│  └─ Resources/
│
├─ datasets/                # Example datasets for exercises
├─ _quarto.yml              # Configuration for the Quarto “book”
├─ index.qmd                # Landing page for Quarto site
├─ .gitignore
└─ README.md                # This file

Each numbered subfolder represents a **module**, roughly corresponding to a lecture or multi-lecture unit.

---

## 🚀 Running Notebooks

### Option 1 — Open in Google Colab
You can launch most notebooks directly in your browser via Google Colab:

1. Navigate to any `.ipynb` file in the repository.  
2. Click **“Open in Colab”** (if available) or paste the GitHub URL into:  
   [https://colab.research.google.com/github](https://colab.research.google.com/github)  
3. Enable access to your Google Drive if the notebook saves results or data.

> 💡 For large data or high-performance tasks, students can instead run notebooks via the OSU Pete HPC system.

---

### Option 2 — Run Locally (Anaconda)
```bash
# Clone this repository
git clone git@github.com:RobBurnap/Bioinformatics-MICR4203-MICR5203.git
cd Bioinformatics-MICR4203-MICR5203

# Create and activate a Python environment
conda create -n bioinfo python=3.11 jupyterlab biopython pandas matplotlib -y
conda activate bioinfo

# Launch JupyterLab
jupyter lab
