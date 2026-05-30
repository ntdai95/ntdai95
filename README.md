# Tan Dai Ngo

**Machine Learning Engineer · Software Engineer · Applied Data Scientist**

M.Eng. Applied Data Science @ University of Victoria
M.S. Computer Science @ University of Chicago
B.S. Economics @ University of Washington

---

## Technical Stack

**Languages:** Python · Java · Go · SQL · R

**Machine Learning:** XGBoost · CatBoost · scikit-learn · PyTorch · MLflow · Optuna · Pandas · NumPy

**Distributed Systems & Data:** Apache Spark · PySpark · Kafka · Cassandra · MongoDB · MySQL · Neo4j

**ML Infrastructure & Deployment:** FastAPI · Docker · AWS (EC2, S3) · Sentence Transformers · Qdrant · Ollama

---

## Featured Projects

### [Distributed Ocean Data ML Platform with RAG](https://github.com/ntdai95/Resume-Projects/tree/main/Distributed%20Ocean%20Data%20ML%20Platform%20with%20RAG)
End-to-end distributed ML system processing 10M+ ocean sensor observations from NOAA and ONC.

- Bronze → Silver → Gold Spark architecture for large-scale ETL
- XGBoost forecasting with chronological holdout validation on temporally correlated data
- Production RAG system using Sentence Transformers, Qdrant, and Ollama
- FastAPI inference and retrieval services with benchmarked performance

**Results:** RMSE 0.00586 · R² 0.9999 · Retrieval hit@k 1.0 · Term recall 0.875

**Stack:** Python · Apache Spark · XGBoost · MLflow · FastAPI · Qdrant · Ollama · Docker · AWS

---

### [Anomaly Detection via Isolation Forest on 1M+ Bird Observations](https://github.com/ntdai95/CSC502-Final-Project)
Custom Isolation Forest implementation on the eBird dataset — 1,093,203 real-world observations across British Columbia.

- From-scratch Python implementation with PySpark data processing
- Stratified sampling preserving species frequency distribution across 8 quantile bins
- Discovered a previously undescribed geographic variant of feature-specific swamping
- Proposed rank transformation and density-aware subsampling as mitigation strategies

**Results:** AUC 0.67 · Linear runtime scaling confirmed across full hyperparameter grid

**Stack:** Python · PySpark · Apache Spark · scikit-learn · Matplotlib

---

### [Fuel Blending ML System — Shell.ai Hackathon 2025](https://github.com/ntdai95/Shell.ai-Hackathon-2025)
Production ML system for multi-output regression across 10 chemical blend properties.

- Benchmarked XGBoost vs CatBoost using 5-fold cross-validation
- Feature engineering with entropy-based mixture metrics and weighted aggregation
- Production inference API deployed on AWS EC2

**Results:** CatBoost MAPE 0.64 vs XGBoost MAPE 1.29

**Stack:** Python · CatBoost · XGBoost · FastAPI · Docker · AWS EC2

---

### [Parallel Image Processing Engine](https://github.com/ntdai95/Resume-Projects/tree/main/Parallel%20Image%20Processing%20Engine)
High-performance image processing engine in Go with multiple concurrency models.

- Implemented sequential, fan-in/fan-out pipeline, and BSP execution models
- Custom 2D convolution kernels for grayscale, sharpening, blurring, edge detection
- 20% runtime reduction with fan-in/fan-out · 30% reduction with BSP model

**Stack:** Go · goroutines · channels · sync.WaitGroup

---

## Connect

[LinkedIn](https://linkedin.com/in/ntdai95) · [Portfolio](https://ntdai95.github.io) · ngotandai95@gmail.com
