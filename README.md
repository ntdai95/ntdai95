# Tan Dai Ngo

**Applied Data Scientist · Machine Learning Engineer · Software Engineer**<br>
Victoria, BC · [LinkedIn](https://linkedin.com/in/ntdai95) · [Portfolio](https://ntdai95.github.io) · ngotandai95@gmail.com

Nearly two years at T-Mobile building REST services in Java and Spring Boot, alongside Kafka and Cassandra. Now in a graduate co-op program, mostly working on detection models and the pipelines underneath them.

I'm interested in whether a result holds up. On my graduate capstone that meant proving our own benchmark leaked, and reporting that the honest score was **a third worse** than the one we'd started with.

**Available January to December 2027** for a co-op or internship term. Valid Canadian co-op work permit.

---

## At a Glance

| Project | What it is | Headline result |
|---|---|---|
| [**IoT Intrusion Detection**](https://github.com/ntdai95/ECE592B-Capstone-Project) | Two-stage detector, unsupervised → supervised | 92.5% recall at 0.96% FPR **and proof the benchmark leaked** |
| [**Ocean Data Platform**](https://github.com/ntdai95/Resume-Projects) | 10M+ sensor records, Spark → forecasting → RAG | Retrieval hit@k 1.0, term recall 0.875 |
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

Two-stage detector on CIC IoT-DIAD 2024. Stage one scores packets with k-means and an autoencoder, Deep SVDD, and an Anomal-E edge-feature GNN, fused into a single score. Stage two is a supervised flow classifier that consumes it. Six models compared under a hard **1% false-positive budget**, best being multiclass XGBoost at **92.5% recall, 0.96% FPR, PR-AUC 0.944**.

**The benchmark leaks capture-session identity.** Benign traffic was recorded on two days while each attack class occupies its own, so the capture window is predictable from flow features alone at **ROC-AUC 0.922**. I ran a four-condition holdout to isolate it. Under an honest session-disjoint split, PR-AUC falls **0.927 → 0.630**, and holding recall costs **32% FPR**, thirty-two times the budget. What fails first is calibration, not ranking.

**My contribution:** the leakage discovery, the four-condition experiment, and `verify_context_integrity.py`, which confirms all 23 engineered features stay causal, label-free and inside the budget.

---

### [Ocean Data Platform with Retrieval-Augmented Search](https://github.com/ntdai95/Resume-Projects/tree/main/Distributed%20Ocean%20Data%20ML%20Platform%20with%20RAG)
*Solo · Python, Spark, XGBoost, MLflow, Optuna, Qdrant, FastAPI, Docker, AWS*

A platform over **10M+ ocean sensor observations** from NOAA and ONC, two agencies whose NetCDF formats don't agree on much.

- Bronze → Silver → Gold Spark layers for large-scale ETL
- XGBoost forecasting validated on **chronological** holdouts, not random splits, since the series is temporally correlated
- Retrieval over dataset metadata with Sentence Transformers, Qdrant and Ollama, running locally end to end
- MLflow for experiment tracking, Optuna for hyperparameter search, FastAPI serving both paths, containerized so any run reproduces

**Retrieval scored against a held-out query set: hit@k 1.0, term recall 0.875.**<br>
I built the evaluation set first, before the retrieval was working.

---

### [Distributed Facility Reservation System](https://github.com/ntdai95/Resume-Projects)
*Applied Software Engineering · team of 4 · Python, FastAPI, SQLite, pytest*

A booking service that had to interoperate with **four other teams' independent implementations** of one shared HTTP contract that nobody could change unilaterally.

- **27 versioned `/v1/` endpoints** with published OpenAPI documentation
- **71 pytest tests** across the API, database and reservation-rules layers, run on every change
- Session tokens checked for existence, one-hour freshness and permission scope
- 847-line SQLite layer over four tables enforcing rules on funds and availability

A good number of those tests exist because another team's service did something we hadn't anticipated.

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
