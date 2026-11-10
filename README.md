# Tan Dai Ngo

**Software Engineer building ML and data systems**<br>
Victoria, BC · [LinkedIn](https://linkedin.com/in/ntdai95) · [Portfolio](https://ntdai95.github.io) · [Resume](https://ntdai95.github.io/documents/Ngo%20Tan%20Dai%20-%20Resume.pdf) · ngotandai95@gmail.com

I spent nearly two years supporting T-Mobile through BeaconFire Inc., building Java and Spring Boot services backed by Kafka and Cassandra. I returned to graduate school to go deeper into ML and data systems, with recent work in Spark pipelines and deployed inference services.

I'm interested in whether a result holds up. On my graduate capstone that meant proving our own benchmark leaked, and reporting that the honest score fell to **about one-eighth** of where we'd started.

I am **available from January to December 2027** for a co-op or internship term, and I am authorized to work in Canada.

---

## At a Glance

- The [**Ocean Data ML Platform with RAG**](https://github.com/ntdai95/Resume-Projects/tree/main/Ocean%20Data%20ML%20Platform%20with%20RAG) processes 10.8M sensor records through Spark, forecasting, and RAG. Its retrieval benchmark reached hit@k 0.9 and term recall 0.85.
- The [**Multi-Stage IoT Intrusion Detection**](https://github.com/ntdai95/ECE592B-Capstone-Project) combines unsupervised scoring with supervised classification. It reached 99.5% recall at 0.94% FPR and exposed leakage in the benchmark.
- The [**Distributed Facility Reservation System**](https://github.com/ntdai95/Resume-Projects/tree/main/Distributed%20Facility%20Reservation%20System) interoperates with four peer teams through a shared REST contract. It exposes 27 versioned endpoints backed by 71 pytest tests.
- The [**Auction Marketplace Microservices**](https://github.com/ntdai95/Auction-Website) splits the marketplace across six Flask services with isolated databases and durable messaging. Its 14 Docker containers use dependency-ordered startup.
- The [**Anomaly Detection at Scale on Species Data**](https://github.com/ntdai95/CSC502-Final-Project) implements Isolation Forest from the published algorithm. It processed 1,093,203 records and verified linear runtime scaling.
- The [**End-to-End Multi-Output Fuel Blending System**](https://github.com/ntdai95/Shell.ai-Hackathon-2025) deploys multi-output regression through FastAPI. CatBoost reached a MAPE of 0.64 versus XGBoost’s 1.29.

---

## Technical Stack

| | |
|---|---|
| **Languages** | Python · Java · Go · SQL · Cypher · JavaScript |
| **Machine Learning & Statistics** | PyTorch · scikit-learn · XGBoost · CatBoost · Isolation Forest · SVM · kNN · SMOTE · Fairlearn · PennyLane · GARCH · Granger causality |
| **NLP & Retrieval** | Sentence Transformers · DistilBERT · FinTwitBERT · TF-IDF · Qdrant · Ollama · RAG |
| **Data & Graphs** | Apache Spark · PySpark · pandas · NumPy · Kafka · Cassandra · MySQL · SQLite · MongoDB · Neo4j · knowledge graphs |
| **Backend & Systems** | Spring Boot · FastAPI · Flask · REST APIs · microservices · RabbitMQ · Go concurrency · goroutines · channels · bulk synchronous parallelism |
| **Cloud, MLOps & Delivery** | AWS (EC2, S3) · Docker · Docker Compose · MLflow · Optuna · Streamlit · Jenkins · GitHub Actions · CI/CD · OpenAPI · pytest |

---

## Production Experience

**Software Developer, T-Mobile (via BeaconFire Inc.)**<br>
*Bellevue, WA · Jun 2022 - Apr 2024 · Java, Spring Boot, Kafka, Cassandra, Jenkins*

- Developed and maintained REST endpoints across 5+ Roaming Business System microservices in Java and Spring Boot.
- Automated reprocessing of rejected roaming tests with weekly Kafka retries, cutting manual effort by 80%.
- Traced 20+ cross service defects to their root cause and deployed features via Jenkins across 50+ releases.
- Tuned Cassandra queries across multiple data sources to respond in under 1 second, debugging in Splunk.

---

## Education

**M.Eng. Applied Data Science**, University of Victoria - Sep 2025 - Dec 2027<br>
**M.S. Computer Science**, University of Chicago - Sep 2020 - Mar 2022<br>
**B.S. Economics**, University of Washington - Sep 2015 - Aug 2019

---

## Featured Work

### [Ocean Data ML Platform with RAG](https://github.com/ntdai95/Resume-Projects/tree/main/Ocean%20Data%20ML%20Platform%20with%20RAG)
*Solo · Python, Spark, XGBoost, MLflow, Optuna, Qdrant, FastAPI, Docker*

This is a platform over **10.8M ocean and weather sensor observations** from NOAA and ONC, two agencies whose NetCDF formats don't agree on much.

- Bronze ingestion runs in pandas and xarray, Spark handles the Silver layer, and the result is a **3.69M-row Gold** forecasting table.
- I validated the XGBoost forecasts on **chronological** holdouts, because the series is temporally correlated and a random split would leak.
- Retrieval runs over the dataset metadata with Sentence Transformers, Qdrant and Ollama, all of it local end to end.
- MLflow tracks the experiments and Optuna runs the hyperparameter search, and Docker Compose containerizes FastAPI together with the vector store.

**I scored retrieval against a held-out query set covering every document, reaching hit@k 0.9 and term recall 0.85.**

On **water temperature**, a naive persistence baseline (predict = previous reading) beats the tuned XGBoost model on raw RMSE. That is expected for a high-frequency, smooth signal, and it is why this section gives both numbers instead of the model's R² on its own. I extended the check across seven horizons out to 2 hours, and added a version with sensor context (salinity and dissolved oxygen). Persistence won every horizon, and XGBoost’s R² went negative past 30 minutes, which is what a model looks like when it fits training-period noise instead of learning real drift.

**I ran the same benchmark as a control, on a signal from the same ONC network that should be forecastable.** Air temperature from ONC's Baynes Sound weather station has an obvious deterministic driver (the daily solar cycle) that persistence can't anticipate. There, XGBoost wins decisively from 3-12 hours out. Persistence's R² actually goes negative at 6 and 12 hours, while XGBoost cuts RMSE by up to 48% at the 12-hour mark. The pipeline and the evaluation stayed the same. Only the signal changed, and the answer came out the other way.

---

### [Multi-Stage IoT Intrusion Detection](https://github.com/ntdai95/ECE592B-Capstone-Project)
*Graduate capstone · team of 7 · Python, XGBoost, scikit-learn*

The detector works in two stages on CIC IoT-DIAD 2024. Stage one scores packets with k-means and an autoencoder, Deep SVDD, and an Anomal-E edge-feature GNN, fused into a single score. Stage two is a supervised flow classifier that consumes it. I compared six models under a hard **1% false-positive budget**. Binary XGBoost came out best at **99.5% recall, 0.94% FPR, PR-AUC 0.989**, and I regenerated all six under split-first preprocessing.

**The benchmark leaks capture-session identity.** Benign traffic was recorded on two days while each attack class occupies its own. The same threshold that holds 1% FPR on one capture day costs 25 to 29% on another. I ran a four-condition holdout to isolate it. Under an honest session-disjoint split, PR-AUC falls from **0.981 to 0.125**, and holding recall costs **25% FPR**, roughly twenty-five times the budget. Calibration is what breaks first. The ranking itself still holds up.

**My contribution** was the leakage discovery, the four-condition experiment, and `verify_context_integrity.py`, which rebuilds the 60-second connection-count feature on a truncated capture to prove it uses no future flows.

---

### [Distributed Facility Reservation System](https://github.com/ntdai95/Resume-Projects/tree/main/Distributed%20Facility%20Reservation%20System)
*Applied Software Engineering · team of 4 · Python, FastAPI, SQLite, pytest*

This is a booking service that had to interoperate with **four other teams' independent implementations** of one shared HTTP contract that nobody could change unilaterally.

- The service exposes **27 versioned `/v1/` endpoints**, each with published OpenAPI documentation.
- **71 pytest tests** cover the API, database and reservation-rules layers.
- Every request checks its session token for existence, one-hour freshness and permission scope.
- An 847-line SQLite layer over four tables enforces the rules on funds and availability.

---

### [Auction Marketplace Microservices](https://github.com/ntdai95/Auction-Website)
*Team of 4 · Python, Flask, MySQL, MongoDB, RabbitMQ*

This is an auction marketplace split into six Flask REST services (items, users, auctions, transactions, watchlist and messages), each owning its own datastore, so a schema change in one cannot break its callers. Five sit behind their own MySQL database; messages uses MongoDB.

Messages move between services through **RabbitMQ** and are stored in MongoDB for durable delivery. The stack runs as **14 Docker containers** with dependency-ordered startup on a shared bridge network, so every database is up before the service that reads it.

---

### [Anomaly Detection at Scale on Species Data](https://github.com/ntdai95/CSC502-Final-Project)
*Systems for Massive Datasets · team of 3 · Python, PySpark, scikit-learn*

I wrote Isolation Forest **from the published algorithm instead of importing it from a library**, and ran it on 1,093,203 eBird observations across British Columbia.

- I wrote the implementation from scratch in Python and processed the data with PySpark.
- I stratified the sampling across eight quantile bins, which preserves the species frequency distribution.
- I **observed a geographic form of feature-specific swamping**, and proposed rank transformation and density-aware subsampling as mitigations.

**The detector reached AUC 0.67, and runtime scaled linearly across the hyperparameter grid.**

---

### [End-to-End Multi-Output Fuel Blending System](https://github.com/ntdai95/Shell.ai-Hackathon-2025)
*Solo · Shell.ai Hackathon 2025 · Python, CatBoost, FastAPI, Docker, AWS EC2*

- I built and deployed multi-output regression across 10 blend properties through FastAPI on Dockerized AWS EC2.
- Advanced CatBoost to deployment based on 5-fold cross-validation with a MAPE of 0.64 versus XGBoost’s 1.29.
- I engineered entropy-based mixture metrics and serialized the preprocessing so training and inference stayed consistent.

---

## Additional Selected Work

- In [**Stock Sentiment Analysis**](https://github.com/ntdai95/Resume-Projects/tree/main/Stock%20Sentiment%20Analysis), I scored financial tweets with FinTwitBERT, joined daily sentiment to market returns in SQLite, and preserved author-to-tweet-to-stock relationships in Neo4j. NVDA was the only stock with a significant Granger result, and the broader sample did not support influencer sentiment as a strong standalone signal.
- In the [**Parallel Image Processing Engine**](https://github.com/ntdai95/Resume-Projects/tree/main/Parallel%20Image%20Processing%20Engine), I implemented grayscale, sharpening, blurring, and edge detection in Go with custom convolution kernels and three execution models. On batches of more than 30 images, fan-in/fan-out reduced runtime by **20%**, while bulk synchronous execution reduced it by **30%**.
- In the [**Belay Real-Time Chat Application**](https://github.com/ntdai95/Personal-Projects/tree/main/Belay), I built channels, messages, threaded replies, and shareable client-side routes with Flask and JavaScript. The service uses four SQLite tables, nested REST endpoints, hashed passwords, and a token checked on every authenticated request.
- In [**Support Ticket Triage**](https://github.com/ntdai95/ECE569A-Final-Project), I compared TF-IDF with a linear SVM, retrieval kNN, and DistilBERT on the same routing task. Retrieval kNN at k=5 won on all three labels, including queue accuracy of **0.702 versus 0.597** for DistilBERT, and the Streamlit demo showed the retrieved tickets behind each prediction.
- In the [**Loan Approval Classifier**](https://github.com/ntdai95/CSC503-Final-Project), I compared tuned XGBoost and neural-network classifiers across baseline, SMOTE, class-weighted, and quantum-transformed feature sets. I applied Fairlearn constraints across age and income and tested a specialist ensemble trained separately on inlier and outlier partitions.
