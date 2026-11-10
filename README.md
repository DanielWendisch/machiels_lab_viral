# machiels_lab_viral

Single-cell RNA-seq and surface-protein (BD Rhapsody, AbSeq) analysis of a mouse viral-infection time course, with lung and bronchoalveolar lavage (BAL) samples from two experiments. The focus is on alveolar macrophage responses (including Ms4a3-lineage tracing), differential expression, module scores, and compositional analysis. Written in R (Seurat, Quarto).

![flowchart](viral_data_analysis_flowchart.png)

> **Status: archived analysis log (2023–2024).** Raw data and rendered reports are not included, so the notebooks will not run end-to-end without the original data.

## Pipeline (in order)

| Step | Files |
|---|---|
| 1. Read counts, build Seurat objects | `counts_to_seurat.R`, `read_in_empty_and_nonempty_protein_counts.R`, `dataset_QC_setup_chunk_exp*_{lung,bal}.R` |
| 2. Protein (ADT) normalisation | `antibody_derived_tags_transformation.R`, `case_study_dsb_adt_normalization.qmd` |
| 3. Quality control | `experiment_1_qc.qmd`, `QC_dashboard_layout.qmd`, `seurat_obj_qc_layout.qmd` |
| 4. Integration | `experiment_1_intergration.qmd`, `batch_integration.R`, `case_study_experiment_1_2_intergration.qmd` |
| 5. Metadata and sex/sample demultiplexing | `add_meta_data.R`, `sex_determination_case_study.qmd`, `case_study_DeSeq2_exp1_sex_demultiplex.qmd` |
| 6. Differential expression and dashboards | `DeSeq2_d60_all_alv_mac.qmd`, `exp1_deg_dashboard.qmd`, `exp1_wilcoxon_heatmaps.qmd`, `child_deg_dashboard.qmd` |
| 7. Case studies | `case_study_module_scores.qmd`, `case_study_protein_analysis.qmd`, `compositional_analysis.qmd`, `case_study_adjustment_of_Ms4a3_sorting_by_gabbr2.qmd` |
| 8. Bootstrap fold-change analysis | `bootstrap_2.qmd`, `diff_diff_analysis/`, Shiny app in `boostrap_fc_fc/` |
| 9. Reports | `2023-12-28_*_end_of_year_report.qmd`, `2024-03-*.qmd` |

## Expected directory layout

Scripts use paths relative to the project root, with raw data two levels up:

```
<parent>/
├── raw_data/machiels_lab/viral/   # BD Rhapsody outputs (not included)
└── <projects>/machiels_lab_viral/ # this repository
```

Intermediate objects are written to `intermediate_data/` and results to `output/` (both git-ignored). `boostrap_fc_fc/bootstrap_mean_tbl.rds` is the small summary table used by the Shiny app.

## Requirements

R with Seurat, tidyverse, tidyseurat, DESeq2, dsb, and Quarto for rendering. No lockfile was kept for this project.
