# Customer Segmentation and Churn Prediction with LightGBM

This repository contains a complete *machine learning* pipeline developed for a real-world **bank customer churn prediction** problem, originally created for the competitive challenge **Data Mining in Economics and Finance (DMEyF) 2024**.

The solution evolved through multiple competitive stages, scaling from small datasets to processing **two full years of information on Google Cloud Platform (GCP)**.

The project presents an advanced workflow that integrates **unsupervised customer segmentation** with a robust supervised approach based on model ensembling to predict churn, using **LightGBM** as the main algorithm.

---

## 🧠 Methodology and Key Technical Aspects

### 1. Advanced Customer Segmentation

The *clustering* process was not based on raw variables, but on a **proximity matrix derived from Random Forest**, designed to capture non-linear and complex relationships between customers.

- **Proximity Matrix Calculation:**  
  A custom function (`distanceMatrix`) computed pairwise similarities based on the terminal nodes in which customers landed across all trees of the Random Forest model. This matrix served as a learned distance metric.

- **Dimensionality Reduction:**  
  The high-dimensional matrix was reduced to 2D embeddings using **UMAP**, chosen for its ability to preserve both local and global data structure, outperforming alternatives such as *t-SNE*.

- **Clustering:**  
  The resulting embeddings were clustered with **DBSCAN**, which identified dense regions of customers without assuming spherical shapes, uncovering differentiated behavioral segments.

<img width="841" height="547" alt="Cluster DBSCAN" src="https://github.com/user-attachments/assets/faac1b03-bd31-4f0b-896b-68ba8cc30871" />


#### Description of the 5 Customer Groups

The clustering process revealed five distinct customer profiles with very different behaviors and value for the bank. Characterizing each group enables the design of specific and efficient retention strategies:

- **Cluster 1: Inactive Customers**  
  Characterized by **total financial inactivity** (no transfers, no card usage, and near-zero balances). They generate no profitability and probably used the account as a secondary product.  
  **Recommendation:** evaluate whether to invest resources in their retention, prioritizing higher-value profiles.

- **Cluster 0: Salary Receivers**  
  All customers in this segment received their salary the month prior to churn, suggesting they are **employees in formal jobs** who likely changed employer and bank.  
  **Recommendation:** implement banking portability strategies or competitive offers during the transition to retain them.

- **Cluster 4: High-Value Customers**  
  This is the **most critical profile to retain**. They do not receive salaries but maintain **high balances** (in pesos, dollars, or both), indicating strong financial capacity (possibly small business owners or investors). Losing them represents a significant drop in profitability.  
  **Recommendation:** develop proactive and personalized strategies, such as premium financial advisory, exclusive products, and direct communication to better understand their needs.

- **Clusters 2 & 3: Active Customers with Potential**  
  Both groups show **high transactional activity and intensive credit card use** (with higher limits in Cluster 3). They do not receive salaries, so they may be **self-employed or freelancers**. They generate growing profitability and deserve attention.  
  **Recommendation:** deepen the analysis to identify specific churn drivers and design offers that increase engagement and loyalty.

---

### 2. Churn Prediction

The supervised workflow was designed to **maximize performance and generalization**:

- **Algorithm Selection:**  
  **LightGBM** was chosen for its speed, efficiency on large datasets, and native ability to handle missing values without prior imputation (avoiding biases from methods like *MICE* or *KNN*).

- **Feature Engineering:**  
  A key factor in performance. New features were generated from detailed temporal analysis of customer behavior, which significantly improved model accuracy.

- **Hyperparameter Optimization:**  
  Conducted with **Optuna**, leveraging Bayesian search, which is more efficient than *GridSearch* for finding superior and robust configurations.

- **Model Robustness and Temporal Validation:**  
  - **Seed Ensembling (Voting):** multiple models were trained with different seeds and their predictions averaged (*soft voting*) to mitigate training randomness, producing more stable and generalizable results.  
  - **Temporal Backtesting:** the model was rigorously validated with out-of-time splits to simulate real-world deployment and ensure consistency under temporal drift, a critical step often overlooked.

---

## 🛠️ Tech Stack

- **Language:** Python  
- **ML Frameworks:** LightGBM, Scikit-learn, XGBoost  
- **Unsupervised Learning:** UMAP, DBSCAN, Scikit-learn  
- **Hyperparameter Optimization:** Optuna  
- **Data Handling & Computing:** Pandas, NumPy, Google Cloud Platform (GCP)  
- **Visualization:** Matplotlib, Seaborn

## Kaggle Competitions

[DM EYF 2024 - Primera](https://www.kaggle.com/competitions/dm-ey-f-2024-primera/leaderboard)  

[DM EYF 2024 - Segunda](https://www.kaggle.com/competitions/dm-ey-f-2024-segunda)  

[DM EYF 2024 - Tercera](https://www.kaggle.com/competitions/dm-ey-f-2024-tercera)  
