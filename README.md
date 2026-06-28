# ACM Summer School — AI for Health: Hands-on Notebooks

Self-contained Google Colab notebooks accompanying the talk
**"Exploring Health and Wellness through Respiratory Sensing"** (Nipun Batra,
Sustainability Lab, IIT Gandhinagar).

Every notebook **runs top-to-bottom with no setup**: it first proves the
pipeline on synthetic data with a *known* answer, then runs the **same code on
real lab data** downloaded at runtime from the projects' public repositories.

> ⚠️ All notebooks are **educational demos, not medical devices.** Do not use
> them for diagnosis or any clinical decision.

| # | Notebook | Open in Colab | Teaches | Real data used |
|---|----------|---------------|---------|----------------|
| 01 | **Heart Rate from a Phone Camera** | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/sustainability-lab/acm-health-notebooks/blob/main/01_Heart_Rate_from_Phone_Camera.ipynb) | Contact **PPG** — finger-on-lens video (flash on) → HR via FFT + peak detection, HRV | *(record your own; no lab dataset)* |
| 02 | **Respiration Rate from Thermal Video** | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/sustainability-lab/acm-health-notebooks/blob/main/02_Respiration_Rate_from_Thermal_Video.ipynb) | Respiration from a thermal ROI; **RR→Energy-Expenditure** (JoulesEye) | Real 72 s thermal clip (`ApneaEye_Demo`) → 17.6 brpm |
| 03 | **Sleep Apnea Detection & AHI** | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/sustainability-lab/acm-health-notebooks/blob/main/03_Sleep_Apnea_Detection_and_AHI.ipynb) | Central/obstructive apnea + hypopnea → Precision/Sensitivity/Specificity → **AHI** (ApneaEye) | Real thermal clip for the airflow front-end |
| 04 | **Lung Function from Breathing Sound** | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/sustainability-lab/acm-health-notebooks/blob/main/04_Lung_Function_from_Breathing_Sound.ipynb) | Mask-mic spirometry: envelope, **MFCC from scratch**, flow–volume, FEV1/FVC (SpiroMask) | Real N95 mask-mic FVC audio + clinical ground truth (`SpiroMask_DIY`) |

## Running

- **Colab (recommended):** click a badge above → `Runtime → Run all`. Real data
  downloads automatically; notebook 01 (and the "your own data" cells) let you
  upload your own recording.
- **Locally:** `pip install numpy scipy matplotlib opencv-python` then
  `jupyter lab`. Verified end-to-end on numpy 1.26 / scipy 1.16 / matplotlib 3.10.

## Data provenance & credit

Real samples are fetched at runtime from the original authors' public repos:

- **Thermal video** — [`AyushShrivstava/ApneaEye_Demo`](https://github.com/AyushShrivstava/ApneaEye_Demo) (ApneaEye)
- **Mask-mic audio + ground truth** — [`AyushShrivstava/SpiroMask_DIY`](https://github.com/AyushShrivstava/SpiroMask_DIY) and [`rishi-a/SpiroMask`](https://github.com/rishi-a/SpiroMask) (SpiroMask, ACM HEALTH '23)
- **JoulesEye** — [`rishi-a/JoulesEye-Release`](https://github.com/rishi-a/JoulesEye-Release) (ACM IMWUT '24)

Real, labelled overnight **apnea** recordings are clinical and access-restricted
(ApneaEye was evaluated at AIIMS New Delhi), so notebook 03 uses synthetic
signals for the event/AHI stage and real thermal data only for the front-end.

## Design notes

- Synthetic-first: every method is validated against a known answer before being
  trusted on real data.
- Shared signal-processing core: detrend → zero-phase Butterworth band-pass →
  FFT peak / time-domain peak detection.
- No private datasets are bundled; only small public samples are downloaded.
