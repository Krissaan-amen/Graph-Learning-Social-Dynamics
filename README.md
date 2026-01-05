# Social Network Analysis & Graph Learning: Facebook100

![Python](https://img.shields.io/badge/Python-3.8%2B-blue?style=for-the-badge&logo=python&logoColor=white)
![NetworkX](https://img.shields.io/badge/NetworkX-Graph%20Theory-red?style=for-the-badge)
![Scikit-Learn](https://img.shields.io/badge/scikit--learn-Machine%20Learning-orange?style=for-the-badge&logo=scikit-learn&logoColor=white)

## 📖 Overview

This project implements a comprehensive **Network Science and Graph Learning** pipeline to analyze social structures within the **Facebook100 (FB100)** dataset. The FB100 dataset contains complete friendship networks from 100 U.S. universities from September 2005, providing a rich benchmark for analyzing social dynamics, homophily, and community structure.

The analysis focuses on uncovering latent patterns in social graphs through structural property analysis, link prediction algorithms, and semi-supervised attribute inference.

## 📊 Dataset

**Source**: The [Facebook100 Dataset](https://archive.org/details/oxford-2005-facebook-matrix) (Traud et al., 2012).
*   **Scale**: 100 separate university networks.
*   **Nodes**: Users (students/faculty).
*   **Edges**: "Friendship" links.
*   **Attributes**: Dorm, Major, Gender, Class Year, Student/Faculty Status.

> **Note**: This repository uses the anonymized version of the dataset for educational and research purposes.

## 🛠️ Project Objectives & Methodology

### 1. Social Network Analysis (SNA)
Exploratory analysis of fundamental graph properties to characterize the topology of social interactions.
*   **Degree Distributions**: Analysis of scale-free properties and heavy-tailed distributions.
*   **Clustering**: Computation of local and global clustering coefficients.
*   **Density & Path Lengths**: Assessment of the "small-world" nature of the networks.

### 2. Assortativity & Homophily
Quantifying the tendency of individuals to associate with peers who share similar attributes using assortativity coefficients.
*   **Attributes Analyzed**: Student/Faculty status, Dorm, Class Year, Major, and Gender.

### 3. Link Prediction
Implementation and evaluation of heuristic algorithms to predict missing or future edges:
*   **Algorithms**: Common Neighbors, Jaccard Coefficient, Adamic-Adar Index.
*   **Validation**: Precision-Recall analysis on graphs with randomly removed edges (f=0.05, f=0.2).

### 4. Label Propagation (Semi-Supervised Learning)
Recovering missing node attributes using graph structure and the principle of homophily.
*   **Algorithm**: Iterative Label Propagation.
*   **Evaluated Attributes**: Gender (Binary) vs. Major/Dorm (Multi-class).

### 5. Community Detection
Detecting latent social groups using **Louvain Modularity Optimization** and validating them against ground-truth labels like *Dormitory* (spatial) or *Class Year* (temporal).

## 📈 Key Findings & Results

### 1. Network Topology (Selected Universities)
Small, residential colleges (like Caltech) exhibit significantly higher density and clustering than large universities, reflecting a tighter "small-world" community structure.

| Metric | Caltech | MIT | Johns Hopkins |
| :--- | :--- | :--- | :--- |
| **Global Clustering Coeff.** | 0.2913 | 0.1803 | 0.1932 |
| **Avg. Local Clustering** | 0.4091 | 0.2724 | 0.2690 |
| **Density** | 0.0574 | 0.0123 | 0.0140 |

### 2. Assortativity Coefficients (Homophily)
We observed that **Status** and **Year** are the strongest drivers of friendship, while **Gender** plays a negligible role in tie formation.

| Attribute | Assortativity Range (Approx) | Interpretation |
| :--- | :--- | :--- |
| **Student/Faculty** | `0.30 - 0.40` | **Strong Homophily**: Distinct separation between students and staff. |
| **Class Year** | `0.20 - 0.50` | **Strong Homophily**: Students mostly befriend their cohort. |
| **Dorm** | `0.10 - 0.30` | **Moderate**: Housing influences friendship, especially in smaller schools. |
| **Major** | `0.03 - 0.06` | **Weak**: Academic major is not a primary driver of social circles. |
| **Gender** | `~ 0.00` | **Neutral**: No significant preference for same-gender friendships. |

### 3. Link Prediction Performance
*   **Best Performer**: **Adamic-Adar** generally outperformed Common Neighbors and Jaccard by penalizing connections to high-degree hubs.
*   **Impact of Sparsity**: Removing 20% of edges yielded higher precision (~70% at k=50 for Caltech) compared to removing 5%, as the top-scoring predictions were more likely to match the larger set of missing edges.

### 4. Label Propagation Accuracy (Caltech Case Study)
Binary attributes were recovered with much higher success than high-cardinality attributes.

| Attribute Type | Attribute | Accuracy | Observations |
| :--- | :--- | :--- | :--- |
| **Binary** | Gender | **~62 - 66%** | High success rate due to simple binary classification. |
| **Multi-class** | Major | **~47 - 49%** | Moderate success; homophily exists but is weaker. |
| **Multi-class** | Dorm | **~12 - 15%** | Low accuracy due to high number of categories and noise. |

##  Getting Started

### Installation

```bash
git clone https://github.com/Krissaan-amen/Graph-Learning-Social-Dynamics.git
cd facebook100-graph-learning
pip install -r requirements.txt
```

### Usage
Run the main analysis notebook to reproduce the results:

```bash
jupyter notebook main.ipynb
```

## 📚 References

*   **Traud, A. L., Mucha, P. J., & Porter, M. A. (2012).** *Social structure of Facebook networks.* Physica A: Statistical Mechanics and its Applications, 391(16), 4165-4180.
*   **Newman, M. E. J. (2003).** *The structure and function of complex networks.* SIAM Review.
```
