# Two-Stage Diagenesis Model Validation Code

**Supplementary Code S3 for Quantitative Assessment of Single-Stage vs. Two-Stage Diagenetic Models**

---

## 📁 File Structure

```
Supplementary_Code_S3/
├── 01-model_fit_quality_assessment.py      # Model fit quality evaluation
├── 02-parameter_validation.py              # Parameter sensitivity analysis
├── 03-comparative_analysis.py              # Single-Stage vs Two-Stage comparison
├── Dataset-Case-3-2.csv                    # Example dataset (n=476 samples)
└── README.md                                # This file
```

---

## 🔬 Overview

This code package implements quantitative validation of the **Two-Stage Diagenetic Model** proposed in the main manuscript. It provides three independent analytical modules to:

1. **Assess model fit quality** using ternary diagram projections and statistical metrics
2. **Validate parameter robustness** through sensitivity analysis
3. **Compare model performance** between Single-Stage and Two-Stage scenarios

**Theoretical Framework**: Banner & Hanson (1990) water-rock interaction model applied to carbonate diagenesis.

**Reference**: See main manuscript Section 3.6-3.7 and Supplementary Materials for detailed methodology.

---

## 📋 Prerequisites

### Python Environment
- **Python version**: ≥ 3.7
- **Recommended**: Anaconda or Miniconda

### Required Libraries
Install dependencies using pip:

```bash
pip install numpy pandas matplotlib scipy
```

Or use the provided `requirements.txt`:
```bash
pip install -r requirements.txt
```

**Library versions used in this study**:
- numpy >= 1.21.0
- pandas >= 1.3.0
- matplotlib >= 3.4.0
- scipy >= 1.7.0

---

## 🚀 Execution Instructions

### **Step 1: Prepare Input Data**

Ensure `Dataset-Case-3-2.csv` is in the **same directory** as the Python scripts.

**Dataset specifications**:
- **Sample size**: n = 476 ooid samples
- **Required columns**: `Mn/Sr`, `Mn/Fe`, `Sr/Ca`
- **Data format**: Numeric values (atomic ratios)

**Example CSV structure**:
```csv
Unnamed: 0,Mn/Fe,Mn/Sr,Sr/Ca
SJ-1_0,0.392393,2.240617,0.001131
SJ-1_1,0.317557,2.034954,0.001562
...
```

---

### **Step 2: Execute Scripts**

The three scripts can be run **independently** or **sequentially** for comprehensive analysis.

#### **Option A: Run All Scripts Sequentially (Recommended)**

```bash
python 01-model_fit_quality_assessment.py
python 02-parameter_validation.py
python 03-comparative_analysis.py
```

**Total runtime**: ~1-2 minutes (standard laptop)

#### **Option B: Run Individual Scripts**

If you only need specific analyses:

```bash
# For fit quality assessment only
python 01-model_fit_quality_assessment.py

# For parameter validation only
python 02-parameter_validation.py

# For model comparison only
python 03-comparative_analysis.py
```

---

### **Step 3: Check Outputs**

Each script generates both **figure** and **data** outputs:

| Script | Output Figure | Output Data | Description |
|--------|---------------|-------------|-------------|
| **Script 01** | `Fit_Quality_Assessment.png` | `model_fit_statistics.csv` | Ternary diagram with model curves and sample points |
| **Script 02** | `Parameter_Sensitivity_Analysis.png` | `parameter_validation_results.csv` | Sensitivity analysis for key parameters (D, N ranges) |
| **Script 03** | `Model_Comparison.png` | `comparative_analysis_results.csv` | RMSE comparison and goodness-of-fit statistics |

**All figures are publication-ready** (300 DPI, vector-compatible PNG format).

---

## 🔧 Model Parameters

### **Single-Stage Model Parameters**

| Parameter | Value | Description |
|-----------|-------|-------------|
| **Cs0_Sr** | 9874 ppm | Initial Sr concentration in solid phase |
| **Cs0_Mn** | 0.735 ppm | Initial Mn concentration in solid phase |
| **Cs0_Fe** | 164 ppm | Initial Fe concentration in solid phase |
| **Cf0_Sr** | 0.15 ppm | Sr concentration in diagenetic fluid |
| **Cf0_Mn** | 6.0 ppm | Mn concentration in diagenetic fluid |
| **Cf0_Fe** | 120 ppm | Fe concentration in diagenetic fluid |
| **D_Sr** | 0.08 | Sr partition coefficient |
| **D_Mn** | 18.0 | Mn partition coefficient |
| **D_Fe** | 18.0 | Fe partition coefficient |
| **N_range** | 0.01–300 | Water-rock ratio range |

### **Two-Stage Model Parameters**

