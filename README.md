# Crime Clustering in Kelantan

**Author:** MD ZIHADUL AHSAN RATUL  
**Project type:** Unsupervised machine learning / exploratory data analysis  
**Location focus:** Kelantan, Malaysia  
**Algorithms:** K-Means, Hierarchical (Agglomerative) Clustering and DBSCAN  
**Environment:** Google Colab / Python

## Overview

This project explores district-level crime patterns in Kelantan, Malaysia, using unsupervised machine-learning techniques. It combines data cleaning and exploratory data analysis with three clustering approaches to group districts by their crime-category profiles and examine potential outliers.

The notebook includes:
- Data cleaning, validation and formatting
- Exploratory data analysis (EDA)
- K-Means clustering
- Hierarchical clustering
- DBSCAN-based anomaly detection
- Silhouette-score evaluation and cluster visualizations
- PCA-based two-dimensional visualizations

## Dataset

The notebook loads a CSV file named:

`Kelantan_Crime_Statistic.csv`

The CSV was not included with the uploaded notebook. The notebook does not provide a direct download URL, publisher citation or licence statement. See [DATASET.md](DATASET.md) for the required file and expected structure. Do not publish the dataset unless its source and redistribution terms permit it.

## Project workflow

### 1. Data cleaning

The notebook's cleaning section includes:
- Checking duplicate records
- Inspecting categorical and numerical column types
- Counting unique categorical values
- Calculating missing-value percentages
- Dropping the `state` column
- Inspecting outliers with box plots
- Calculating outlier boundaries and removing outliers
- Imputing missing values
- Rechecking outlier bounds
- Validating and formatting data

### 2. Data preprocessing

The notebook converts the `date` field to datetime and extracts a `year` feature. It also demonstrates:
- Min-Max normalization
- Standardization with `StandardScaler`
- One-hot encoding for selected categorical features

### 3. Exploratory data analysis

EDA includes analysis and visualizations such as:
- Crime distributions by category and district
- Average crime counts by district
- Crime totals by district and year
- Histograms and skewness of numerical features
- Swarm, violin and box plots
- Pair plots
- Correlation heatmaps
- Year-wise district comparisons

### 4. K-Means clustering

The notebook pivots the data into a district-by-crime-category matrix, sums crime counts by category, fills missing combinations with zero and standardizes the resulting features.

It then:
- Tests K values from 1 to 10 using the elbow method and WCSS.
- Sets `optimal_k = 3` based on the notebook's stated elbow-plot assumption.
- Fits K-Means using `k-means++`, `random_state=42` and `n_init=10`.
- Assigns cluster labels to districts.
- Visualizes clusters and centroids.
- Calculates a silhouette score.

**Important:** The notebook text says K=3 is assumed from the elbow graph. Treat this as the selected setting in the supplied experiment, not as a universally established optimum.

### 5. Hierarchical clustering

The notebook applies Ward-linkage agglomerative clustering with three clusters. It includes:
- Standardized district feature matrix
- Ward dendrogram
- District cluster assignments
- Cluster-size counts
- Silhouette-score evaluation
- PCA visualization
- Cluster profiling and a cluster-profile heatmap

### 6. DBSCAN anomaly detection

The notebook tests combinations of:
- `eps`: 1.0, 1.2, 1.5, 1.8 and 2.0
- `min_samples`: 2, 3 and 4

It records the resulting number of clusters and noise points for each combination. The final DBSCAN configuration is `eps=1.5` and `min_samples=2`. Points assigned label `-1` are identified as noise/anomalies and visualized using PCA coordinates.

## Repository structure

```text
.
├── crime_clustering_kelantan.ipynb
├── README.md
├── DATASET.md
├── requirements.txt
├── .gitignore
└── LICENSE
```

## Run in Google Colab

1. Open Google Colab.
2. Upload `crime_clustering_kelantan.ipynb`.
3. Upload `Kelantan_Crime_Statistic.csv` to the Colab working directory.
4. Run the notebook sequentially from the beginning.
5. Review the EDA plots, cluster assignments, silhouette scores and DBSCAN noise points.

## Run locally

Use Python 3.10 or 3.11 where possible.

```bash
python -m venv .venv
```

Activate the environment and install the dependencies:

```bash
pip install -r requirements.txt
```

Launch Jupyter:

```bash
jupyter notebook
```

Place `Kelantan_Crime_Statistic.csv` in the notebook's working directory. If the file is elsewhere, update the `pd.read_csv(...)` paths accordingly.

## Interpretation and limitations

- Clustering is exploratory: cluster labels do not represent an official crime-risk rating.
- DBSCAN label `-1` means a point was classified as noise under the selected DBSCAN parameters; it does not prove that a district is objectively abnormal or dangerous.
- Results depend on data coverage, feature selection, scaling, outlier handling and algorithm parameters.
- The notebook uses different preprocessing and feature-construction steps across its K-Means, hierarchical and DBSCAN sections. Compare outputs with that methodological context in mind.
- The notebook includes silhouette scores as evaluation measures, but the source file does not provide a verified fixed summary of the resulting scores. Run the notebook with the dataset to generate them.
- Crime statistics can be sensitive and can be misinterpreted. Avoid stigmatizing districts or communities based on exploratory clusters alone.
- The original notebook is preserved as supplied; this package adds documentation and does not rebuild or independently validate the analysis.
