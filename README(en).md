# NKFCYQ

**NKFCYQ: an interactive web tool for comprehensive multi-omics exploration of liver hepatocellular carcinoma**

Release **v1.0.0** is the archival software release corresponding to the manuscript. It contains the five application modules, their R source files, the locally used processed data objects, and the documentation needed to reproduce the reported application configuration. The release date and repository tag should be recorded when this release is published on GitHub.

## Scope

NKFCYQ is an R/Shiny application for exploratory analysis of liver hepatocellular carcinoma (LIHC) data. The application integrates TCGA-LIHC transcriptomic, miRNA, DNA methylation, somatic mutation, clinical, immune-infiltration, drug-response, and single-cell resources.

The application is intended for hypothesis generation and interactive exploration. Outputs are not a substitute for independent validation, prospective clinical evaluation, or a prespecified statistical analysis plan.

## Repository contents

All five modules are part of this release and should be retained in the public repository:

| Directory | Module | Main functions |
|---|---|---|
| `NKFCYQ1/` | miRNA Analysis | miRNA-gene and gene-miRNA prediction, expression analysis, survival analysis, and ROC analysis |
| `NKFCYQ2/` | miRNA supporting analysis | miRNA expression, correlation, survival, ROC, and related interactive analyses |
| `NKFCYQ3/` | Single-gene Analysis | gene expression, paired analysis, survival, ROC, drug sensitivity, immune infiltration, and single-cell exploration |
| `NKFCYQ4/` | Methylation Analysis | gene-CpG mapping, methylation expression, paired analysis, survival, and ROC analysis |
| `NKFCYQ5/` | Somatic Mutation Analysis | mutation overview, oncoplot, mutation sites, survival, and drug-gene interactions |

The previously omitted `NKFCYQ3/` and `NKFCYQ4/` directories are required components of the tool and must be uploaded together with the other modules. A repository containing only `NKFCYQ1/`, `NKFCYQ2/`, and `NKFCYQ5/` is not a complete release of NKFCYQ.

## System requirements

- Windows, macOS, or Linux
- R 4.4.1 or a compatible later R 4.4.x release
- Sufficient memory and disk space for the TCGA methylation and single-cell objects
- A current web browser

The audited analysis environment used R 4.4.1. The package versions observed in that environment are listed in `docs/REPRODUCIBILITY.md`. The application is not distributed as a hosted service by this repository.

## Installation

Install the CRAN packages used by the application:

```r
install.packages(c(
  "data.table", "dplyr", "DT", "ggplot2", "ggsci", "ggsignif",
  "ggsurvfit", "mlr3", "mlr3learners", "mlr3verse", "mlr3viz",
  "psych", "shiny", "shinydashboard", "shinybusy", "tidyverse"
))
```

Install the Bioconductor packages used by the single-cell and mutation workflows:

```r
if (!requireNamespace("BiocManager", quietly = TRUE)) {
  install.packages("BiocManager")
}
BiocManager::install(c("Seurat", "SingleR", "maftools"))
```

The following resources or packages are required for specific preprocessing workflows and are not guaranteed to be available from the default CRAN installation:

- `oncoPredict` for CTRP v2 drug-response prediction;
- the CIBERSORT implementation and the LM22 signature matrix for immune deconvolution;
- `scRNAtoolVis` for the single-cell dot plot displayed by NKFCYQ3;
- `TCGAmutations` for reproducing the archived mutation-loading step;
- `multiMiR` for miRNA-target retrieval;
- the Human Primary Cell Atlas reference object (`hpca.RData`) for SingleR annotation.

Exact versions for packages that were not preserved in the historical environment are not inferred in this release. They should be recorded in the final environment manifest if the preprocessing workflows are rerun.

## Running the application

Each module is a standalone Shiny application. Open R in the repository root and run one module at a time:

```r
shiny::runApp("NKFCYQ1")
shiny::runApp("NKFCYQ2")
shiny::runApp("NKFCYQ3")
shiny::runApp("NKFCYQ4")
shiny::runApp("NKFCYQ5")
```

Do not run all five modules in the same R session. Each module expects its own relative `data/` directory and source files. `NKFCYQ3` additionally expects the single-cell object and reference resources documented in `docs/REPRODUCIBILITY.md`.

## Data sources

The release uses the following public resources:

- TCGA-LIHC transcriptomic, miRNA, methylation, clinical, survival, and archived somatic-mutation files obtained through UCSC Xena;
- NCBI GEO accession `GSE290925` for single-cell RNA sequencing;
- Cancer Therapeutics Response Portal (CTRP) version 2 for oncoPredict training;
- CIBERSORT LM22 for immune-cell deconvolution;
- Human Primary Cell Atlas for cluster-level SingleR annotation;
- multiMiR-supported databases for miRNA-target queries.

Dataset identifiers, cohort composition, feature counts, processing parameters, and source-access information are documented in `docs/REPRODUCIBILITY.md` and `DATA_AVAILABILITY.md`.

The upstream terms of use and citation requirements of TCGA, UCSC Xena, GEO, CTRP, CIBERSORT/LM22, Human Primary Cell Atlas, and multiMiR remain applicable. The MIT license in this repository applies to original NKFCYQ code only; it does not relicense third-party datasets, reference atlases, software, or database content.

## Reproducibility notes

The public release should include all five source directories. Large files such as the TCGA methylation matrix and `NKFCYQ3/data/HCC_scRNA.rds` may exceed ordinary GitHub limits. They should be tracked with Git LFS or deposited in a persistent repository such as Zenodo, with their permanent DOI, checksums, and exact file names linked from this README. Do not replace the missing modules or data with an e-mail-only request in the release described by the manuscript.

The archived single-cell object contains 148,328 cells and 36,601 genes after the documented `min.features = 200` filter. The archived workflow uses 2,000 variable genes, 50 PCs, PCs 1-30 for neighbors/clustering/UMAP, and clustering resolution 0.05. The exact historical parameters are recorded for transparency, including parameters that should be reconsidered in a future analytical rerun.

## Versioning

The manuscript-associated release is `v1.0.0`. The version is recorded in `VERSION`, `CITATION.cff`, and `docs/REPRODUCIBILITY.md`. When publishing the repository, create the matching immutable Git tag:

```bash
git add README.md LICENSE VERSION CITATION.cff DATA_AVAILABILITY.md docs
git commit -m "Release NKFCYQ v1.0.0"
git tag -a v1.0.0 -m "NKFCYQ manuscript release v1.0.0"
git push origin main
git push origin v1.0.0
```

The tag must identify the exact repository state used for the manuscript. If large data files are hosted through Zenodo or Git LFS, archive the corresponding data revision together with the tag.

## License

Original NKFCYQ source code is released under the MIT License. See `LICENSE`. Third-party data and software remain subject to their own licenses and citation requirements.

## Citation

Please cite the manuscript and the exact software release. Machine-readable citation metadata are provided in `CITATION.cff`.

## Contact

For questions about the manuscript-associated release or access to files that cannot be distributed through GitHub, contact the corresponding author listed in the manuscript. Such contact-based access is a fallback for restricted third-party resources, not a replacement for publishing the complete NKFCYQ source code.
