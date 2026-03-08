# Stage 4 — Synthesis Agent Report
**Date:** 2026-03-08
**Analysts:** A (Faithful Replication), B (Robustness Check), C (Assumption Auditor)
**Analyst Scores:** A=2/5, B=3/5, C=2/5

---

## SECTION 1 — CONSENSUS FINDINGS

All three analysts agreed on the following points without exception:

**Cell counts are exact.** The combined matrix of 1,837 neuronal nuclei and the per-preparation breakdown (212/152/770/281/80/342) were verified independently by all three analysts and match the paper exactly. Gene dimensionality (58,188 genes per matrix) likewise confirmed. This is the single most robustly reproducible finding.

**TMEM100 is near-absent.** All three analysts independently verified: <0.5% of cells (A: <0.5%; B: 0.35%; C: <0.5%), supporting the paper's claim. Robust across all QC configurations (0.33–0.39%).

**S1PR3 is not truly "not detected."** All three analysts found S1PR3 expressed in a small but non-zero fraction of cells across multiple preparations. A: ~6.6% in prep1; B: 1.77% post-filtering; C: ~40–60 cells total (~2–3%). The paper's categorical claim of non-detection is directly contradicted by raw data.

**ISH triplex genes are broadly expressed.** NEFH, TAC1, OSMR confirmed present and heterogeneously expressed. Analyst B quantified: 95.2% of filtered cells express ≥1 probe.

**Spatial coordinate data absent from GEO.** All three identified that MWU p ≤ 6.96×10⁻⁴² cannot be reproduced — ISH tissue XY coordinates not deposited.

**Mouse reference data absent.** Cross-species KL divergence and co-clustering claims are entirely untestable from deposited data.

**Clustering parameters undisclosed.** QC thresholds, HVG count, PC count, resolution parameter, and integration method all absent. No analyst could reproduce cluster assignments without assuming defaults.

**v2/v3 chemistry batch effect is a critical unaddressed confound.** All three flagged the split between Cell Ranger v2 + 10x v2 (preparations 1–3) and Cell Ranger v3 + 10x v3 (preparations 4–6) with no described correction.

**Pseudo-replication unaddressed.** Preparations 3 and 5 from the same individual: 850/1,837 cells (46.3%). Not acknowledged statistically.

---

## SECTION 2 — DIVERGENCES

**Divergence 1: S1PR3 prevalence estimate.**
A: ~6.6% in prep1. B: 1.77% post-filtering. C: ~2–3% overall. Explanation: Analysts A and C worked from pre-filter raw matrices; Analyst B applied QC filtering removing ~143 cells. Not substantively different — all agree paper's claim is wrong.

**Divergence 2: Optimal cluster number.**
Analyst B executed silhouette analysis → k=12 optimal. Analysts A and C could not execute clustering. Mild divergence from paper's stated 15; "approximately a dozen" is not inconsistent with k=12.

**Divergence 3: Severity of batch effect.**
Analyst B: chi² = 586.9, p = 3.2×10⁻¹¹⁶; three clusters 100% chemistry-pure → "critical." Analyst C: "moderate-high" (no quantification). Analyst A: minor mention. Analyst B's quantification is authoritative.

**Divergence 4: H10+H11 ~20% claim.**
Analyst B computed two-smallest clusters = 4.5% (range 1.2–7.5% across alternatives) vs. paper's ~20%. Analysts A and C could not compute. Gap likely reflects label-mapping uncertainty (which clusters are H10/H11), not definitive contradiction — but large enough to be a concern.

**Divergence 5: Overall score.**
A=2/5, B=3/5, C=2/5. Analyst B's greater computational capacity allowed verification of ISH coverage and clustering stability, warranting slightly higher credit.

---

## SECTION 3 — SCORECARD

| Dimension | Analyst Average | Adjusted Score |
|---|---|---|
| Numerical Reproducibility | 2.67 | **3** |
| Methodological Clarity | 1.33 | **2** |
| Robustness | 2.00 | **2** |
| Statistical Validity | 2.00 | **2** |
| Data Transparency | 3.00 | **3** |
| **Overall** | **2.20** | **2.4** |

**Numerical Reproducibility (3):** Cell counts, gene dimensionality, and TMEM100 reproduce exactly. S1PR3 "not detected" fails. Cluster-level statistics unverifiable. Spatial p-value and KL divergence unverifiable.

