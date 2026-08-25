# Tan Dai Ngo

**Applied Data Scientist · Machine Learning Engineer · Software Engineer**

- M.Eng. Applied Data Science, University of Victoria (Co-op, Sep 2025 – Dec 2027)
- M.S. Computer Science, University of Chicago
- B.S. Economics, University of Washington

Two years at T-Mobile building REST services in Java and Spring Boot, alongside Kafka and Cassandra, before returning to graduate school. Most of what I work on now sits somewhere between detection models and the pipelines underneath them, and the part I care about is whether a result survives being checked.

---

## Technical Stack

**Languages:** Python · Java · Go · SQL
**Machine Learning:** PyTorch · scikit-learn · XGBoost · CatBoost · pandas · NumPy · MLflow · Optuna · Sentence Transformers · DistilBERT
**Data at Scale:** Apache Spark · PySpark · Kafka · Cassandra · MySQL · SQLite · MongoDB · Neo4j · Qdrant
**Services & Deployment:** FastAPI · Flask · Spring Boot · Docker · AWS (EC2, S3) · Ollama
**Practice:** Git · GitHub pull requests · code review · pytest · OpenAPI

---

## Featured Projects

### [Multi-Stage IoT Intrusion Detection](https://github.com/ntdai95/ECE592B-Capstone-Project)

Two-stage detector on CIC IoT-DIAD 2024: unsupervised packet scoring feeding a supervised flow classifier. Graduate capstone, team of seven.

- Six models compared under a hard 1% false-positive budget — k-means with autoencoder, Deep SVDD, Anomal-E edge-feature GNN, score fusion, then supervised classification
- 23 causal connection-window features, audited to confirm each stays label-free and inside the budget
- **Found the benchmark leaks capture-session identity.** Benign traffic was recorded on two days while each attack class occupies its own; capture window is predictable from flow features alone at ROC-AUC 0.922
- Ran a four-condition holdout to isolate it: under an honest session-disjoint split, PR-AUC falls 0.927 → 0.630, and holding recall costs 32% FPR

**Best result:** multiclass XGBoost at 92.5% recall, 0.96% FPR, PR-AUC 0.944.
**My contribution:** the leakage discovery, the four-condition experiment, and the feature-integrity audit.
**Stack:** Python · PyTorch · XGBoost · scikit-learn

---

### [Ocean Data Platform with Retrieval-Augmented Search](<https://github.com/ntdai95/Resume-Projects/tree/main/Distributed%20Ocean%20Data%20ML%20Platform%20with%20RAG>)

End-to-end platform over 10M+ ocean sensor observations from NOAA and ONC, built solo.

- Bronze → Silver → Gold Spark layers harmonizing two agencies with incompatible NetCDF formats
- XGBoost forecasting validated on chronological holdouts rather than random splits, since the series is temporally correlated
- Retrieval over dataset metadata with Sentence Transformers, Qdrant and Ollama, running locally end to end
- FastAPI serving for both paths, MLflow for experiment tracking and Optuna for hyperparameter search, containerized so any run reproduces from scratch

**Retrieval evaluated against a held-out query set:** hit@k 1.0, term recall 0.875.
**Stack:** Python · Apache Spark · XGBoost · MLflow · Optuna · Qdrant · Sentence Transformers · Ollama · FastAPI · Docker · AWS

---

### [Distributed Facility Reservation System](https://github.com/ntdai95/Resume-Projects)

Booking service that had to interoperate with four other teams' independent implementations of one shared contract. Graduate software engineering course, team of four.

- 27 versioned `/v1/` REST endpoints with published OpenAPI documentation
- 71 pytest tests across the API, database and reservation-rules layers, run on every change
- Session tokens checked for existence, one-hour freshness and permission scope
- 847-line SQLite layer over four tables enforcing rules on funds and availability

Nobody could change the contract unilaterally, which is a fast way to learn that an unwritten assumption is a defect.
**Stack:** Python · FastAPI · SQLite · pytest

---

### [Anomaly Detection on 1M+ Species Observations](https://github.com/ntdai95/CSC502-Final-Project)

Isolation Forest implemented from the published algorithm rather than imported, on 1,093,203 eBird observations across British Columbia. Team of three.

- From-scratch Python implementation with PySpark processing
- Stratified sampling across eight quantile bins, preserving species frequency distribution
- Identified a previously undescribed geographic variant of feature-specific swamping
- Proposed rank transformation and density-aware subsampling as mitigations

**Results:** AUC 0.67, with linear runtime scaling verified across the hyperparameter grid.
**Stack:** Python · PySpark · scikit-learn · Matplotlib

---

### [Parallel Image Processing Engine](<https://github.com/ntdai95/Resume-Projects/tree/main/Parallel%20Image%20Processing%20Engine>)

Image convolution engine in Go with three execution models, built solo.

- Sequential, fan-in/fan-out pipeline, and bulk-synchronous parallel implementations
- Custom 2D kernels for grayscale, sharpen, blur and edge detection
- 20% runtime reduction with fan-in/fan-out, 30% with BSP

**Stack:** Go · goroutines · channels · sync.WaitGroup

---

## Connect

[LinkedIn](https://linkedin.com/in/ntdai95) · [Portfolio](https://ntdai95.github.io) · ngotandai95@gmail.com
