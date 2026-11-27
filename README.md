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
- Paper link: https://openaccess.thecvf.com/content/WACV2024/papers/Batzner_EfficientAD_Accurate_Visual_Anomaly_Detection_at_Millisecond-Level_Latencies_WACV_2024_paper.pdf 
- Official code: none found as of 27 Nov 2026 (we checked the arXiv page and Papers with Code, which list only third-party implementations). (https://github.com/lx9182/effientAD)
- Implementation reused in this repo: anomalib's EfficientAd (third-party implementation), version 2.7.1 (https://github.com/open-edge-platform/anomalib). Any difference from the paper's reported numbers may partly come from using a non-official implementation.

## Related work with official code

- PUAD (Sugawara and Imamura, 2024), which extends EfficientAD for logical anomalies. Official code: https://github.com/LeapMind/PUAD (we do not use its code in progress-v1; it motivates our planned extension).

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

Environment: exact package versions are in `requirements.txt`; the Colab run also saved `results/environment.json` (Python, GPU, steps, seed).
Install locally with `pip install -r requirements.txt`. The notebook was run on Google Colab with a T4 GPU.

Smoke test: `CATEGORIES = ["bottle"]`, `MAX_STEPS = 300`.

## Baseline settings (declared deviations from the paper)

| Setting | Our run | Paper |
|---|---|---|
| Model | anomalib EfficientAd, size S | EfficientAD-S and -M |
| Training steps | 10,000 per category [confirm: `MAX_STEPS`] | 70,000 |
| Categories | 'BOTTLE' | all 15, plus VisA and MVTec LOCO |
| Image size / batch size | library default (256x256) / 1 | see paper |
| Seed | 42 | not applicable |
| Hardware | Google Colab (T4 GPU) | NVIDIA RTX A6000 (see paper) |

Because of the reduced steps, the subset and the third-party implementation, our numbers are **not** a full reproduction of the paper. Means over our categorie is not comparable with the paper's 15-category means.

## Baseline results

Score summary per class:
  broken_large    n= 20  mean=2.199  min=1.513  max=3.200
  broken_small    n= 22  mean=2.374  min=1.553  max=3.196
  contamination   n= 21  mean=2.459  min=1.110  max=4.410
  good            n= 20  mean=1.157  min=0.929  max=1.459

Image AUROC per defect type:
  broken_large    1.0000
  broken_small    1.0000
  contamination   0.9429

Highest good score: 1.459 | Lowest defect score: 1.110
4.410


## Licence

Our code is released under the MIT licence (see `LICENSE`). MVTec AD keeps its own licence (CC BY-NC-SA 4.0, non-commercial) and is not redistributed here.

## Code provenance

**Written by us**
- `notebooks/efficientad_baseline.ipynb` (and `scripts/efficientad_baseline.py`): the experiment driver, i.e. dataset statistics, per-category training/testing loop, score collection, threshold selection, failure-example selection, latency measurement, plots and result tables. [Edit to match what you actually changed or wrote.]
- Report text, figures and analysis.

**Reused from others (not written by us)**
- **anomalib** (Akcay et al., ICIP 2022): the EfficientAd model, training loop, data loading and metric computation. We call it as a library and do not modify its source.
- **EfficientAD** (Batzner et al., WACV 2024): the method itself. No official code was found; we use anomalib's third-party implementation.
- **MVTec AD** dataset: used under CC BY-NC-SA 4.0, downloaded by anomalib.
- **Imagenette / ImageNet-style images** and the pretrained teacher weights used by EfficientAD's training: downloaded automatically by anomalib.
- Python libraries: PyTorch, Lightning, scikit-learn, pandas, NumPy, Matplotlib, Pillow.

**Not used in progress-v1:** PUAD (https://github.com/LeapMind/PUAD) is cited as related work only; none of its code is in this repo.

**AI tools:** We used Claude (Anthropic) to help draft the report structure, and brain-storming the baseline notebook. We ran the experiments ourselves, checked the code and the results, and can explain every part. 

## Contributions

- NUR HUSNA ELYSA MAISARAH BINTI ROSLI (2310366): README.md, requirements.txt, progress report/PDF
- NUR QISTINA BINTI MOHD FAIZAL (2319512): results/, scripts/, notebooks/

## References

See the report. Key items: EfficientAD (Batzner et al., 2024), MVTec AD (Bergmann et al., 2019), Anomalib (Akcay et al., 2022).
