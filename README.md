# 🧬  Breast Cancer Biomarker Identification from RNA-Seq Transcriptomic Data using Machine Learning
> An end-to-end computational oncology pipeline integrating RNA-Seq transcriptomics, feature engineering, machine learning, biomarker prioritization, pathway enrichment, and biological interpretation for breast cancer classification.

---

## 📌 Project Overview

This project presents a complete machine learning-driven biomarker discovery workflow built from high-dimensional bulk RNA-Seq transcriptomic profiles derived from breast cancer samples. The notebook was designed to demonstrate not only predictive modeling capability, but also biological interpretability and translational relevance.

The pipeline progresses systematically from:

- Raw RNA-Seq dataset ingestion
- Data preprocessing and normalization
- Feature selection using Mutual Information
- Random Forest-based classification
- Cross-validation and model evaluation
- Biomarker prioritization
- Functional enrichment analysis
- Drug-gene association exploration
- Gene Ontology interpretation

The primary objective of this project is to identify biologically meaningful biomarker candidates capable of distinguishing:

- **Primary Tumor samples**
- **Solid Tissue Normal samples**

using robust computational approaches.

---

# 🎯 Why This Project Matters

High-throughput RNA-Seq transcriptomic datasets contain tens of thousands of quantified genes but relatively few biological samples. This creates a classic:

- high-dimensional,
- low-sample-size,
- biologically noisy

machine learning problem.

This project demonstrates the ability to:

✅ Handle RNA-Seq-scale datasets  
✅ Build reproducible ML pipelines  
✅ Perform biologically informed feature reduction  
✅ Interpret model-derived biomarkers  
✅ Connect ML outputs with systems biology  
✅ Translate computational outputs into biologically meaningful hypotheses

---

# 🧠 Research Motivation

Modern computational oncology increasingly relies on interpretable machine learning systems capable of identifying disease-associated molecular signatures.

Rather than treating ML as a black-box classifier, this project emphasizes:

- feature interpretability,
- biomarker extraction,
- biological pathway context,
- and translational relevance.

The workflow was intentionally structured to resemble early-stage computational biomarker discovery pipelines commonly used in:

- cancer bioinformatics,
- translational genomics,
- precision medicine,
- and computational systems biology research.

---

# 🏗️ Complete Pipeline Architecture

```text
Bulk RNA-Seq Transcriptomic Dataset
       │
       ▼
Data Exploration & QC
       │
       ▼
Label Encoding
       │
       ▼
Train/Test Stratified Split
       │
       ▼
MinMax Normalization
       │
       ▼
Mutual Information Feature Selection
       │
       ▼
Random Forest Classification
       │
       ├── Cross Validation
       ├── ROC-AUC Analysis
       ├── Confusion Matrix
       └── Performance Metrics
       │
       ▼
Feature Importance Ranking
       │
       ▼
Top 20 Biomarker Extraction
       │
       ▼
Gene Symbol Mapping
       │
       ▼
Pathway Enrichment Analysis
       │
       ├── KEGG
       ├── Reactome
       ├── WikiPathways
       └── MSigDB Hallmark
       │
       ▼
Drug-Gene Enrichment Analysis
       │
       ▼
Gene Ontology Analysis
       │
       ▼
Biological Interpretation
```

---

# 📂 Repository Structure

```text
.
├── ML_Biomarker_identify.ipynb
├── top_20_biomarker_genes.csv
├── figures/
│   ├── confusion_matrix.png
│   ├── roc_curve.png
│   ├── feature_importance.png
│   ├── kegg_pathways.png
│   └── go_analysis.png
├── data/
│   └── BRCA_expression_dataset.csv
└── README.md
```

---

# 🔬 Methodology

## 1️⃣ RNA-Seq Data Acquisition and Exploration

The workflow begins with importing a processed RNA-Seq expression matrix containing:

- gene expression profiles,
- sample metadata,
- and binary disease labels.

Initial exploratory analysis includes:

- dataset dimensionality inspection,
- label distribution analysis,
- missing value assessment,
- and class visualization.

### Key Objectives

- Verify dataset integrity
- Detect class imbalance
- Understand feature dimensionality
- Ensure ML readiness

---

## 2️⃣ Data Preprocessing

### Label Encoding

Clinical labels were transformed into machine-readable numerical representations.

```python
Primary Tumor → 0
Solid Tissue Normal → 1
```

### Stratified Data Splitting

The dataset was partitioned into training and testing subsets using stratified sampling to preserve class distribution.

### Normalization

MinMax scaling was applied to standardize gene expression values.

This step is critical because RNA-Seq expression features often vary substantially in scale and dynamic range.

---

## 3️⃣ Feature Selection using Mutual Information

One of the central challenges in RNA-Seq machine learning is the curse of dimensionality.

To address this:

- Mutual Information feature selection was applied.
- Informative genes were ranked according to dependency with class labels.
- The top 1000 genes were retained.

### Why Mutual Information?

Unlike simple correlation-based filtering, Mutual Information can capture:

- nonlinear relationships,
- non-monotonic dependencies,
- and complex feature-label interactions.

This improves downstream classification robustness.

---

## 4️⃣ Machine Learning Model Development

### Model Used

- Random Forest Classifier
- Wrapped with One-vs-Rest strategy

### Why Random Forest?

Random Forests are particularly effective for:

- high-dimensional biological datasets,
- nonlinear decision boundaries,
- noisy omics data,
- and embedded feature importance estimation.

### Cross Validation

A 5-fold Stratified Cross Validation framework was implemented to improve reliability and reduce variance in performance estimation.

---

# 📊 Model Evaluation

