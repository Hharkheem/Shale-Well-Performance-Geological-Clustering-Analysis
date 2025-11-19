# Shale-Well-Performance-Geological-Clustering-Analysis

This repository contains a Jupyter notebook (`main2.ipynb`) that performs unsupervised geological clustering on a dataset of 506 horizontal shale wells to identify natural geological "sweet spot" groups based on reservoir properties — independent of completion design.

The goal is to separate geology-driven performance differences from completion-driven ones, helping engineers understand how much of the observed EUR variation is due to "where" the well was drilled versus "how" it was completed.

### Key Features Analyzed (Geological Only)
- `Porosity` (%)
- `Thickness` (ft)
- `Water Saturation` (%)
- `Pressure Gradient` (psi/ft)
- `Dip` (degrees)

Target variable: `EUR` (Estimated Ultimate Recovery)

## Key Findings

Using **K-Means clustering (k=3)** on scaled geological features:

| Cluster | Avg Porosity (%) | Avg Thickness (ft) | Avg Water Sat (%) | Avg Pressure Gradient | Avg Dip (°) | **Avg EUR** | Interpretation |
|---------|------------------|--------------------|-------------------|------------------------|-------------|-------------|----------------|
| 0       | 7.16             | 157                | 18.8              | 0.939                  | **1.0**     | **14.81**   | **High-dip / faulted area** – highest productivity |
| 2       | **7.87**         | **172**            | **17.2**          | **0.946**              | 0.0         | **13.78**   | **Best reservoir quality** (high porosity, thick, low water sat) |
| 1       | **6.47**         | 147                | **22.7**          | 0.902                  | 0.0         | **10.88**   | **Poorest geology** – lowest EUR |

**Cluster 0** stands out as the only group with significant structural dip (~1°), suggesting it may lie in a faulted or structurally complex zone that enhances natural fracturing and productivity.

Even though Cluster 2 has the best reservoir properties, **Cluster 0 outperforms it by ~7% in average EUR**, highlighting the importance of natural fractures/structural setting in this play.

## Visualizations

### 1. PCA Projection of Geological Clusters
<img width="1000" height="600" alt="image" src="https://github.com/user-attachments/assets/f13ccb70-72ae-4364-b675-ed55b5222473" />
*2D PCA visualization showing clear separation of the three geological regimes.*

### 2. EUR Distribution by Cluster
<img width="800" height="600" alt="image" src="https://github.com/user-attachments/assets/8a2cf740-73ab-47ca-bfb2-d5d3e43b7900" />
*Wells in high-dip Cluster 0 consistently outperform even the best rock quality (Cluster 2).*

## Notebook Structure (`main2.ipynb`)

1. **Data Loading & Exploration** – Loads the attached dataset (~506 wells)
2. **Feature Selection** – Uses only pure geological variables
3. **Scaling** – StandardScaler applied
4. **Elbow Method** – Determines optimal k=3 (included in original analysis)
5. **K-Means Clustering** – Fits final model with `k=3`
6. **PCA Visualization** – Reduces to 2D for cluster interpretability
7. **Cluster Interpretation** – Mean values per cluster + geological insight
8. **Productivity Analysis** – Boxplot of EUR by cluster
