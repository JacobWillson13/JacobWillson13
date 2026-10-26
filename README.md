# Jacob Willson

### Analytics Engineering · Business Intelligence · Data Science · Applied AI

[Portfolio](https://jacobwillson.com/) · [LinkedIn](https://www.linkedin.com/in/jacob-j-willson/)

AI research fellow at the Air Force Research Laboratory. My background is business intelligence and data analytics at Forrester Research and New Balance; I now build data pipelines, LLM and agent evaluations, and GPU inference infrastructure.

## Featured Projects

### [Agent-Ready Analytics: Benchmarking Context for Data Agents](https://github.com/JacobWillson13/agent-ready-analytics)

**BigQuery · dbt · MetricFlow · LangGraph · LangSmith · Ollama · GitHub Actions**

A benchmark that measures how much a governed context layer (dbt docs, a MetricFlow semantic layer, and written business guides) changes a data agent's accuracy, cost, and latency, and whether it lets a small local model compete with an API model. The data comes from a seeded simulation of a fictional developer-tools SaaS company with 13 planted data traps, and every answer is scored in code against an answer key.

- Ran **1,152 agent executions** (64 questions, 3 context levels, 2 models, 3 runs each) and reports question-clustered bootstrap intervals.
- The context layer took local **Gemma 4 26B from 23% to 83%** accuracy on one RTX 3090 and cut its gap to Claude Haiku 5.5 from 43 points to 10, though not to parity.
- Traced every remaining full-context error to a cause, including a semantic-layer dimension that reports current state. Fixing its description took those questions from 2 of 12 runs correct to 11 of 12.
- Full context used **63% fewer input tokens** and 59% less time than raw tables. CI reruns the context eval on every pull request that changes the context layer and posts the result as a comment.

<img src="https://raw.githubusercontent.com/JacobWillson13/agent-ready-analytics/main/docs/screenshots/langsmith-dashboard-accuracy.png" alt="LangSmith dashboard showing data agent accuracy by model and context level" width="100%">

### [Seats-to-Cash: SaaS Finance Data Stack](https://github.com/JacobWillson13/seats-to-cash)

**dbt · Snowflake · DuckDB · Streamlit in Snowflake · Hightouch · Salesforce · LookML**

A finance data stack for a fictional product-led SaaS company, where every number is checked against an answer key. It answers a real finance question: *how much of ARR growth is real expansion, and how much is repricing as legacy plans move to per-seat pricing, and do billings, revenue, and cash tie out along the way?*

- Separates **repricing from expansion** in the ARR waterfall: $103K of 67% ARR growth was repricing, with a further ~$227K of exposure still ahead across 453 legacy accounts.
- Reconciles **billings, revenue, deferred revenue, and cash** to the cent, and matches **14,924 of 14,924** customer-months of MRR against the answer key, with six planted data defects all handled.
- Runs **immutable month-end closes** on an append-only ledger, tracing every restatement to the late-arriving rows that caused it.
- Runs the same dbt project (129 nodes, all tests passing) on **DuckDB and Snowflake**, reports through **Streamlit in Snowflake**, and reverse-ETLs account signals to **Salesforce via Hightouch**.

<img src="https://raw.githubusercontent.com/JacobWillson13/seats-to-cash/main/docs/img/streamlit_app.png" alt="Seats-to-Cash Streamlit in Snowflake report" width="100%">

### [AdventureWorks Lakehouse](https://github.com/JacobWillson13/adventureworks-lakehouse)

**Databricks Asset Bundles · Lakeflow Declarative Pipelines · dbt · PySpark · MLflow · AI/BI Dashboards**

A medallion lakehouse on Databricks that turns a broken 72-file CSV export into a tested dbt star schema, MLflow-tracked analyses, and a five-page AI/BI dashboard, all deployed as one Asset Bundle.

- **Bronze:** repairs headerless, mis-encoded, and malformed files with config-driven fixes, verifying every load against expected row counts.
- **Silver:** 20 typed tables in a Lakeflow pipeline with data-quality expectations on keys, foreign keys, and required columns.
- **Gold:** 34 dbt models and 148 tests, including revenue reconciliation and effective-dated cost history for margin analysis.
- **Analysis:** customer segmentation, forecasting backtests, margin, and supplier quality, tracked in MLflow. Findings include a 40% online vs. 0.6% reseller margin split and an honest result that forecasting does not beat a naive baseline at this grain.

<img src="https://raw.githubusercontent.com/JacobWillson13/adventureworks-lakehouse/main/docs/images/dashboard_overview.png" alt="AdventureWorks AI/BI dashboard overview" width="100%">

### [SaaS Usage Streaming on Azure](https://github.com/JacobWillson13/saas-usage-stream-azure)

**Azure Database for PostgreSQL · Azure Managed Grafana · Python · SQL · River**

A real-time analytics pipeline for a simulated B2B SaaS company. CRM, product, and payment data stream into Azure PostgreSQL at about 500 events per minute, feeding a live Grafana dashboard, an outlier detector, and an online model that predicts which free trials convert to paid.

- Loads **1.25 million rows** of history, then streams live events in one-second transactions. Consumers read past their own watermarks and write idempotently, so a take can be reset and replayed exactly in about 3 seconds.
- Flags anomalies **about 2.5 seconds** after they land, with perfect recall and precision on duplicate payments and negative invoices across 517 labeled injections.
- Caught a **label leak** in its own evaluation: an apparent 0.71 AUC came from when trials were scored. Fixed day-7 scoring gives an honest 0.54 from a calibrated model whose main signal is prior personal use (52% vs. 30% conversion).
- Serves a **42-panel Grafana dashboard** through a read-only role that can see only dashboard views.

<img src="https://raw.githubusercontent.com/JacobWillson13/saas-usage-stream-azure/main/docs/img/dashboard-live.png" alt="Live Grafana dashboard for the SaaS streaming pipeline" width="100%">

### [NFIP CRS Measurement: Are Flood Insurance Discounts Priced Right?](https://github.com/JacobWillson13/nfip-crs-measurement)

**Databricks Asset Bundles · Delta Lake · Unity Catalog · MLflow · PySpark · DuckDB · AI/BI Dashboards**

A data pipeline and measurement study on FEMA's National Flood Insurance Program. It asks whether Community Rating System discounts, 5% per class step, match the losses they actually prevent. About 75 million policy records and 2.7 million claims become a national community-year panel in DuckDB, and gold, quality checks, and the analysis run as a serverless Databricks job from the same SQL and Python.

- Caught a data problem on the first national load: FEMA's records stamp each community's **current** CRS class onto every historical year. The feasibility gates flagged it, and class history is rebuilt from Community Status Book dates.
- Within the same county and year, each class step lowers loss cost **5.9% against a scheduled 5%**, so discounts are right on average. By class, the **Class 7 and Class 9** discounts are 85% and 94% likely too generous.
- Placebo simulations showed the original difference-in-differences was **biased (+41% with no true effect, 25% false positives)**. The within-county redesign removed the bias, and a pre-registered randomized trial design shows what randomization can and cannot measure.
- A Bayesian pricing decision with value of information: halving the uncertainty is worth about **$96M a year**, far more than re-pricing on today's evidence.
- The same SQL and quality checks run on DuckDB and Databricks, with a CI parity test, Unity Catalog lineage, MLflow tracking, and a dashboard defined in code.

<img src="https://raw.githubusercontent.com/JacobWillson13/nfip-crs-measurement/main/databricks/screenshots/overview.png" alt="Databricks AI/BI dashboard for the NFIP CRS project: discounts right on average, with Class 7 and Class 9 flagged as likely too generous, and a state map of CRS participation" width="100%">

### [Ghost Storefronts: How Stale Is NYC's Record of Open Businesses?](https://github.com/JacobWillson13/ghost-storefronts)

**MongoDB · Python · LightGBM · scikit-learn · Altair / Vega-Lite · Docker**

**[Interactive data story](https://jacobwillson.com/dashboards/ghost-storefronts.html)**

New York's inspection agency only learns a business closed when an inspector visits, so its list of open businesses is only as current as the last inspection. This project rebuilds 1.18 million storefront inspection records (2010 to 2026) in MongoDB, measures how stale that list gets, checks it against three chains that closed on known dates, and predicts which visits will find a business already closed.

- Built raw, silver, and gold layers in MongoDB across two city record systems, with `$geoWithin` neighborhood assignment, business identities linked across a 2023 record-system switch, and leak-free visit features from `$setWindowFields`.
- **17.4% of 2025 inspection visits** found the business already closed, and 48% of those businesses were last seen open three or more years earlier.
- Used RadioShack, Payless, and Rite Aid as ground truth: about **1 in 4** RadioShack and Payless stores never got a closure record, and Payless records took a median **5.1 years** to arrive.
- A one-line rule (months since a business was last seen open) finds a closed business in **55% of the top 10%** of visits; trained models add 2.9 to 8.9 points, reported with business-clustered bootstrap intervals and calibration.
- Estimates that about **5,700 of 43,447** businesses seen open since 2023 would be recorded closed if visited today.

<img src="https://raw.githubusercontent.com/JacobWillson13/ghost-storefronts/main/docs/img/map.png" alt="Map of New York City neighborhoods shaded by the share of 2025 inspection visits that found the business already closed" width="100%">

## Selected Projects

### Analytics Engineering and Data Platforms

- **[U.S. Retail Sales Time Series in SQL](https://github.com/JacobWillson13/retail-sales-timeseries-sql)** — Analyzed 29 years of U.S. Census retail data in PostgreSQL using window functions, regression aggregates, change-point detection, and three-year forecasts with prediction intervals and backtests.

### Experimentation and Decision Science

- **[Next-Day Stockout Alerts](https://github.com/JacobWillson13/freshretail-stockout-prediction)** — Built a LightGBM model on a layered SQL feature pipeline that ranks 50,000 perishable store-product series by next-day stockout risk, raising alert precision from 54.9% to 65.1% at 5,000 alerts a day, validated with a leakage test, rolling-origin backtest, and store-clustered bootstrap intervals.

- **[Freight Broker Boom and Bust](https://github.com/JacobWillson13/freight-broker-boom-bust)** — Analyzed 99,281 real FMCSA broker authority records with a from-scratch Kaplan-Meier estimator, log-rank tests, and restricted mean survival time, showing that brokers who entered during the 2021-2022 freight boom lost their authority faster than earlier entrants.

- **[Freight Cost & Sampling Analysis](https://github.com/JacobWillson13/freight-cost-analysis)** — Analyzed a 500,000-trip synthetic freight network using sampling simulation, cost-driver analysis, confounding controls, and route segmentation to produce operational decision insights.

- **[Gemma 4 Security-Advisory Evaluation](https://github.com/JacobWillson13/gemma4-eval)** — Designed and analyzed a 3,900-run controlled experiment measuring how model size, supplied evidence, reasoning configuration, and temperature affect accuracy, latency, reliability, and deployment trade-offs.

- **[Synthetic UAV Telemetry Evaluation](https://github.com/JacobWillson13/uav-pnt)** — Compared seven synthetic time-series generation approaches across two UAV datasets using statistical diagnostics and train-synthetic/test-real predictive evaluation.

- **[Grateful Dead Lyric Analysis](https://github.com/JacobWillson13/grateful-dead-lyric-analysis)** — Tested whether the Grateful Dead's 50 most-played songs are lyrically simpler across 309 transcriptions, showing that type-token ratio is biased by song length and using MATTR, weighted log-odds, and NMF topic models to find that the real difference is subject matter.

### Applied AI and Information Systems

- **[Multi-Node LLM Inference on Two DGX Sparks](https://github.com/JacobWillson13/dgx-spark-cluster)** — Built and benchmarked a two-node vLLM cluster over a 196 Gb/s ConnectX-7 link, with a correctness gate on every throughput run and predictions recorded before each test, finding that one server split across both nodes reached 1.90x one node's throughput, tensor parallelism beat pipeline parallelism 2x, and FP8 cost 1.8 GSM8K points against 13.7 for NVFP4.

- **[SCIO Ontology Validation](https://github.com/JacobWillson13/scio-eval)** — Combined literature analysis, LLM-assisted evidence coding, embeddings, clustering, network analysis, topology, and structured review to evaluate a socio-cognitive influence ontology.

- **[News Acquisition Feasibility](https://github.com/JacobWillson13/news-acquisition-feasibility)** — Tested whether open tools can supply a reliable news corpus for persuasion analysis by collecting 246 articles from 30 U.S. outlets through Media Cloud and Trafilatura with a robots.txt-compliant crawler and two Gemini completeness judges, finding 62% to 72% complete-text yield overall and up to 89% from a curated outlet list.

- **[DOME Handbook RAG](https://github.com/JacobWillson13/dome-rag)** — Built a local RAG application and evaluation suite containing 6,672 question-level results across retrieval strategies, embedding models, and language models.

- **[CiteBench](https://github.com/JacobWillson13/citebench)** — Developed a reproducible benchmark comparing citation-extraction workflows across PDF, text, vision, targeted-context, hybrid, and specialist-parser approaches.

- **[Agentic Development Workflow](https://github.com/JacobWillson13/agentic-dev-workflow)** — Designed a vendor-neutral, human-governed methodology for planning and executing analytics and AI projects with coding agents, with structured scoping, role separation, and quality gates.

## Areas of Practice

Analytics engineering and data modeling · Business intelligence and decision support · Financial and revenue analytics · Statistical analysis and experimental design · Predictive modeling and forecasting · NLP and RAG · AI agent evaluation and context engineering · Model evaluation · Synthetic data and time series · Document intelligence · AI infrastructure

## Technical Toolkit

- **Programming and Analytics:** Python, SQL, R, JupyterLab, Excel
- **Data Engineering and Modeling:** dbt, MetricFlow, Snowflake, BigQuery, Databricks (Asset Bundles, Lakeflow, Unity Catalog), Apache Spark / PySpark, Delta Lake, DuckDB, Hightouch
- **BI and Enterprise Platforms:** Power BI, Tableau, Looker / LookML, Streamlit, Databricks AI/BI, Spotfire, SAP, Microsoft Dynamics 365, Salesforce, o9 Solutions
- **Machine Learning and Applied AI:** scikit-learn, LightGBM, SHAP, River, PyTorch, Hugging Face Transformers, LangChain, LangGraph, LangSmith, Pydantic, Ollama, vLLM
- **Data and Retrieval:** PostgreSQL, MongoDB, ChromaDB, Qdrant, Trafilatura
- **Cloud, MLOps, and Infrastructure:** Azure (Database for PostgreSQL, Managed Grafana), GCP, Vertex AI, MLflow, Docker, GitHub Actions, Linux, CUDA, Prometheus, Grafana