The project evaluates classification performance using multiple complementary metrics.

## Metrics Used

| Metric | Purpose |
|---|---|
| Accuracy | Overall prediction correctness |
| Precision | False positive control |
| Recall | Sensitivity to positive samples |
| F1 Score | Precision-recall balance |
| ROC-AUC | Threshold-independent separability |

---

## Confusion Matrix Analysis

A confusion matrix heatmap was generated to visualize:

- true positives,
- false positives,
- false negatives,
- and true negatives.

This provides class-level diagnostic insight beyond raw accuracy.

---

## ROC Curve and AUC

Receiver Operating Characteristic analysis was implemented to evaluate discrimination capability across decision thresholds.

The ROC-AUC analysis demonstrates the classifier's ability to distinguish tumor from normal samples.

---

# 🧬 Biomarker Discovery

## Feature Importance Extraction

After model training:

- feature importance scores were extracted from the trained Random Forest model,
- genes were ranked according to predictive contribution,
- and the top candidate biomarkers were identified.

### Final Output

- Top 20 biomarker candidates
- Ranked importance scores
- Exportable biomarker table

---

## Reduced Biomarker Model

A secondary classifier was trained using only the top 20 genes.

This step evaluates whether a compact biomarker signature can maintain strong predictive performance while improving interpretability and translational feasibility.

---

# 🧪 Biological Interpretation

## Gene Symbol Mapping

Ensembl identifiers were converted into human-readable gene symbols using:

- `mygene`
- Ensembl annotation mapping

This allows direct downstream biological interpretation.

---

# 🧭 Functional Enrichment Analysis

To move beyond predictive modeling into systems-level interpretation, enrichment analyses were performed.

## Databases Used

| Database | Purpose |
|---|---|
| KEGG | Pathway analysis |
| Reactome | Biological process networks |
| WikiPathways | Community-curated pathways |
| MSigDB Hallmark | Canonical gene signatures |
| DSigDB | Drug-gene enrichment |

---

## Biological Questions Addressed

- Which pathways are dysregulated?
- Which signaling systems dominate the biomarker set?
- Are identified genes associated with known cancer pathways?
- Which drugs may target these molecular signatures?

---

# 💊 Drug-Gene Enrichment Analysis

The project additionally explores:

- candidate therapeutic associations,
- drug-target relationships,
- and repurposing hypotheses.

This bridges computational biomarker discovery with translational oncology.

---

# 🌱 Gene Ontology Analysis

Gene Ontology analysis was performed across:

- Biological Process (BP)
- Molecular Function (MF)
- Cellular Component (CC)

This enables functional interpretation of identified biomarkers at multiple biological levels.

---

# 📈 Visualizations Included

The notebook includes multiple publication-style visualizations:

- Dataset distribution plots
- Confusion matrix heatmaps
- ROC curves
- Feature importance barplots
- KEGG enrichment visualizations
- Reactome pathway analysis
- GO enrichment plots
- Drug-gene enrichment graphs

---

# 🧰 Technologies and Libraries

## Core Data Science Stack

- Python
- NumPy
- Pandas
- Matplotlib
- Seaborn

## Machine Learning

- Scikit-learn

## Bioinformatics and Functional Analysis

- GSEApy
- MyGene

## Visualization

- Matplotlib
- Seaborn

---

# ⚙️ Reproducibility

The workflow was designed with reproducibility in mind.

### Reproducibility Features

- Fixed random seeds
- Structured pipeline ordering
- Explicit train-test partitioning
- Cross-validation framework
- Exportable biomarker outputs

---

# 🚀 Potential Future Improvements

This repository represents a strong foundational biomarker discovery workflow, with several planned future extensions:

## Planned Enhancements

- Leakage-safe feature selection pipeline
- External dataset validation
- SHAP explainability analysis
- Precision-Recall curve analysis
- Multiple classifier benchmarking
- Nested cross-validation
- Hyperparameter optimization
- Survival analysis integration
- Deep learning-based transcriptomic modeling
- Multi-omics integration

---

# 📚 Scientific Relevance

This project demonstrates practical competency in:

- computational biology,
- RNA-Seq transcriptomics,
- machine learning,
- feature engineering,
- and systems-level biological interpretation.

The workflow reflects many components commonly encountered in:

- bioinformatics MSc/MRes projects,
- computational oncology pipelines,
- and early-stage translational AI research.

---

# 🧠 Skills Demonstrated

## Machine Learning

- Classification modeling
- Cross-validation
- Feature selection
- Performance evaluation
- Model interpretation

## Bioinformatics

- RNA-Seq transcriptomic analysis
- Biomarker prioritization
- Pathway enrichment
- Gene ontology analysis
- Drug-gene interaction exploration

## Research Engineering

- Reproducible notebook structuring
- Scientific visualization
- Data preprocessing pipelines
- Computational workflow design

---

# 💡 Key Takeaway

This repository is not merely a classification notebook.

It is a biologically interpretable computational pipeline demonstrating how machine learning can be integrated with RNA-Seq transcriptomics and systems biology to generate clinically relevant biomarker hypotheses.

The emphasis on:

- interpretability,
- reproducibility,
- biological validation,
- and translational context

reflects a research-oriented mindset beyond basic predictive modeling.

---

# 📬 Contact

If you are interested in:

- computational oncology,
- machine learning for omics data,
- RNA-Seq biomarker discovery,
- or interdisciplinary bioinformatics collaborations,

feel free to connect.

---

# ⭐ If You Found This Useful

Consider starring the repository to support ongoing work in computational biomarker discovery and interpretable machine learning for precision medicine.