#### Stage 1: Early Diagenesis (N = 0.01–10)
- Same initial conditions as Single-Stage model
- Partition coefficients: D_Sr = 0.08, D_Mn = 18.0, D_Fe = 18.0

#### Stage 2: Late Diagenesis (N = 0.5–200)
| Parameter | Value | Change from Stage 1 |
|-----------|-------|---------------------|
| **Cs0_Sr** | 5000 ppm | ↓ (inherited from Stage 1 endpoint) |
| **Cs0_Mn** | 25 ppm | ↑ (Mn-enriched after early diagenesis) |
| **Cs0_Fe** | 140 ppm | ↑ (slight increase) |
| **Cf0_Sr** | 0.05 ppm | ↓ (depleted fluid) |
| **Cf0_Mn** | 15 ppm | ↑ (Mn-rich burial fluid) |
| **Cf0_Fe** | 200 ppm | ↑ (Fe-rich burial fluid) |
| **D_Sr** | 0.04 | ↓ (lower temperature) |
| **D_Mn** | 25.0 | ↑ (enhanced partitioning) |
| **D_Fe** | 22.0 | ↑ (enhanced partitioning) |

**Reference**: See Table 3 and Section 3.6 in the main manuscript.

---

## 📊 Expected Results

### **Script 01: Fit Quality Assessment**

**Output Figure** (`Fit_Quality_Assessment.png`):
- Ternary diagram with Mn/Sr, Mn/Fe, and Sr/Ca (scaled ×300) as vertices
- Sample points color-coded by deviation from model curves
- Model curves for Single-Stage (black dashed) and Two-Stage (crimson + blue) models

**Key Metrics** (saved in `model_fit_statistics.csv`):
- Mean RMSE: Single-Stage ≈ 0.0345, Two-Stage ≈ 0.0245
- Excellent fit (<0.05): Single-Stage ≈ 75%, Two-Stage ≈ 93%

### **Script 02: Parameter Validation**

**Output Figure** (`Parameter_Sensitivity_Analysis.png`):
- Multi-panel figure showing how model curves respond to ±20% variation in:
  - Partition coefficients (D_Sr, D_Mn, D_Fe)
  - Water-rock ratio ranges (N_min, N_max)

**Interpretation**: 
- Small parameter variations cause minimal curve shifts → Model is robust

### **Script 03: Comparative Analysis**

**Output Figure** (`Model_Comparison.png`):
- Histogram comparing RMSE distributions for Single-Stage vs Two-Stage models
- Statistical annotation showing improvement metrics

**Key Findings** (saved in `comparative_analysis_results.csv`):
- RMSE reduction: ~29% (from 0.0345 to 0.0245)
- Goodness-of-fit improvement: +18.3 percentage points in excellent-fit samples

---

## ⚠️ Troubleshooting

### Common Issues:

1. **Error: "FileNotFoundError: Dataset-Case-3-2.csv"**
   - Ensure the CSV file is in the same directory as the Python script
   - Check filename spelling (case-sensitive on Linux/Mac)

2. **Error: "KeyError: 'Mn/Sr' not found"**
   - Verify that the CSV contains columns: `Mn/Sr`, `Mn/Fe`, `Sr/Ca`
   - Check for extra spaces in column names

3. **Warning: "Figure window too small"**
   - Ignore this warning (matplotlib auto-adjusts layout)
   - Output figures are not affected

4. **Poor figure quality when opening PNG**
   - Figures are high-resolution (300 DPI)
   - Use professional image viewers (not Windows Photo Viewer)
   - For publication, convert PNG to TIFF or EPS if required

5. **Import errors**
   - Reinstall dependencies: `pip install --upgrade numpy pandas matplotlib scipy`
   - Check Python version: `python --version` (should be ≥ 3.7)

---

## 📖 Citation

If you use this code in your research, please cite:

> [Author et al. (Year). Article Title. *Journal Name*, Volume(Issue), Pages. DOI: xxx]

---

## 📧 Contact

For questions or issues related to this code, please contact:

- **Corresponding Author**: [Name] ([email@institution.edu])
- **Code Developer**: [Name] ([email@institution.edu])  
  (Code development assisted by large language models Claude and Gemini for optimization and documentation)

---

## 📄 License

This code is provided as supplementary material for academic research purposes.  
Redistribution and use in source and binary forms are permitted for non-commercial applications with proper citation of the original publication.

---

## 🔄 Version History

- **v1.0** (2026-02-02): Initial release with manuscript submission

---

## 🔗 Related Code Packages

- **Supplementary Code S1**: CL-RIQA & DTW Alignment Protocol
- **Supplementary Code S2**: [Description if applicable]

---

**Last Updated**: February 2, 2026
