# Tan Dai Ngo

**Applied Data Scientist · Machine Learning Engineer · Software Engineer**<br>
Victoria, BC · [LinkedIn](https://linkedin.com/in/ntdai95) · [Portfolio](https://ntdai95.github.io) · ngotandai95@gmail.com

Nearly two years at T-Mobile building REST services in Java and Spring Boot, alongside Kafka and Cassandra. Now in a graduate co-op program, mostly working on detection models and the pipelines underneath them.

I'm interested in whether a result holds up. On my graduate capstone that meant proving our own benchmark leaked, and reporting that the honest score fell to **about a quarter** of where we'd started.

**Available from January to December 2027** for a co-op or internship term. Valid Canadian co-op work permit.

---

## At a Glance

| Project | What it is | Headline result |
|---|---|---|
| [**IoT Intrusion Detection**](https://github.com/ntdai95/ECE592B-Capstone-Project) | Two-stage detector, unsupervised → supervised | 99.6% recall at 0.82% FPR **and proof the benchmark leaked** |
| [**Distributed Ocean Data ML Platform with RAG**](https://github.com/ntdai95/Resume-Projects) | 10M+ sensor records, Spark → forecasting → RAG | Retrieval hit@k 0.9, term recall 0.85 |
| [**Facility Reservation System**](https://github.com/ntdai95/Resume-Projects) | REST service interoperating with 4 peer teams | 27 versioned endpoints, 71 pytest tests |
| [**Anomaly Detection at Scale**](https://github.com/ntdai95/CSC502-Final-Project) | Isolation Forest written from the paper | 1,093,203 records, linear scaling verified |
| [**Parallel Image Engine**](https://github.com/ntdai95/Resume-Projects) | Three concurrency models in Go | 30% runtime reduction (BSP) |

---

## Technical Stack

| | |
|---|---|
| **Languages** | Python · Java · Go · SQL |
| **Machine Learning** | PyTorch · scikit-learn · XGBoost · CatBoost · MLflow · Optuna · pandas · NumPy |
| **NLP & Retrieval** | Sentence Transformers · DistilBERT · Qdrant · Ollama · RAG |
| **Data at Scale** | Apache Spark · PySpark · Kafka · Cassandra · MySQL · SQLite · MongoDB · Neo4j |
| **Services & Deploy** | FastAPI · Flask · Spring Boot · Docker · AWS (EC2, S3) · Jenkins |
| **Practice** | Git · pull requests · code review · pytest · OpenAPI |

---

## Education

**M.Eng. Applied Data Science**, University of Victoria – Sep 2025 – Dec 2027<br>
**M.S. Computer Science**, University of Chicago – Sep 2020 – Mar 2022<br>
**B.S. Economics**, University of Washington – Sep 2015 – Aug 2019

---

## Featured Work

### [Multi-Stage IoT Intrusion Detection](https://github.com/ntdai95/ECE592B-Capstone-Project)
*Graduate capstone · team of 7 · Python, PyTorch, XGBoost*

Two-stage detector on CIC IoT-DIAD 2024. Stage one scores packets with k-means and an autoencoder, Deep SVDD, and an Anomal-E edge-feature GNN, fused into a single score. Stage two is a supervised flow classifier that consumes it. Six models compared under a hard **1% false-positive budget**, best being multiclass XGBoost at **99.6% recall, 0.82% FPR, PR-AUC 0.995**.

**The benchmark leaks capture-session identity.** Benign traffic was recorded on two days while each attack class occupies its own — the same threshold that holds 1% FPR on one capture day costs over 30% on another. I ran a four-condition holdout to isolate it. Under an honest session-disjoint split, PR-AUC falls **0.995 → 0.242**, and holding recall costs over **34% FPR**, roughly thirty-four times the budget. What fails first is calibration, not ranking.

**My contribution:** the leakage discovery, the four-condition experiment, and `verify_context_integrity.py`, which confirms all 23 engineered features stay causal, label-free and inside the budget.

---

### [Distributed Ocean Data ML Platform with RAG](https://github.com/ntdai95/Resume-Projects/tree/main/Distributed%20Ocean%20Data%20ML%20Platform%20with%20RAG)
*Solo · Python, Spark, XGBoost, MLflow, Optuna, Qdrant, FastAPI, Docker*

A platform over **10M+ ocean and weather sensor observations** from NOAA and ONC, two agencies whose NetCDF formats don't agree on much.

- Bronze → Silver → Gold Spark layers for large-scale ETL
- XGBoost forecasting validated on **chronological** holdouts, not random splits, since the series is temporally correlated
- Retrieval over dataset metadata with Sentence Transformers, Qdrant and Ollama, running locally end to end
- MLflow for experiment tracking, Optuna for hyperparameter search, FastAPI and the vector store containerized with Docker Compose

**Retrieval scored against a held-out query set of 10 natural-language questions: hit@k 0.9, term recall 0.85.**

A naive persistence baseline (predict = previous reading) beats the tuned XGBoost model on raw RMSE. Expected for a high-frequency, smooth signal, and the reason this section reports both numbers rather than the model's R² alone. Extended the check across seven horizons out to 2 hours and a version with sensor context added (salinity, dissolved oxygen) — persistence won every horizon, and XGBoost's R² went negative past 30 minutes, the signature of a model overfitting training-period noise rather than learning real drift.

**Ran the same benchmark, as a control, on a signal from the same ONC network that should be forecastable.** Air temperature from ONC's Baynes Sound weather station has an obvious deterministic driver (the daily solar cycle) that persistence can't anticipate. There, XGBoost wins decisively from 3-12 hours out — persistence's R² actually goes negative at 6 and 12 hours, while XGBoost cuts RMSE by up to 48% at the 12-hour mark. Same pipeline, same evaluation, opposite result on the right kind of signal.

---

### [Distributed Facility Reservation System](https://github.com/ntdai95/Resume-Projects)
*Applied Software Engineering · team of 4 · Python, FastAPI, SQLite, pytest*

A booking service that had to interoperate with **four other teams' independent implementations** of one shared HTTP contract that nobody could change unilaterally.

- **27 versioned `/v1/` endpoints** with published OpenAPI documentation
- **71 pytest tests** across the API, database and reservation-rules layers, run on every change
- Session tokens checked for existence, one-hour freshness and permission scope
- 847-line SQLite layer over four tables enforcing rules on funds and availability

---

### [Anomaly Detection on 1M+ Species Observations](https://github.com/ntdai95/CSC502-Final-Project)
*Systems for Massive Datasets · team of 3 · Python, PySpark, scikit-learn*

Isolation Forest implemented **from the published algorithm rather than imported**, on 1,093,203 eBird observations across British Columbia.

- From-scratch Python implementation with PySpark processing
- Stratified sampling across eight quantile bins, preserving species frequency distribution
- **Identified a previously undescribed geographic variant of feature-specific swamping**, and proposed rank transformation and density-aware subsampling as mitigations

**AUC 0.67, with linear runtime scaling verified across the hyperparameter grid.**

---

### [Parallel Image Processing Engine](https://github.com/ntdai95/Resume-Projects/tree/main/Parallel%20Image%20Processing%20Engine)
*Solo · Go, goroutines, channels, sync.WaitGroup*

Image convolution engine with three execution models: sequential, a fan-in/fan-out pipeline, and bulk-synchronous parallel. Custom 2D kernels for grayscale, sharpen, blur and edge detection.

**20% runtime reduction with fan-in/fan-out, 30% with BSP.**