**Methodological Clarity (2):** QC thresholds, HVG count, PC count, resolution, normalization method, integration algorithm, KL pseudocount, ortholog mapping, co-clustering procedure all absent. Paper communicates its biology; fails to communicate its computation.

**Robustness (2):** Mean ARI = 0.547 across perturbations. Three clusters 100% chemistry-pure. KL rankings internally stable (rho ≥ 0.936) but cross-species comparisons untestable. Core descriptive claims maximally robust; cluster-level and cross-species claims fragile.

**Statistical Validity (2):** Pseudo-replication unaddressed (46.3% cells from one donor). No multiple comparisons correction described. No uncertainty quantification on KL divergence. Batch confound not corrected. Single male donor (n=152 cells) insufficient for sex-independent population claims.

**Data Transparency (3):** Raw count matrices fully deposited and exactly match paper claims. Metadata present. Spatial coordinates, mouse reference, and author code absent. QC-filtered vs. raw matrix status ambiguous.

---

## SECTION 4 — FAILURE MODE ANALYSIS

**Methodological Clarity → 4 requires:**
- State the complete Seurat parameter chain: min/max genes per cell, max MT%, UMI floor, HVG count, HVG method (vst vs normalized dispersion), PC count, clustering algorithm (Louvain/Leiden), resolution parameter
- For multi-sample integration: exact method (CCA, RPCA, Harmony, scVI) and hyperparameters
- For KL divergence: pseudocount, gene set, directionality, ortholog mapping source and version
- Deposit analysis code (R or Python scripts) in GEO or linked public repository

**Robustness → 4 requires:**
- Report cluster composition by chemistry; demonstrate claimed transcriptomic classes are not reducible to technical batch variation
- Sensitivity analysis comparing pre- and post-integration cluster assignments
- Address pseudo-replication: mixed-effects model with donor as random effect, or sensitivity analysis excluding one same-donor preparation
- Supplementary ARI figures across parameter ranges (PC count, HVG count, resolution)

**Statistical Validity → 4 requires:**
- Apply multiple comparisons correction (or justify its omission) for cluster marker analysis
- Power analysis or explicit limitation acknowledgment for the single male donor
- Bootstrap confidence intervals or permutation tests for KL divergence rankings
- Address spatial autocorrelation in the MWU spatial test

**Data Transparency → 4 requires:**
- Deposit ISH tissue section XY coordinates used for spatial clustering analysis
- Cite mouse reference dataset with accession number, version, and preprocessing steps
- Clarify in GEO record whether deposited matrices are pre- or post-QC filtered, and if post-QC, state thresholds applied

---

## SECTION 5 — FINAL VERDICT

### PARTIALLY REPRODUCIBLE

The paper's foundational data claims — 1,837 neuronal nuclei across six preparations, per-preparation cell counts, 58,188 genes per matrix, and TMEM100 near-absence — reproduce exactly and without ambiguity across all three independent analyses. The broad expression of NEFH, TAC1, and OSMR across essentially all cells is quantitatively confirmed (95.2% coverage, Analyst B). These are genuine, verifiable findings. However, the core analytical outputs that constitute the paper's scientific contribution cannot be independently reproduced: clustering parameters are entirely undisclosed, rendering the 15 transcriptomic class assignments unverifiable and subject to ARI instability (mean 0.547 across perturbations); three clusters identified by Analyst B are 100% chemistry-pure (chi² p = 3.2×10⁻¹¹⁶), raising the possibility that a subset of claimed biological classes are technical artifacts of an unaddressed batch effect; the spatial clustering p-value and KL divergence rankings depend on data not deposited in GEO; and the paper's explicit claim that S1PR3 is "not detected" is directly and consistently contradicted by raw count data across all three independent analyses (~40–60 cells expressing S1PR3 across multiple preparations). The verdict of PARTIALLY REPRODUCIBLE rather than NOT REPRODUCIBLE is supported by the fact that the biological direction of major findings — NTRK2-high/CALCA-low populations, OSMR heterogeneity, rare versus common transcriptomic subtypes, ~12-15 classes — is visible and consistent in the raw data; the paper fails not because its biology is wrong, but because its methods are underspecified to a degree that makes exact reproduction impossible and renders several secondary claims unverifiable or contradicted.
