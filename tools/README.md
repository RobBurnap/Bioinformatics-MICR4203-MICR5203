# Bioinformatics Tools

These are optional utilities, separate from numbered course assignments. They have no assignment number, points, or Canvas submission. Use them when the project calls for the workflow described below.

## Tool catalog

| Tool | Purpose | Order |
|---|---|---:|
| [Advanced Tool 1 — Proteome Library Builder](Advanced_Tool_01_Proteome_Library_Builder.ipynb) | Build a persistent set of local protein FASTAs and a separate BLAST database for each selected taxon. | 1 |
| [Advanced Tool 2 — Taxon-Directed BLAST Search](Advanced_Tool_02_Taxon_Directed_BLAST_Search.ipynb) | Search one protein query against each ready taxon database and export ranked homologs. Requires Advanced Tool 1. | 2 |
| [Protein Alignment Trimming with ClipKIT](Tool_Protein_Alignment_Trimming_with_ClipKIT.ipynb) | Trim an existing multiple-sequence protein alignment before phylogenetic inference. | After alignment |

## Proteome library and taxon-directed BLAST

This is a two-stage, more intensive workflow. The first notebook is the **producer**: it prepares the taxonomy table, downloads protein sequences, and builds the local databases. The second notebook is the **consumer**: it searches those prepared databases. The search does not rebuild the library.

### What the workflow does

1. **Start with a curated taxon list.** The builder reads `Taxon_library_v1.csv` from `BIOINFO4-5203-F26/Databases/proteome_library/`. It uses NCBI Taxonomy IDs where available and can match some records by organism name.
2. **Add taxonomic breadth.** The builder reads GTDB bacterial and archaeal metadata (currently configured for GTDB release R232), adds GTDB lineage and quality fields to matching curated taxa, and samples additional representative genomes to fill underrepresented phyla. The sampling settings are visible in the configuration cell; the current defaults favor isolates and require high completeness with low contamination.
3. **Fetch one protein FASTA per taxon.** Curated taxa are resolved through NCBI Taxonomy and the builder’s assembly fallbacks. GTDB-sampled taxa use the selected representative accession. Downloaded FASTAs are cached.
4. **Build one local protein BLAST database per taxon.** The FASTAs and BLAST indexes are stored separately under `proteomes/` and `blastdbs/`. A manifest records status and errors, so a missing proteome does not halt the entire library.
5. **Search locally, one organism at a time.** The second notebook runs `blastp` against each ready organism database, then applies the E-value, query-coverage, and top-hit settings. Checkpoints let the search resume organism by organism.
6. **Export the evidence.** Each run writes a ranked summary CSV and a FASTA containing the full sequences of selected hits, plus per-organism state and an event log.

The per-taxon design makes it clear which organisms produced hits and allows the tool to retain more than one candidate per organism when `TOP_N` is greater than one. A sequence hit is evidence of similarity; it does not, by itself, establish orthology, function, or a species relationship.

### One-time setup

