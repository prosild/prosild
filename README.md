<!--
**prosild/prosild** is a ✨ _special_ ✨ repository because its `README.md` (this file) appears on your GitHub profile.

Here are some ideas to get you started:

- 🔭 I’m currently working on ...
- 🌱 I’m currently learning ...
- 👯 I’m looking to collaborate on ...
- 🤔 I’m looking for help with ...
- 💬 Ask me about ...
- 📫 How to reach me: ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...
-->
# Gil Su Park · prosild

**Backend Development → Data Science → Log Anomaly Detection**

## About

I studied Management Information Systems and spent about three years and four months maintaining Java/Spring web systems.  
Tracing production issues through application code, SQL, data, and logs led me to questions about how system behavior appears in operational data.  
I later pursued master's studies in Data Science, focusing my research on graph-based log anomaly detection.  
My interests span the full path from collecting system data and detecting anomalies to making the results useful in a service.

## What I Work On

- **Log anomaly detection** — Studying which log characteristics help distinguish normal and abnormal system behavior.
- **Graph and temporal learning** — Representing relationships between logs and system entities, together with changes over time.
- **Network and security anomaly detection** — Applying rules and learned models to patterns in network traffic.
- **AIOps** — Exploring how logs and other operational data can support investigation of system issues.
- **ML engineering** — Connecting data processing, model evaluation, inference APIs, and applications.

## Research Focus

System logs contain more than messages. The intervals between events, bursts of activity, log levels, and relationships with system entities can also provide signals of abnormal behavior.

My master's research examined temporal information that an existing Log-Entity Graph model did not fully capture. I incorporated time intervals, burst patterns, and log levels into graph representations, and experimented with time-aware connections and attention weights.

Across **BGL, Thunderbird, and HDFS**, the most effective design varied by dataset, but **information about the time between logs repeatedly contributed to better anomaly detection**.

The central question was which signals remained useful across different datasets, why they helped, and what the original representation missed.

## Experience

### Software Development

**Java / Spring web system maintenance · About 3 years and 4 months**

- Implemented user requests and investigated errors across the UI, request handling, Java code, SQL, stored data, and application logs.
- Used code, queries, and logs together to narrow down causes and checked related functionality after changes.
- Worked with Spring, MyBatis, CUBRID, jQuery, and JBoss.

### Data Science & Research

**Master's studies in Data Science · Log anomaly detection**

- Studied statistics, machine learning, deep learning, NLP, and computer vision.
- Built and evaluated graph-based log anomaly detection experiments with Python and PyTorch.
- Examined how timing, occurrence patterns, and entity relationships affected detection across log datasets.

## Tech Stack

| Area | Technologies |
| --- | --- |
| Languages | Python, Java, SQL, JavaScript |
| AI / Data | PyTorch, scikit-learn, pandas, NumPy |
| Backend / Web | Spring / Spring Boot, MyBatis, jQuery, HTML / CSS |
| Database / Infrastructure | CUBRID, PostgreSQL, JBoss, Git, Linux |

## Selected Projects

### [netflow_portscan_detection](https://github.com/prosild/netflow_portscan_detection)

Port scan detection combining a rule-based detector with FlowTransformer, using CIDDS-002 for training and evaluation and a NAS-to-PC pipeline for packet collection and inference.

`Python` `PyTorch` `FastAPI` `Network Anomaly Detection`

### [NexusPortal](https://github.com/prosild/NexusPortal)

A Spring MVC portal migrated to Java 17 and Spring Boot, with authentication improvements, PostgreSQL integration, and a dashboard for the NetFlow project's detection results.

`Java` `Spring Boot` `MyBatis` `PostgreSQL`

## Currently Exploring

- Dynamic and temporal graphs for changing system behavior.
- Security anomaly detection and AIOps workflows that connect detection with investigation.
- MLOps practices for reproducible experiments and consistent training and inference pipelines.
- LLM-assisted log and security analysis grounded in system data.
