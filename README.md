# Cross-Species Comparative Genomics of Regeneration: Axolotl, Mouse, and Human

## Overview
This project investigates whether regeneration-associated gene expression programs
are conserved across species with differing regenerative capacity: axolotl (full
limb regeneration), mouse (digit-tip regeneration only), and human (fingertip
regeneration only, and only in limited circumstances). All analysis uses public,
previously published datasets, reprocessed independently.

## Project History: Design Evolution
This repository documents two analysis phases, kept separate intentionally to
show the project's methodological development:

- **`preliminary_design/`** — an initial three-species gene-overlap approach,
  comparing axolotl single-cell markers, mouse bulk RNA-seq, and human wound
  proteomics. This design was found to produce statistically indistinguishable-
  from-chance overlaps (see Methods) and was superseded.
- **`final_design/`** — the core analysis: a matched regenerating-vs-uninjured
  contrast in axolotl and mouse fibroblasts, correlated genome-wide, with a
  non-regenerative human wound-healing dataset used as a specificity control.
  **This is the project's primary result set.**

## Key Findings (final_design)
1. **Mest**, previously reported as regeneration-specific in the mouse digit tip,
   was reproduced as one of the most significantly upregulated genes (log2FC=5.96,
   padj~0). This uses the same dataset as the original authors, so it is a
   pipeline check, not independent replication.
2. Axolotl and mouse fold-changes correlate modestly but significantly
   (Spearman rho=0.162, n=9,817, permutation p<0.0001) after excluding genes with
   extreme fold-changes (|log2FC|>10, detection artifacts). With all genes
   rho=0.085. Result holds after removing cell-cycle genes (rho=0.152) and at a
   stricter cap of 5 (rho=0.161). The cap was chosen after inspecting the
   scatter plot; all-gene results are reported alongside.
3. This agreement is **not regeneration-specific**: axolotl-human (rho=0.178) and
   mouse-human (rho=0.228) are as high or higher, more consistent with
   evolutionary distance, sequencing technology and a general wound response
   (results/tables/final_design/correlation_fold_change_cap_robustness.csv).
4. Extracellular matrix, collagen and axon-guidance pathways are shared by all
   three species (20 of 22 axolotl-mouse pathways are also significant in
   human), pointing to a general repair response.

## Datasets
| Species | Accession | Used in | Design |
|---|---|---|---|
| Axolotl | GSE106269 (Table S7) | `04_axolotl_scanpy_processing.ipynb`, `07_axolotl_regeneration_specific_de.ipynb` | Both |
| Mouse (bulk) | GSE131078 (Qu et al. 2020) | `05_mouse_deseq2_analysis.ipynb` | Preliminary |
| Mouse (single-cell) | GSE143888 | `08_mouse_scrna_load.ipynb` | Final |
| Human (proteomics) | Schultz et al. 2025, supplementary data | `06_human_proteomics_orthology.ipynb` | Preliminary |
| Human (single-cell) | GSE241132 (Liu et al. 2025) | `09_human_scrna_load.ipynb` | Final |

Raw data is not included in this repository (see `.gitignore`); all datasets
are public and downloadable from the accessions above.

## Repository Structure

notebooks/ Analysis notebooks, numbered in chronological order (00-09)
docs/ Literature and data reconnaissance logs
results/
tables/
final_design/ Primary results - start here
preliminary_design/ Superseded three-species comparison
figures/
final_design/
preliminary_design/
axolotl_qc/ Clustering/QC figures used in both phases


## Key Limitations
- Mouse single-cell data has one biological sample per timepoint (no
  replicates), limiting confidence in exact significance thresholds
  (pseudoreplication).
- Axolotl genes are matched to mouse/human by symbol identity; no curated
  axolotl ortholog database (e.g., BioMart) is currently available.
- Human specificity control uses skin wound tissue, not fingertip tissue,
  due to the absence of a public fingertip single-cell dataset.
- A platform-matched axolotl 10x dataset (to disentangle phylogenetic distance
  from sequencing-platform effects in the specificity test) was sought but is
  not available in reusable form from GSE106269.

## Author
Ghayyas Ahmed
Govt. Post Graduate College Mandian Abbottabad
