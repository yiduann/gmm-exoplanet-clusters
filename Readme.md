# Cluster classification tables for exoplanet populations

This repository contains the data products associated with the paper

[Duann et al., 2026, A&A, published]

The data provide cluster classification results for an observational
exoplanet sample and for a synthetic planet population mapped into the
observational cluster space using a Gaussian Mixture Model (GMM)
framework.

---

## Files

### GMM_cluster_obs.csv

Cluster classifications for the observational exoplanet sample selected
from the NASA Exoplanet Archive.

Each row corresponds to one planet. The table includes the assigned
cluster label derived from the unsupervised GMM analysis, together with
relevant quality flags.

### Pebb_Acc_SP_mapped.csv

Mapped cluster classifications for the pebble accreted synthetic planet 
population (Johansen et al. 2019).

Each row corresponds to one synthetic planet. The table includes the
observational cluster label assigned via probabilistic mapping, as well
as a confidence metric quantifying the robustness of the assignment.

---

## Key columns

### GMM_cluster_obs.csv

- `pl_type`  
  The definition and usage of this categorical label are described in
  Section 2.1 (Z-score Normalization and Outlier Filtering) of the paper.

- `GMM_cluster_final`  
  Final cluster assignment derived from the GMM analysis.  
  The labels correspond to the physically interpreted cluster categories
  defined in this work:  
  A1 (Hot Giants; HG), A2 (Warm Jupiter Desert; WJD),  
  B (Low-Mass Giants; LMG), C (Very Massive Gas Giants; VMGG).  
  Cluster D is retained for completeness but is not included in the
  physical analysis.

- `first_gmm_max_probs`  
  Maximum posterior probability of the first-stage GMM cluster
  assignment, quantifying the confidence of the primary classification.

- `GMM_2nd_cluster`  
  Second-most probable first-stage GMM cluster for a given planet,
  corresponding to the alternative cluster with the next highest
  posterior probability.

- `GMM_2nd_prob`  
  Posterior probability associated with `GMM_2nd_cluster`.

- `Mass_Ratio_q`  
  Planet-to-star mass ratio, defined as  
  q = M_p / M_s,  
  where M_p is the planetary mass and M_s is the stellar mass.

- `a_over_Rs`  
  Scaled semi-major axis, defined as  
  a / R_s,  
  where a is the orbital semi-major axis and R_s is the stellar radius.

- `Hill_Radius_AU`  
  Hill radius of the planet, expressed in astronomical units (AU), defined
  as  
  R_Hill = a * (M_p / (3 * M_s))^(1/3).

- `v_esc_over_v_orb`  
  Ratio of the planetary escape velocity to the orbital velocity, defined
  as  
  v_esc / v_orb = sqrt(2 * G * M_p / R_p) / sqrt(G * M_s / a).

- `Safronov_Number`  
  Safronov number, defined as  
  Theta = 0.5 * (v_esc / v_orb)^2 = (a / R_p) * (M_p / M_s).

- `log_g_p_cgs`  
  Logarithm of the planetary surface gravity in cgs units, defined as  
  log g_p = log(G M_p / R_p^2),  
  where g_p is expressed in cm s^-2.

### Pebb_Acc_SP_mapped.csv

- `rrp`  
  Initial orbital distance from the host star at embryo placement, in meters (m).

- `rrpla`  
  Orbital distance after formation (i.e. at the end of the formation stage), in meters (m).
  `rrpla_AU`is in astronomical units (AU).

- `tt0`  
  Embryo formation time in seconds (s). Larger values correspond to later formation.
  `tt0_Myr` is in Myr.  

- `mmpla`  
  Core mass in kilograms (kg).

- `mmice`  
  Ice mass in kilograms (kg).

- `mmgas`  
  Gas-envelope mass in kilograms (kg).

- `Mp`  
  Total planetary mass in kilograms (kg), defined as  
  `Mp = mmpla + mmgas`
  `Mp_earth` is in Earth-mass units.
  `Mp_jup` is in Jupiter-mass units.

- `Mp_Ms_ratio_q`  
  Planet-to-star mass ratio, Mp_Ms_ratio_q = Mp / M_sun, M_sun = 1.989e30 kg.

- `transit_prob_rrpla`  
  Transit probability computed using `rrpla_AU`.  
  The method is described in Appendix C.2 (Mass-Radius Relation and Transit Probability).

- `rrpla_AU_migrated`  
  Semi-major axis after late migration, in AU.  
  The late migration prescription is described in Appendix C.1 (Close-in Migration).

- `transit_prob_rrpla_migrated`  
  Transit probability computed using `rrpla_AU_migrated`.  
  The method is described in Appendix C.2.

- `Rp_m`  
  Planetary radius in metres (m), inferred from the same mass–radius relation (Appendix C.2).
  `Rp_earth` is in Earth-radius units, and `Rp_jup` is in Jupiter-radius units.

- `gp_cgs`  
  Planetary surface gravity in cgs units (cm s\(^{-2}\)), computed as  
  \[
  g_{\mathrm{p}} = \frac{G\,Mp}{Rp_m^2},
  \]
  where \(G\) is the gravitational constant.  
  The stored value `gp_cgs` is \(g_{\mathrm{p}}\) expressed in cgs units (cm s\(^{-2}\)).

- `G1`  
  Gas availability parameter, computed as defined in Section 3 (Methodology).

- `gas_frac`  
  Gas mass fraction, defined as: mmgas / (mmpla + mmgas).

- `IceRock`  
  Ice–rock mass ratio, defined as: mmice / (mmpla - mmice).

- `cluster_map`  
  Mapped observational cluster label assigned to each synthetic planet (e.g. A1, A2, B, C, D), following the mapping procedure described in the paper.

- `pred3D_conf_margin`  
  Confidence margin of the mapping assignment, defined as the difference
  between the log posterior probabilities of the most likely and
  second-most likely clusters. Larger values indicate more decisive
  (higher-confidence) assignments.

  In the released dataset, values of `pred3D_conf_margin` span a wide
  range and can be interpreted as follows:

  - ~0:  
    The two most likely clusters have nearly equal probabilities. These
    cases represent highly ambiguous assignments and typically occur
    near cluster boundaries.

  - 0–1:  
    Weak preference for the most likely cluster.

  - 1–2:  
    Moderate preference for the most likely cluster, indicating partial
    separation between clusters but still substantial overlap.

  - 2–5:  
    Clear preference for a single cluster. Assignments in this range are
    generally robust but not strictly deterministic.

  - >5:  
    Very high-confidence assignments, where the probability of
    alternative cluster memberships is negligible.

  In this dataset, `pred3D_conf_margin` values extend up to ~50, which
  corresponds to effectively unambiguous cluster mappings.

  No hard threshold is imposed in the released data. Users may apply
  confidence cuts or weighting schemes appropriate to their specific
  scientific applications.
"""

---

## Notes

The GMM cluster classifications are intended for statistical and
population-level analyses. Individual cluster assignments with low
confidence margins should be interpreted with caution.

---

## Citation

If you use these data products, please cite the associated paper and
the data repository DOI.

