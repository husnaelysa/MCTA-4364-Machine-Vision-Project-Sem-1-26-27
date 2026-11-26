# Improving Deep Learning-Based Industrial Visual Anomaly Detection for Automated Quality Inspection

**Course:** MCTA 4364 Machine Vision, Semester 1, 2026/2027 (IIUM)
**Track:** Track 2 (Paper reproduction and extension)

## Members

| Name | Matric no. | GitHub username |
|---|---|---|
| NUR HUSNA ELYSA MAISARAH BINTI ROSLI | 2310366 | husnaelysa |
| NUR QISTINA BINTI MOHD FAIZAL | 2319512 | qistinafaizal |

## Source paper

- Batzner, Heckler, König. *EfficientAD: Accurate Visual Anomaly Detection at Millisecond-Level Latencies.* WACV 2024.
- Paper link (PDF): (https://openaccess.thecvf.com/content/WACV2024/papers/Batzner_EfficientAD_Accurate_Visual_Anomaly_Detection_at_Millisecond-Level_Latencies_WACV_2024_paper.pdf)
- Official code: https://github.com/lx9182/effientAD
- Implementation reused in this repo: anomalib, version 2.7.1 (https://github.com/open-edge-platform/anomalib) 

## Dataset

MVTec AD (Bergmann et al., CVPR 2019). Licence: CC BY-NC-SA 4.0 (non-commercial), see the dataset page. The dataset is **not** included in this repo; the notebook downloads it.
Subset used: Bottle.

## What is in this repo (progress-v1)

```
.
├── README.md
├── requirements.txt
├── notebooks/
│   └── efficientad_baseline.ipynb   # runs on Google Colab (GPU)
├── scripts/
│   └── efficientad_baseline.py      # same code as plain text
├── results/
│   ├── baseline_results.csv
│   ├── dataset_stats.csv
│   ├── environment.json
│   └── figures/                     # class distribution, samples, correct/failed examples
└── report/
    └── MCTA4364_Progress_<GroupRepName>.pdf
```

## How to run the baseline

1. Open `notebooks/efficientad_baseline.ipynb` in Google Colab.
2. Runtime > Change runtime type > GPU (T4).
3. Edit the configuration cell: `CATEGORIES`, `MAX_STEPS`, `SEED`.
4. Run all cells. Results and figures are saved to Google Drive (`MyDrive/mcta4364_efficientad`). Copy them into `results/`.

Environment: Python 3.13.18 (main, Oct 26 2026, 15:28:15) [GCC 13.3.0], PyTorch 2.14.1+cpu, anomalib 2.7.1, GPU Colab T4. See `results/environment.json`.

Smoke test: `CATEGORIES = "bottle"`, `MAX_STEPS = 300`.

## Baseline settings

- Model: anomalib EfficientAd, size S
- Training steps: 70,000
- Image size: 256x256, batch size 1, seed 42

## Baseline results

[Paste the table from results/baseline_results.csv and compare with the paper. Do not fill in numbers you did not obtain.]

## Code provenance

- Written by us: [notebook glue code, evaluation loop, plots, analysis]
- Reused: anomalib library (model, training, data loading), MVTec AD dataset, Imagenette (used by EfficientAD's training penalty)
- AI tools: [declare how they were used]

## Contributions

- NUR HUSNA ELYSA MAISARAH BINTI ROSLI (2310366): README, requirements.txt, notebook, scripts/
- NUR QISTINA BINTI MOHD FAIZAL (2319512): results/, report/ PDF, dataset notes in the README

## References

See the report. Key items: EfficientAD (Batzner et al., 2024), MVTec AD (Bergmann et al., 2019), Anomalib (Akcay et al., 2022).
