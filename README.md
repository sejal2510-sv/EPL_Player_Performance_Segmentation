# EPL Player Performance Segmentation

## 📌 Project Overview

This project analyzes English Premier League (EPL) player performance data using **Unsupervised Machine Learning** techniques.

The objective is to identify meaningful groups of players based on their performance statistics, playing time, attacking contribution, and defensive performance.

The project follows a complete machine learning pipeline:

**Data Preprocessing → Standardization → PCA → K-Means Clustering → Cluster Profiling**

The analysis identifies **three distinct player segments** based primarily on attacking output and playing time.

---

## 🎯 Objectives

- Analyze EPL player performance data.
- Explore and preprocess player statistics.
- Standardize numerical features using `StandardScaler`.
- Reduce dimensionality using **Principal Component Analysis (PCA)**.
- Determine a suitable number of clusters using the **Elbow Method** and **Silhouette Score**.
- Apply **K-Means Clustering** to segment players.
- Interpret and profile the resulting player groups.

---

## 📊 Dataset

The dataset contains **476 players and 13 columns**.

### Player Information
- `Player_Name`
- `Club`
- `Position`

### Performance Features
- `Goals_Scored`
- `Assists`
- `Total_Points`
- `Minutes`
- `Goals_Conceded`
- `Creativity`
- `Influence`
- `Threat`
- `Bonus`
- `Clean_Sheets`

No duplicate records were found in the dataset. The numerical variables have different scales, so standardization was performed before applying PCA and clustering.

---

## 🛠️ Technologies Used

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-learn
- Jupyter Notebook / Google Colab

---

## 🤖 Machine Learning Methods

### 1. StandardScaler

The numerical performance variables have different ranges. For example, player minutes can be in the thousands while goals are generally much smaller.

Therefore, `StandardScaler` was used to transform the numerical features to a common scale before further analysis.

### 2. Principal Component Analysis (PCA)

PCA was used to reduce the dimensionality of the 10 numerical performance features.

The first three principal components explain approximately **91.7% of the total variance**:

| Component | Cumulative Variance |
|-----------|--------------------:|
| PC1 | 72.2% |
| PC2 | 85.8% |
| PC3 | 91.7% |

Therefore, **3 principal components** were retained for clustering.

### 3. K-Means Clustering

K-Means clustering was evaluated for different values of `k` from 2 to 10 using:

- Elbow Method
- Inertia
- Silhouette Score

The silhouette score was highest for `k = 2` (0.523), while `k = 3` achieved a very close score of 0.514.

`k = 3` was selected because it provides more meaningful and actionable player segments.

---

## 📈 Clustering Results

The final K-Means model identified **3 player segments**:

| Cluster | Players | Percentage | Player Segment |
|---------|--------:|-----------:|----------------|
| Cluster 0 | 63 | 13.2% | Attacking Threats |
| Cluster 1 | 248 | 52.1% | Fringe / Low-Minute Players |
| Cluster 2 | 165 | 34.7% | Defensive Regulars |

---

## 🔴 Cluster 0 — Attacking Threats

**63 players (13.2%)**

This group contains players with strong attacking performance.

Key characteristics:

- High goals scored
- High assists
- High threat
- High creativity
- High bonus points
- Strong overall point contribution

This cluster is mainly composed of midfielders and forwards.

---

## 🟡 Cluster 1 — Fringe / Low-Minute Players

**248 players (52.1%)**

This is the largest cluster.

Key characteristics:

- Low playing minutes
- Low total points
- Lower influence and attacking statistics
- Mixed player positions

The main characteristic of this group is **limited playing time**, representing players such as squad-depth, rotation, or fringe players.

---

## 🟢 Cluster 2 — Defensive Regulars

**165 players (34.7%)**

This group contains players with relatively high playing time and defensive contributions.

Key characteristics:

- High minutes
- Higher clean-sheet counts
- High influence
- Strong defensive statistics
- Regular playing time

The cluster contains mainly defenders and midfielders, along with some goalkeepers and forwards.

---

## 🔍 Key Findings

- Player segmentation is influenced more by **playing time and attacking output** than by nominal playing position.
- The largest group consists of fringe or low-minute players.
- A smaller group contains players with strong attacking contributions.
- Another major group represents regular players with stronger defensive characteristics.
- PCA reduced the 10-dimensional feature space to 3 components while retaining approximately **91.7% of the total variance**.
- K-Means with `k = 3` produced three interpretable player segments.

---

## ⚠️ Important Modeling Note

During the analysis, the cluster profiling procedure was corrected to ensure that the engineered `Cluster` label was not treated as a performance feature.

The final profiling approach uses **standardized feature values (z-scores)** to compare the characteristics of each cluster fairly.

---

## 🔄 Project Workflow

```text
EPL Player Dataset
        ↓
Data Exploration
        ↓
Data Validation
        ↓
Select Numerical Features
        ↓
StandardScaler
        ↓
Principal Component Analysis (PCA)
        ↓
Select 3 Principal Components
        ↓
Elbow Method + Silhouette Score
        ↓
K-Means Clustering
        ↓
3 Player Segments
        ↓
Cluster Profiling & Interpretation
