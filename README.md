# DBSCAN Demystified: Epsilon, Min Samples, Noise Detection and Arbitrary Shapes

> A machine learning tutorial exploring how DBSCAN's two key parameters — ε (epsilon) and min_samples — control cluster granularity, noise detection, and the discovery of arbitrarily-shaped clusters.

---

## Overview

This repository contains the code and report for a tutorial on **DBSCAN** (Density-Based Spatial Clustering of Applications with Noise), a powerful unsupervised learning algorithm that groups data by local density rather than distance to centroids.

Unlike K-Means, DBSCAN:

- Discovers clusters of **any arbitrary shape** (crescents, rings, spirals)
- **Automatically identifies outliers** — labelled as noise (class `-1`)
- Does **not require the number of clusters** to be specified in advance

The tutorial investigates DBSCAN's two key parameters through five controlled experiments:

| Parameter | What it controls |
|---|---|
| `eps` (ε) | Neighbourhood radius — how close two points must be to be considered neighbours |
| `min_samples` | Minimum neighbours within ε for a point to qualify as a core point |

---

## Repository Structure

```
dbscan-tutorial/
│
├── dbscan_tutorial.ipynb            # Full Jupyter notebook with all experiments
├── dbscan_tutorial.docx             # Word document tutorial report (<2000 words)
│
├── figures/                         # All generated figures
│   ├── dbscan_fig1_concept.png      # Core / border / noise diagram
│   ├── dbscan_fig2_epsilon_sweep.png
│   ├── dbscan_fig3_minsamples_sweep.png
│   ├── dbscan_fig4_shapes.png       # DBSCAN vs K-Means comparison
│   ├── dbscan_fig5_noise.png        # Noise detection demo
│   ├── dbscan_fig6_heatmap.png      # Parameter sensitivity heatmap
│   └── dbscan_fig7_kdistance.png    # k-distance elbow plot
│
├── README.md                        # This file
└── LICENSE                          # MIT License
```

---

## Getting Started

### Prerequisites

Python 3.8 or higher is required. Install all dependencies with:

```bash
pip install -r requirements.txt
```

Or manually:

```bash
pip install numpy pandas matplotlib seaborn scikit-learn jupyter
```

No additional datasets need to be downloaded — all data is generated synthetically using `sklearn.datasets`.

### Running the Notebook

```bash
git clone https://github.com/YOUR_USERNAME/dbscan-tutorial.git
cd dbscan-tutorial
jupyter notebook dbscan_tutorial.ipynb
```

Run all cells from top to bottom. Each section is self-contained and produces its own figure.

---

## Experiments

### Experiment 1 — Effect of ε (Epsilon)
Sweeps ε from 0.1 to 1.0 on the Two Moons dataset with `min_samples=5` fixed. Demonstrates the transition from over-fragmented (all noise) to optimal (2 correct clusters) to over-merged (1 giant cluster).

### Experiment 2 — Effect of min_samples
Fixes `eps=0.35` and varies `min_samples` from 2 to 40. Shows how the density threshold controls noise sensitivity — too low and even isolated pairs form clusters; too high and genuine cluster members become noise.

### Experiment 3 — Parameter Sensitivity Heatmap
A full grid search over ε × min_samples showing the number of clusters found and noise points generated for every combination. Reveals the narrow optimal region and the interaction between both parameters.

### Experiment 4 — Arbitrary Shape Detection
Compares DBSCAN against K-Means on three non-convex datasets: Two Moons, Concentric Rings, and Anisotropic Blobs. K-Means fails on all three; DBSCAN succeeds by using local density rather than centroid distance.

### Experiment 5 — Noise Detection
Injects 50 uniformly random outliers into a structured 3-cluster dataset. Demonstrates that well-tuned parameters correctly isolate outliers, while over-permissive parameters absorb them into clusters.

---

## Key Results

| Setting | Clusters Found | Noise Points | Result |
|---|---|---|---|
| ε=0.1, min_samples=5 | 0–10+ | ~250 | Under-connected — too much noise |
| ε=0.35, min_samples=5 | 2 | ~5 | **Optimal** — both moons correct |
| ε=1.0, min_samples=5 | 1 | 0 | Over-merged — single cluster |
| ε=0.5, min_samples=8 (noise test) | 3 | ~48 | Correctly detects injected outliers |

---

## Accessibility

This tutorial was designed with accessibility in mind:

- All figures use a **colour-blind friendly palette** (Wong 2011 eight-colour set)
- Noise/outlier points use both a **distinct colour** and an **× marker shape** so they are distinguishable without relying on colour alone
- All figures include descriptive captions
- Tables use clear headers with sufficient contrast
- Code is fully commented for screen reader compatibility

---

## References

1. Ester, M., Kriegel, H. P., Sander, J., & Xu, X. (1996). A density-based algorithm for discovering clusters in large spatial databases with noise. *KDD-96*, 226–231.
2. Schubert, E. et al. (2017). DBSCAN Revisited, Revisited: Why and How You Should (Still) Use DBSCAN. *ACM TODS*, 42(3). https://doi.org/10.1145/3068335
3. Rahmah, N. & Sitanggang, I.S. (2016). Determination of Optimal Epsilon (Eps) Value on DBSCAN Algorithm. *IOP Conf. Series*. https://doi.org/10.1088/1755-1315/31/1/012012
4. Pedregosa, F. et al. (2011). Scikit-learn: Machine Learning in Python. *JMLR*, 12, 2825–2830.

---

## License

This project is licensed under the **MIT License** — see the [LICENSE](LICENSE) file for details. You are free to use, modify, and distribute this code with attribution.

---

## Author

**[Your Name]**  
[Your Institution / Course Name]  
[Your Email (optional)]
