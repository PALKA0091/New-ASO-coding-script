ASO Gapmer Design Pipeline This repository contains an R-based pipeline for designing antisense oligonucleotide (ASO) gapmers against a human target gene (default example: CerS2 / ENSG00000143418). It generates candidate ASO target sites (14–20 nt), annotates them with sequence/structure/off-target and safety features, filters by design criteria, and selects a spatially diverse set of candidates across the transcript. What the pipeline does: Given a human Ensembl gene ID, the workflow:

Builds (once) and loads a TxDb annotation database from Ensembl BioMart.
Extracts the gene’s pre-mRNA/genomic gene region sequence from GRCh38.
Generates all k-mers (k = 14–20) across the target region and annotates: genomic coordinates (start/end, strand)
repeats within the target transcript
population SNP positions/frequencies (Ensembl variation fields)
conservation of candidate sites in mouse ortholog
Predicts structural accessibility and binding energetics using ViennaRNA:
accessibility via RNAplfold
ASO self-folding via RNAfold
duplex formation via RNAduplex
Computes off-target burden across the full human “transcriptome” sequence set:
perfect matches (0 mismatches)
near matches (exactly 1 mismatch)
Designs a gapmer architecture mask (LNA flanks + DNA gap) based on oligo length.
Estimates acute neurotoxicity risk using a published sequence-feature score.
Applies filters to retain high-quality candidates.
Clusters candidates by genomic position and samples 1 per cluster to ensure coverage across the gene.
Output: a table (nucleobase_select) of prioritized ASO candidates.

Requirements for running this R-script: R / Bioconductor packages: BiocManager, GenomicFeatures, txdbmaker, biomaRt, AnnotationDbi, BSgenome.Hsapiens.NCBI.GRCh38, GenomeInfoDbData, Biostrings, tidyverse, cluster

External software dependency: ViennaRNA You must install ViennaRNA (tested with 2.7.2) and ensure the binaries are available on your PATH: RNAplfold RNAfold RNAduplex
