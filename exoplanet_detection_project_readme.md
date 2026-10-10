# 🪐 AI-enabled Detection of Exoplanets from Noisy Astronomical Light Curves

![ISRO](https://img.shields.io/badge/ISRO-Bharatiya_Antariksh_Hackathon_2026-orange?style=for-the-badge)
![Problem Statement](https://img.shields.io/badge/Problem_Statement-7-blue?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Prototype-success?style=for-the-badge)

**Team Name:** Masala_Dosa  
**Institution:** Delhi Technological University  
**Team Members:** Aditya Bhaker (Leader), Akansha, Kornika Hajra, Gatik Singh  

## 📖 Overview

The proposed automated exoplanet detection pipeline effectively handles instrumental noise and single-transit gaps using adaptive preprocessing and a dual-track detection framework. It reduces false-positive contamination while overcoming the limitations of black-box AI through the integration of physics-based validation and explainable machine learning techniques.

## 🎯 Objectives & Challenges Mitigated

Throughout the scope of this project, our focus has remained on mitigating the following critical challenges faced by existing astronomical pipelines:

1. **Stellar Blending:** Nearby stars contaminate the target's light, hiding real transits and causing false positives.
2. **High Computational Overhead:** Millions of light curves make validation computationally expensive and difficult to scale.
3. **Telemetry Discontinuities:** Data downlinks and spacecraft jitter interrupt observations, creating corrupted data segments.
4. **Single-Transit Bottleneck:** Traditional methods miss long-period planets that transit only once.
5. **Non-Gaussian Red Noise:** Thermal changes and detector aging create time-correlated noise that distorts transit signals.
6. **Low Signal-to-Noise Ratio (SNR):** Small exoplanet transits are buried beneath stellar and instrumental noise.

## ⚙️ Methodology & Pipeline Architecture

Our end-to-end pipeline is structured into a rigorous, multi-stage workflow:

1. **Data Acquisition & Triage:** Collects stellar light curve data from surveys like TESS (SPOC/QLP/TPFs) and performs initial screening to determine the required processing approach.
2. **Adaptive Light Curve Preparation:** Removes noise, systematic effects (CBV, GP Regression), and outliers while normalizing the signal to create a clean and reliable light curve.
3. **Hybrid Transit Detection:** Detects possible exoplanet transit events using periodic (BLS/TLS) and single-event (Matched Filter) detection methods with candidate fitting.
4. **Dual-View & CNN Encoding:** Extracts local and global transit patterns and uses a 1D CNN model to encode light curve morphology features.
5. **Physics Feature Fusion:** Combines AI-extracted features with astrophysical parameters (cross-matched via Gaia DR3 or TIC v8) to create a comprehensive feature representation.
6. **Hierarchical AI Decision Engine (Stage 1):** Uses an XGBoost machine learning classifier to quickly screen and separate potential planet candidates from false positives/junk.
7. **High-Fidelity Fitting (Stage 2):** Applies detailed transit modeling (BATMAN) and statistical sampling (MCMC) to estimate planetary and stellar parameters accurately.
8. **Physics Validation:** Applies astrophysical constraints (Kepler's Law, Stellar Density, Roche Limit, Transit Duration, Contamination) to eliminate physically impossible candidates.
9. **Final Decision:** Confirms candidates that satisfy all AI, statistical, and physical validation criteria as highly reliable planet candidates.
10. **Explainable AI:** Provides model interpretation using tabular **SHAP** and **Grad-CAM** to understand feature importance and ensure transparent AI decision-making.

## 📊 Uncertainties Estimation

To ensure scientific rigor, uncertainties are tracked and estimated at every stage of the pipeline:

| Stage | Uncertainty | How to Estimate |
| :--- | :--- | :--- |
| **Light Curve Data** | Photometric (flux) uncertainty | Use flux error values provided in TESS data or estimate standard deviation of out-of-transit flux. |
| **Preprocessing** | Noise reduction uncertainty | Compare Signal-to-Noise Ratio (SNR) before/after preprocessing; compute residual noise (RMS). |
| **Transit Detection** | Detection confidence | Signal Detection Efficiency (SDE), Signal-to-Noise Ratio (SNR), False Alarm Probability (FAP). |
| **CNN Classification** | Prediction uncertainty | Softmax probability, Monte Carlo Dropout, or Deep Ensembles. |
| **XGBoost Classification** | Classification confidence | Predicted probability score and confidence threshold. |
| **Feature Engineering** | Measurement uncertainty | Propagate uncertainties from Gaia DR3 stellar parameters into derived features. |
| **BATMAN + MCMC** | Transit parameter uncertainty | Posterior distributions with median and 68%/95% credible intervals. |
| **Physics Validation** | Physical consistency uncertainty | Compare fitted parameters against expected astrophysical ranges. |
| **Explainability** | Explanation stability | Compare SHAP values or Grad-CAM maps across multiple runs or perturbed inputs. |

## 🧠 Fundamental Assumptions

1. **Transit Signal Assumption:** Planetary transits produce measurable, recognizable dips in stellar brightness.
2. **Noise Removal Assumption:** Preprocessing effectively separates instrumental noise from genuine astrophysical signals.
3. **Feature Representation Assumption:** Extracted light curve features sufficiently distinguish planets from false positives.
4. **Astrophysical Model Assumption:** Transit fitting follows established orbital mechanics and stellar physics.
5. **Feature Fusion Assumption:** Combining AI and physics-based features improves detection accuracy over relying on either alone.
6. **Explainability Assumption:** SHAP and Grad-CAM accurately reflect the mathematical factors driving the model's decisions.

## 🛠️ Tools and Libraries Used

* **Data Sources:** TESS, SPOC/QLP, TPFs, Gaia DR3, TIC v8
* **Astronomy & Signal Processing:** `Lightkurve`, `Astropy`, `SciPy`, `TLS` (Transit Least Squares), `BLS`
* **AI & Transit Modeling:** `TensorFlow`/`Keras` (CNN), `XGBoost`, `BATMAN`, `MCMC`, `PyTorch`
* **Explainability & Visualization:** `SHAP`, `Grad-CAM`, `Matplotlib`, `Plotly`
* **Development Environment:** Python, Jupyter, VS Code, GitHub

## 💰 Implementation Cost
* **Software:** 100% Open-Source Ecosystem.
* **Infrastructure:** Designed to run on free cloud platforms (Google Colab, Kaggle Notebooks) or standard laptops. 
* **Estimated Prototype Cost:** ₹0 - ₹5,000.

## 📚 References

* **BLS:** [https://doi.org/10.1051/0004-6361:20020802](https://doi.org/10.1051/0004-6361:20020802)
* **TLS:** [https://doi.org/10.1051/0004-6361/201834672](https://doi.org/10.1051/0004-6361/201834672)
* **AstroNet:** [https://doi.org/10.3847/1538-3881/aa9e09](https://doi.org/10.3847/1538-3881/aa9e09)
* **ExoMiner:** [https://doi.org/10.1038/s41550-023-01914-0](https://doi.org/10.1038/s41550-023-01914-0)
* **SHAP:** [NeurIPS 2017 Paper](https://proceedings.neurips.cc/paper/2017/hash/8a20a8621978632d76c43dfd28b67767-Abstract.html)
* **BATMAN:** [https://doi.org/10.1086/683602](https://doi.org/10.1086/683602)

---
*Developed for the Bharatiya Antariksh Hackathon 2026.*