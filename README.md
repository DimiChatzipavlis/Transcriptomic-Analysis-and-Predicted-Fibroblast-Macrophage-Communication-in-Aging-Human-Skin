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
