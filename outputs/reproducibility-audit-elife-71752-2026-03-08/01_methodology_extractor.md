# Stage 2 — Methodology Extractor Report
**Date:** 2026-03-08

## SECTION 1 — CORE CLAIMS

1. Five human DRGs from 5 donors (1 male, 4 female, ages 34–55) yielded 1,837 neuronal nuclei after filtering and reclustering, organized into approximately a dozen transcriptomic classes (H1–H15).
2. Reclustering of 1,837 neuronal nuclei identified a range of about a dozen diverse transcriptomic classes.
3. H10 and H11 together account for approximately 20% of neurons in the dataset.
4. Mouse nonpeptidergic small-diameter neurons account for approximately 40% of sensory neurons (comparative reference).
5. Spatial clustering statistically significant: p ≤ 6.96 × 10⁻⁴², one-tailed Mann–Whitney U-test, n = 803 single positive cells, range 1–40 neighbors.
6. Multigene ISH (NEFH, TAC1, OSMR) labels essentially every cell with minimal coexpression.
7. TMEM100 almost undetectable in human DRG data.
8. S1PR3 not detected in human DRG data.
9. H5 neurons: CALCA and NTRK1 negative, strongly NTRK2 positive.
10. H9 showed only weak similarity to any mouse neuron class (KL divergence).
11. No human class shows appreciable similarity to mouse cLTMRs.

## SECTION 2 — STATISTICAL METHODS

- Software: Seurat v3 in R
- Each sample processed individually, then integrated across 6 preparations
- Non-neuronal nuclei removed; reclustering on 1,837 neuronal cells
- Clustering algorithm, resolution, PCs, normalization NOT STATED
- Spatial clustering: one-tailed Mann–Whitney U-test; range 1–40 neighbors; n=803; p ≤ 6.96×10⁻⁴²
- Cross-species comparison: KL divergence (implementation details not specified)
- Co-clustering: joint human+mouse (method not specified)
- No multiple comparisons correction described
- No explicit alpha threshold stated

## SECTION 3 — DATA PREPROCESSING STEPS

- bcl2fastq v2.17 for basecalling
- Cell Ranger 2 (hDRG1–3) / Cell Ranger 3 (hDRG4–6)
- Reference genome: GRCh38.v25.premRNA
- Seurat v3: individual sample QC (thresholds NOT stated), non-neuronal removal (criteria NOT stated)
- Integration across 6 samples (method NOT specified)
- v2 vs v3 chemistry split; no batch correction described

## SECTION 4 — KEY OUTPUT TARGETS

1. Total neuronal nuclei = 1,837 (prep1=212, prep2=152, prep3=770, prep4=281, prep5=80, prep6=342)
2. ~15 transcriptomic classes (H1–H15)
3. H10+H11 ≈ 20% of 1,837 neurons
4. Spatial clustering: p ≤ 6.96×10⁻⁴² (Mann–Whitney, n=803)
5. KL divergence rankings: H8→Trpm8, H1/H2/H5→c-peptidergic, H9→weak all, H12→proprioceptors
6. Co-clustering alignments: H15–proprioceptors, H14–Aβ, H13–AδLTMRs, H11–NP3, H3/H6–Aδ nociceptors, H10–NP1
7. ISH: NEFH/TAC1/OSMR jointly label all cells, minimal coexpression

## SECTION 5 — AMBIGUITIES AND GAPS

1. Seurat QC thresholds not specified
2. Clustering algorithm, resolution, PCs, normalization not stated
3. Integration method across 6 samples not specified
4. No batch correction for v2 vs v3 chemistry described
5. Non-neuronal removal criteria not specified
6. KL divergence: gene set, distribution construction, directionality not specified
7. Co-clustering: joint method not specified; mouse reference dataset not fully described
8. Same-donor prep3/prep5 handling for pseudo-replication not described
9. No quantitative stopping rule for data collection
10. NeuN antibody catalog number not given
11. Mann–Whitney p-value: whether most conservative across range, and precise null hypothesis, not stated
12. Gene filtering per sample before integration not described
