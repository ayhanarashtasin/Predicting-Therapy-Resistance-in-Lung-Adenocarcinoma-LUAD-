

# Predicting Therapy Resistance in Lung Adenocarcinoma (LUAD)

### Leveraging scRNA-seq and Deep Autoencoders for Biomarker Discovery

##  Project Overview

This project addresses a critical challenge in oncology: **Therapy Resistance**. Using single-cell RNA sequencing (scRNA-seq) data from 208,506 cells, I developed a deep learning pipeline to identify rare resistant subpopulations within lung cancer tissues that traditional bulk sequencing often misses.

By integrating a **Residual Autoencoder** with **Explainable AI (SHAP)**, the model achieves high-accuracy classification while identifying biologically validated drivers of resistance, such as the **SPP1** gene.

---

##  Pipeline Architecture

The project follows a structured 10-step bioinformatics and machine learning workflow:

1. **Environment Setup:** Integration of PyTorch, Scanpy, and AnnData.
2. **Data Engineering:** Memory-safe sampling of the GSE131907 dataset.
3. **Quality Control (QC):** Mitochondrial gene filtering (<20%) and doublet removal.
4. **Preprocessing:** Normalization (10k counts), log-transformation, and scaling.
5. **Dimensionality Reduction:** PCA and UMAP for cellular atlas visualization.
6. **Clustering:** Leiden clustering for cell type identification.
7. **Pseudo-Labeling:** Establishing resistance labels using established molecular signatures (EGFR, MET, etc.).
8. **Feature Engineering:** Differential Gene Expression (DGE) analysis to select the top 144 predictive features.
9. **Deep Learning:** Training a custom Autoencoder + Classifier with a 64-D latent bottleneck.
10. **Explainability:** SHAP analysis to decode the "Black Box" and extract biomarkers.

---

## 🛠️ Model Architecture: Scdeep-style Autoencoder

The core of the project is a hybrid neural network designed to handle the high dimensionality and sparsity of scRNA-seq data:

* **Encoder:** Maps input genes to a 64-dimensional latent space using Residual Blocks (ResBlocks).
* **Decoder (Auxiliary):** Reconstructs the original expression to regularize the latent space and ensure biological fidelity.
* **Classifier Head:** Predicts "Resistant" vs. "Sensitive" labels from the latent bottleneck.

---

##  Results & Key Findings

* **Performance:**
* **Test AUC-ROC:** 0.9235
* **Test F1-Score:** 0.86


* **Latent Space:** UMAP visualization of the 64-D bottleneck shows clear structural separation between resistant and sensitive cell manifolds.
* **Biomarker Discovery:** SHAP analysis identified **SPP1 (Osteopontin)** as the top predictive gene. This aligns with clinical literature where SPP1 is a known driver of metastasis and lung cancer resistance.

---

##  Dataset

* **Source:** [GSE131907](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE131907) (Nature Communications, 2020).
* **Scope:** 58 samples from 44 patients, covering primary tumors, lymph nodes, and brain metastases.

---

##  How to Run

1. Clone the repository:
```bash
git clone https://github.com/your-username/lung-cancer-resistance-dl.git

```


2. Install dependencies:
```bash
pip install -q scanpy[leiden] anndata torch shap umap-learn

```


3. Open the Jupyter Notebook/Colab file and update the `file_path` to point to your `GSE131907_Lung_Cancer_raw_UMI_matrix.txt.gz`.

---

##  Author

**Ayhan Arash Tasin**
Computer Science Student | Machine Learning Enthusiast
*Focus: Bioinformatics, NLP, and LLM Thesis Research.*

---

## 📜 Acknowledgments

Special thanks to the authors of *Nature Communications 2020, 11(1):2285* for providing the open-access scRNA-seq dataset that made this research possible.
