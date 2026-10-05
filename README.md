# Jacob Willson

### Analytics Engineering · Business Intelligence · Data Science · Applied AI

[Portfolio](https://jacobwillson.com/) · [LinkedIn](https://www.linkedin.com/in/jacob-j-willson/)

My work spans analytics engineering, business intelligence, advanced analytics, data science, and applied AI. I built that foundation through analytics work at New Balance and through research, consulting, and operational roles across multiple industries.

Today, I work as an Applied AI Research Fellow, extending that foundation through experimental design, predictive modeling, NLP, retrieval-augmented generation, synthetic data, model evaluation, and AI infrastructure. I focus on turning complex data and model behavior into tested pipelines, defensible findings, and practical decisions.

## Featured Projects

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

## Selected Projects

### Analytics Engineering and Business Intelligence

- **[U.S. Retail Sales Time Series in SQL](https://github.com/JacobWillson13/retail-sales-timeseries-sql)** — Analyzed 29 years of U.S. Census retail data in PostgreSQL using window functions, regression aggregates, change-point detection, and three-year forecasts with prediction intervals and backtests.

### Advanced Analytics, Experimentation, and Decision Science

- **[Freight Cost & Sampling Analysis](https://github.com/JacobWillson13/freight-cost-analysis)** — Analyzed a 500,000-trip synthetic freight network using sampling simulation, cost-driver analysis, confounding controls, and route segmentation to produce operational decision insights.

- **[Gemma 4 Security-Advisory Evaluation](https://github.com/JacobWillson13/gemma4-eval)** — Designed and analyzed a 3,900-run controlled experiment measuring how model size, supplied evidence, reasoning configuration, and temperature affect accuracy, latency, reliability, and deployment trade-offs.

- **[Synthetic UAV Telemetry Evaluation](https://github.com/JacobWillson13/uav-pnt)** — Compared seven synthetic time-series generation approaches across two UAV datasets using statistical diagnostics and train-synthetic/test-real predictive evaluation.

### Applied AI and Information Systems

- **[SCIO Ontology Validation](https://github.com/JacobWillson13/scio-eval)** — Combined literature analysis, LLM-assisted evidence coding, embeddings, clustering, network analysis, topology, and structured review to evaluate a socio-cognitive influence ontology.

- **[DOME Handbook RAG](https://github.com/JacobWillson13/dome-rag)** — Built a local RAG application and evaluation suite containing 6,672 question-level results across retrieval strategies, embedding models, and language models.

- **[CiteBench](https://github.com/JacobWillson13/citebench)** — Developed a reproducible benchmark comparing citation-extraction workflows across PDF, text, vision, targeted-context, hybrid, and specialist-parser approaches.

- **[Agentic Development Workflow](https://github.com/JacobWillson13/agentic-dev-workflow)** — Designed a vendor-neutral, human-governed methodology for planning and executing analytics and AI projects with coding agents, with structured scoping, role separation, and quality gates.

## Areas of Practice

Analytics engineering and data modeling · Business intelligence and decision support · Financial and revenue analytics · Statistical analysis and experimental design · Predictive modeling and forecasting · NLP and RAG · Model evaluation · Synthetic data and time series · Document intelligence · AI infrastructure

## Technical Toolkit

- **Programming and Analytics:** Python, SQL, R, JupyterLab, Excel
- **Data Engineering and Modeling:** dbt, Snowflake, Databricks (Asset Bundles, Lakeflow), Apache Spark / PySpark, Delta Lake, DuckDB, Hightouch
- **BI and Enterprise Platforms:** Power BI, Tableau, Looker / LookML, Streamlit, Databricks AI/BI, Spotfire, SAP, Microsoft Dynamics 365, Salesforce, o9 Solutions
- **Machine Learning and Applied AI:** scikit-learn, PyTorch, Hugging Face Transformers, LangChain, Ollama, vLLM
- **Data and Retrieval:** PostgreSQL, ChromaDB, Qdrant
- **Cloud, MLOps, and Infrastructure:** GCP, Vertex AI, MLflow, Docker, GitHub Actions, Linux, CUDA, Prometheus, Grafana
