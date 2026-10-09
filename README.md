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
1. **Mest**, previously identified as a mouse digit-tip regeneration-specific
   gene (Jou et al., 2024), was independently recovered as one of the most significantly
   upregulated genes in this reanalysis (log2FC=5.96, padj≈0) — external validation
   of the pipeline.
2. Axolotl and mouse regeneration fold-changes correlate significantly across
   11,544 shared genes (Spearman rho=0.085, permutation p<0.0001), robust to
   cell-cycle gene exclusion and 1:1 ortholog restriction.
3. This correlation is **not regeneration-specific**: axolotl-human and
   mouse-human correlations are both higher (rho=0.118, 0.141), a pattern more
   consistent with phylogenetic/platform covariates than a shared regeneration
   program (see `results/tables/final_design/specificity_test_summary.csv`).
4. Pathway-level analysis (cell-cycle genes excluded) identifies extracellular
   matrix organization and axon guidance as shared axolotl-mouse processes.

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
