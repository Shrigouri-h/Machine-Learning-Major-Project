# Unsupervised Machine Learning Major Project
# Smart Traffic Clustering System

## Overview
This project applies unsupervised machine learning to identify hidden patterns in urban traffic behaviour and uncover distinct congestion profiles across road segments and time periods — entirely without labelled data.

## GitHub Repository
[View on GitHub](https://github.com/your-username/your-repo-name)

---

## Problem Statement
Urban traffic congestion causes economic losses, increased emissions, and longer commute times. Traditional systems rely on fixed signal timings and manual monitoring. This project uses large-scale traffic sensor data to automatically detect congestion patterns and flag anomalous events.

## Objectives
- Analyse urban traffic patterns across road segments and time periods
- Identify hidden traffic groups using unsupervised clustering
- Interpret clusters as congestion risk profiles
- Detect anomalous traffic events using outlier detection
- Visualise spatial and temporal patterns

## Dataset
- Source: Kaggle — All Features Traffic Dataset
- Size: 61,368 rows × 30 features | 2018–2024
- Key features: traffic volume, density, speed, travel time, weather conditions, traffic incidents, peak hour indicators, emission levels, road segment IDs, signal phase duration

## Technologies Used
Python, Pandas, NumPy, Matplotlib, Seaborn, Scikit-learn, Plotly, SciPy — run via Google Colab / Jupyter Notebook

---

## Methodology

### 1. Data Collection and Understanding
- Loaded and inspected the dataset; checked for missing values and data types
- Excluded Incidents_or_Events (70% missing) in favour of Traffic_Incidents

### 2. Preprocessing and Feature Engineering
- Ordinal encoding for categorical variables; cyclic sine/cosine for hour and day
- Composite risk score from incident severity, density, and weather
- Flow efficiency computed as speed relative to volume
- All 13 features standardised using StandardScaler

### 3. Dimensionality Reduction
- PCA applied for 2D/3D visualisation; scree plot used to identify components explaining 90% of variance

### 4. Clustering Models
- K-Means on full dataset; optimal K via Elbow, Silhouette, and Davies-Bouldin scores
- DBSCAN for density-based clustering and noise detection
- Agglomerative Hierarchical Clustering on a stratified 5,000-row sample

### 5. Anomaly Detection
- LOF (5% contamination) combined with DBSCAN noise points for a unified anomaly flag
- Approximately 5–10% of records identified as anomalous

### 6. Visualisation
- PCA scatter plots, radar/spider charts, temporal heatmaps, monthly trends, cluster size distributions

---

## Observations
- The dataset was clean with no missing values in core numerical columns, enabling direct use of all 61,368 records.
- PCA showed that a small number of components explain 90% of variance, confirming the engineered features carry strong signal.
- K-Means produced well-balanced cluster sizes with the highest Silhouette and Calinski-Harabasz scores among all algorithms tested.
- DBSCAN noise points were concentrated in high-congestion records, validating that anomalies align with genuine traffic stress events.
- Agglomerative Clustering showed strong agreement with K-Means (high ARI), confirming cluster stability across methods.
- Traffic density peaks sharply during morning (7–9 AM) and evening (5–8 PM) on weekdays; late-night periods are dominated by free-flow clusters.
- Weather conditions such as rain and snow correlate with elevated risk scores and higher anomaly rates.

---

## Cluster Interpretation
Clusters were ranked by average Traffic Density and assigned semantic labels:

- **Free Flow** — very low density, high speed, mostly late-night/early-morning. Managed well with green-wave signal timing.
- **Light Traffic** — low density, minor slowdowns, typical on weekends and off-peak hours.
- **Moderate** — transitional state where weather sensitivity begins; early adaptive signal intervention can prevent escalation.
- **Heavy Traffic** — peak-hour driven with elevated emissions; benefits from staggered work hours and real-time rerouting.
- **Severe Congestion** — persistent bottlenecks with high risk scores; requires adaptive signal control and active monitoring.
- **Gridlock** — full flow breakdown with the highest anomaly rate; needs real-time incident response and emergency signal overrides.

---

## Key Findings
- High traffic density and low speed strongly associate with higher-risk clusters.
- Peak hours show significantly different cluster compositions versus off-peak hours.
- K-Means outperformed DBSCAN and Agglomerative Clustering on Silhouette and Davies-Bouldin metrics.
- Clear congestion profiles were identified with no labelled ground truth.

---

## Conclusion
The Smart Traffic Clustering System demonstrates that unsupervised learning can extract meaningful, stable, and operationally useful congestion profiles from raw sensor data. K-Means delivered the best cluster quality, validated by Agglomerative Clustering and DBSCAN. The anomaly detection layer adds a practical early-warning capability for traffic operators, forming a solid foundation for intelligent, data-driven urban traffic management.

---

## Real-World Implications
- Supports adaptive signal timing and real-time rerouting
- Useful for traffic control centres to prioritise interventions
- Applicable in highway monitoring and incident response planning
- Helps identify congestion hotspots to reduce emissions proactively

## Limitations
- Sensor data may contain measurement errors
- No expert-labelled ground truth for cluster validation
- Agglomerative Clustering limited to a 5,000-row sample due to memory constraints
- No geographic coordinates — map-based visualisation is not possible
- Results are sensitive to feature selection and parameter choices

## Future Work
- Incorporate real-time streaming traffic data
- Apply deep learning models for pattern detection
- Validate clusters with expert traffic engineer feedback
- Integrate weather forecasts for predictive congestion modelling

## Ethical Considerations
- Anonymise road user data to protect privacy
- Use models as decision-support tools, not fully automated systems
- Prevent misclassification of normal traffic as high risk
- Consider equity impacts of rerouting decisions on local communities

## How to Run
1. Open the project in Google Colab or Jupyter Notebook
2. Upload `all_features_traffic_dataset.csv` to the session
3. Run all cells sequentially from top to bottom
4. Output files are saved automatically in the same directory

## Output
- `traffic_clustering_results.csv` — clustered dataset with labels and anomaly flags
- `model_evaluation.csv` — algorithm performance metrics
- 13 visualisation plots saved as PNG files

## Authors
Group Project — Unsupervised Machine Learning

1. Shrigouri Hooli
2. Anu C S
3. Roman Pena
4. Deepak Rajesh
5. A. Harini Goud
