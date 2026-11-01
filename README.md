# Financial Inclusion under PMJDY: Clustering States by Account Uptake and Usage

**Student:** Nancy Singh

## Project overview
This project explores state/UT-level variation in Pradhan Mantri Jan-Dhan Yojana (PMJDY) indicators using feature engineering, K-Means clustering and Principal Component Analysis (PCA). The unit of analysis is a state or Union Territory; the analysis does not make individual-level claims.

## Data
The project uses the state-wise PMJDY statistics table published on the [official PMJDY website](https://pmjdy.gov.in/statewise-statistics). A cleaned snapshot is stored in `PMJDY_Statewise_Cleaned.csv` so the notebook can run without scraping the website on every execution.

The dataset contains 36 state/UT rows. The source snapshot date should be recorded when the data is refreshed.

## Methodology
1. Load the committed cleaned CSV from this repository.
2. Convert numeric fields, remove summary rows and duplicate state/UT names, and check whether rural plus urban beneficiaries equal reported total beneficiaries.
3. Engineer the following indicators:
   - Rural and urban beneficiary shares.
   - Average account balance per beneficiary (rupees), calculated from the balance reported in crore.
   - RuPay cards issued per 100 beneficiaries. This is an issuance indicator, not a verified card-ownership or usage rate.
4. Apply a log transformation to total beneficiaries and standardize the four clustering features.
5. Compare K-Means solutions for K = 2 to 6 using inertia and silhouette score. The notebook uses K = 4 for the final exploratory segmentation; interpret the silhouette score and cluster separation cautiously.
6. Use PCA to project the standardized features into two dimensions for visualization.
7. Summarize each cluster and export tables and charts.

## Repository files
- `PMJDY_Financial_Inclusion.ipynb` — complete analysis notebook.
- `PMJDY_Statewise_Cleaned.csv` — cleaned input data.
- `PMJDY_Clustered_States.csv` — state/UT records with engineered features, cluster labels and PCA coordinates (regenerate after running the notebook).
- `PMJDY_Cluster_Profiles.csv` — cluster-level summary (regenerate after running the notebook).
- `PMJDY_KMeans_Clusters.png` — PCA cluster plot.
- `PMJDY_Rural_Share_by_Cluster.png` — rural beneficiary share chart.
- `PMJDY_Balance_by_Cluster.png` — average balance chart.

## Run in Google Colab
1. Open `PMJDY_Financial_Inclusion.ipynb` from this repository in Google Colab.
2. Choose **Runtime → Run all**.
3. The notebook loads the committed CSV from GitHub. If that download is unavailable, it asks you to upload `PMJDY_Statewise_Cleaned.csv`.
4. After execution, download the generated CSVs and PNG charts from the Colab Files panel (or run the optional final download cell).
5. If you want the repository's output files to match the latest run, upload the regenerated CSVs and PNGs to GitHub.

## Limitations
- This is a cross-sectional, aggregate state/UT-level analysis; it cannot establish causation or describe every account holder's experience.
- K-Means cluster numbers are arbitrary labels, not rankings.
- A modest silhouette score indicates that groups may overlap; the selected K should be treated as an exploratory segmentation, not a definitive classification.
- RuPay cards issued per 100 beneficiaries does not measure actual card activation, usage or unique ownership.
- Results depend on the date and completeness of the official data snapshot. Record the data access/update date whenever the dataset is refreshed.