1. In Google Drive, confirm the course project folder is `BIOINFO4-5203-F26`. The builder and searcher use this location by default. If your project folder has a different name, change `PROJECT_DRIVE` in both notebooks to the same correct path.
2. Confirm that the curated `Taxon_library_v1.csv` is in `Databases/proteome_library/`. Preserve a backup of the source table before making edits.
3. Open [Advanced Tool 1 in Colab](https://colab.research.google.com/github/RobBurnap/Bioinformatics-MICR4203-MICR5203/blob/main/tools/Advanced_Tool_01_Proteome_Library_Builder.ipynb). Choose **File → Save a copy in Drive**. Select a standard CPU runtime and run cells in order.
4. The setup cell mounts Drive, creates the library and cache directories, and installs the Python/NCBI Datasets/BLAST+ dependencies used by the notebook. The first run fetches GTDB metadata and one protein set per selected taxon. This can be slow and can use substantial Drive storage because both FASTAs and database indexes persist.
5. Let the builder finish its status report. Review `Taxon_library_final.csv` and `manifest/library_status.csv`; note any failed taxa. The builder caches completed downloads and databases, so rerunning it should handle missing or new work rather than starting from scratch.
6. Open [Advanced Tool 2 in Colab](https://colab.research.google.com/github/RobBurnap/Bioinformatics-MICR4203-MICR5203/blob/main/tools/Advanced_Tool_02_Taxon_Directed_BLAST_Search.ipynb), save your own Drive copy, and run the setup cells. Confirm it detects the shared library before beginning a search.

Do not run two copies of the builder against the same Drive library at once. The builder writes the shared database; the search notebook reads it. If the library already exists, inspect its status before deciding to rebuild it.

### Running a query

1. Put a **single protein sequence** in FASTA format in `BIOINFO4-5203-F26/Data/NB03_taxon_directed_homologs/queries/`. Create that folder if needed by running the search notebook’s setup cell.
2. In Section 1, set `QUERY_FASTA` to the file’s name. The notebook currently searches the first record if the file has multiple FASTA records, so use one query sequence per run.
3. Set a descriptive `QUERY_NAME` if desired; otherwise it uses the filename. Set a new `RUN_LABEL` for every parameter set you want to compare.
4. Check the search settings:
   - `EVALUE`: BLAST significance threshold. A smaller value is stricter.
   - `MIN_QUERY_COVERAGE`: minimum percentage of the query covered by an alignment. Raising it filters short or partial matches.
   - `TOP_N`: number of candidate proteins retained per organism. Values above one preserve possible paralogs for review.
5. Run all cells. The search records its progress per taxon and can resume from completed checkpoints. To keep a previous parameter run, use a new `RUN_LABEL`.
6. Inspect the results under `Outputs/NB03_taxon_directed_homologs/<QUERY_NAME>/<RUN_LABEL>/`. Review the summary CSV and FASTA together. Validate candidate homologs with alignment, domain, motif, and phylogenetic evidence before making biological claims.

### Shared Drive layout

```text
BIOINFO4-5203-F26/
├── Databases/
│   ├── gtdb/                                  # cached GTDB metadata
│   └── proteome_library/
│       ├── Taxon_library_v1.csv               # curated input
│       ├── Taxon_library_final.csv            # builder output used by search
│       ├── proteomes/<taxid>.faa              # one protein FASTA per taxon
│       ├── blastdbs/<taxid>.*                 # local BLAST+ files per taxon
│       └── manifest/library_status.csv        # ready/error state
├── Data/NB03_taxon_directed_homologs/queries/ # one FASTA query per run
└── Outputs/NB03_taxon_directed_homologs/
    └── <query>/<run_label>/
        ├── *_summary.csv
        ├── *_hits.faa
        ├── state/
        └── events.jsonl
```

### Common problems and checks

- **Builder cannot find the curated CSV:** check the exact Drive path and the filename `Taxon_library_v1.csv`.
- **No BLAST databases found:** run Advanced Tool 1 and confirm that `manifest/library_status.csv` has ready taxa before running the searcher.
- **Query not found:** move the FASTA into the persistent `queries/` folder or set `QUERY_FASTA` to its absolute path.
- **No hits:** distinguish a genuine no-hit result from a failed taxon in the library status. Test a less restrictive E-value or coverage threshold only as a separately labeled run.
- **Repeated parameters overwrite a run:** use a fresh `RUN_LABEL` for each parameter set. The search notebook intentionally keeps results organized by query and run label.
- **A Colab session disconnects:** notebooks and files saved to mounted Drive persist, but temporary runtime state does not. The builder caches completed artifacts; the searcher stores checkpoints in its run folder.

### ClipKIT alignment trimming tool

Use [Protein Alignment Trimming with ClipKIT](Tool_Protein_Alignment_Trimming_with_ClipKIT.ipynb) **after** homolog selection and multiple-sequence alignment, and **before** tree inference. The input must already be a protein multiple-sequence alignment. The tool does not search for homologs or align raw sequences.

In Colab, save a Drive copy, run the setup cell, put an aligned FASTA in the created `alignments/` folder, set `ALIGNMENT_FASTA`, and run all. To compare trimming modes or gap thresholds, change the setting and assign a new `RUN_LABEL`; inspect the retained alignment and reports before using the output for a tree. Trimming changes the columns analyzed and can affect phylogenetic inference; compare settings and report them with the tree.

## External documentation

The builder currently uses GTDB release R232. Check the upstream release page before a future library refresh and record any release change.

- [GTDB R232 data index](https://data.gtdb.ecogenomic.org/releases/release232/232.0/)
- [NCBI Datasets CLI installation](https://www.ncbi.nlm.nih.gov/datasets/docs/v2/command-line-start/)
- [NCBI Datasets genome download guide](https://www.ncbi.nlm.nih.gov/datasets/docs/v2/how-tos/genomes/download-genome/)
- [NCBI BLAST+ documentation](https://blast.ncbi.nlm.nih.gov/doc/blast-help/downloadblastdata.html)


## Learning by changing settings

These tools are optional utilities, not graded assignments. There are no points, required responses, or submission steps. Their instructional purpose is to make the reasoning behind each workflow visible and let you inspect how a small number of settings changes the result. Keep the default for a first run; then change one setting at a time, use a new run label where available, and compare outputs. The parameter notes below explain what to change and what to watch.

### Advanced Tool 1: library design choices

The curated taxon list is the biological starting point. GTDB enrichment and representative sampling add breadth while genome quality filters limit low-quality records. In the configuration cell, TARGET_RICH and TARGET_OTHER set how many representatives are sought per phylum group; SAMPLE_MIN_COMPLETENESS and SAMPLE_MAX_CONTAMINATION set quality cutoffs; PREFER_ISOLATES and ALLOW_MAG_FALLBACK control isolate versus metagenome-assembled genome choices. For a small safe exploration, adjust a representative target or quality cutoff and inspect the Section 6 count and final taxon table. These choices change the size, taxonomic breadth, and quality balance of the database. Change GTDB_RELEASE only when intentionally refreshing the source release, since a release change can alter taxonomy and accessions. Never run two builders against the same library at once.

### Advanced Tool 2: search sensitivity

EVALUE controls the expected chance similarity score: a lower value is stricter and tends to retain fewer, stronger matches; a higher value can admit weaker, more divergent matches. MIN_QUERY_COVERAGE rejects alignments that span too little of the query; raising it can remove short domain-only matches. TOP_N retains this many best hits per organism and can preserve candidate paralogs when set above one. RUN_LABEL names the output folder, so change it for every parameter comparison. Compare the summary table and retained full-length hit FASTA; these settings affect candidate detection, but a BLAST match alone does not establish orthology or function.

### ClipKIT: alignment trimming choices

ClipKIT acts on columns of an alignment, not on the sequence set itself. MODE="smart-gap" lets ClipKIT choose a gap-aware threshold from the alignment; MODE="gappy" uses the user-set GAP_THRESHOLD. In gappy mode, a value such as 0.8 removes columns whose gap fraction is above 80%; increasing the threshold generally retains more columns. Change one setting at a time, use a distinct RUN_LABEL, and compare the retained-site count, column log, and coverage summaries. Trimming can reduce poorly aligned or gap-heavy sites, but cannot repair a bad alignment and can remove useful evolutionary signal. The short questions in the notebook are optional self-checks for interpreting the report; they are not submissions.
