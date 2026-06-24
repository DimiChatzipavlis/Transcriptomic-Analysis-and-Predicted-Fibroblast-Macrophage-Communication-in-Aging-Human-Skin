# Transcriptomic Analysis and Predicted Fibroblast-Macrophage Communication in Aging Human Skin

A computational (dry-lab) re-analysis of single-cell RNA-seq from young versus aged human skin,
asking how dermal fibroblasts are transcriptionally rewired with age and whether that shift alters
their predicted signalling to tissue-resident macrophages.

**Dataset:** [GSE130973](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE130973) — Solé-Boldo
et al. (2020); 5 male donors, ~15,000 cells. Raw data are downloaded automatically by the notebook.

## Pipeline — `skin_aging_optimised.ipynb`

1. **Preprocessing & annotation** — QC and Scrublet doublet removal, log-normalization, Harmony
   batch integration across donors, Leiden clustering, and canonical-marker cell-type annotation.
2. **Differential expression** — donor-aware pseudobulk with PyDESeq2 (negative-binomial Wald test)
   for the OLD vs YOUNG fibroblast contrast.
3. **Systems inference** — transcription-factor activity (decoupleR · DoRothEA · ULM) and
   cell–cell communication (LIANA consensus).

## Summary of findings

Aged fibroblasts shift from a structural/ECM programme toward an immune-associated one, accompanied
by a predicted remodelling of fibroblast → macrophage communication (loss of homeostatic axes and
emergence of inflammatory ones). These are computational predictions and warrant experimental
validation.

## Running

Open the notebook in Google Colab (or any Jupyter environment) and run it top to bottom —
dependencies are installed in the first cell.

## Next steps toward a publishable study

This notebook is a sound *exploratory, single-dataset* re-analysis; the results are
hypothesis-generating, not confirmatory. Closing the gaps below — roughly in priority order —
would bring the work to paper level.

1. **Independent replication and statistical power (essential).** The contrast rests on
   **2 young vs 3 old donors** — too few for stable pseudobulk dispersion estimates, so the
   200-DEG signature should be treated as provisional. Reproduce it in ≥1 independent skin-aging
   scRNA-seq cohort and report cross-dataset concordance (rank correlation, overlap significance)
   or a formal meta-analysis.
2. **Remove the sex confound.** All donors are male, and skin aging is sex-dimorphic. Add female
   donors and test for shared versus sex-specific aging programmes.
3. **Resolve fibroblast subpopulations.** The pipeline collapses all fibroblasts into a single
   pseudobulk, yet the source dataset's central finding is an age-related *loss of fibroblast
   priming* (subpopulation structure). Subcluster fibroblasts, repeat the DE / TF / communication
   analyses per subtype, and benchmark against the original study.
4. **Tighten the statistical inference.** Apply multiple-testing correction to transcription-factor
   activity (currently called at raw *p* < 0.05 across 429 regulons); replace the set-difference
   "emergent/lost" communication call with a differential cell–cell-communication test that models
   per-donor variability (permutation or mixed-effects); add log-fold-change shrinkage for DEG
   ranking and a sensitivity analysis over clustering resolution, HVG count, and thresholds.
5. **Contextualize the biology.** Add pathway / GSEA enrichment and overlap with curated
   senescence / SASP and dermal-aging signatures, and cross-check the inferred regulators against an
   orthogonal regulon resource (high FOXA1/GATA3 activity in fibroblasts is unexpected and warrants
   scrutiny).
6. **Orthogonal and spatial validation.** Co-expression is not interaction — corroborate the top
   fibroblast → macrophage axes with spatial transcriptomics or protein-level data, and validate the
   cell-type labels against a reference-based annotator.
7. **Reproducibility and release.** Pin an exact software environment, fix stochastic steps for
   determinism, and archive the code and processed objects under a citable DOI.
