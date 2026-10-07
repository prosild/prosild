<div align="center">

<h1>Gil Su Park</h1>

<p><strong>Backend Development · Data Science · Anomaly Detection</strong></p>

<p>From understanding system behavior to learning from its data.</p>

<p>
  <a href="#research-focus">Research</a> &nbsp;·&nbsp;
  <a href="#experience">Experience</a> &nbsp;·&nbsp;
  <a href="#selected-projects">Projects</a> &nbsp;·&nbsp;
  <a href="#tech-stack">Tech Stack</a>
</p>

</div>

---

## About

My background is in **Management Information Systems**, followed by **3 years and 4 months maintaining Java/Spring web systems**.

Tracing production issues through code, SQL, and application logs led me to study how system behavior appears in operational data. I later pursued **master's studies in Data Science**, focusing on **graph-based log anomaly detection**.

I am interested in connecting data collection, anomaly detection, and the services that use the results.

## What I Work On

| Area | Focus |
| :--- | :--- |
| **Log Anomaly Detection** | Finding signals that distinguish normal and abnormal system behavior. |
| **Graph & Temporal Learning** | Representing relationships between logs, entities, and events over time. |
| **Security Anomaly Detection** | Combining rules and learned models to analyze network traffic. |
| **AIOps** | Using operational data to support investigation of system issues. |
| **ML Engineering** | Connecting data processing, model evaluation, inference, and applications. |

## Research Focus

### What can log timing tell us about system behavior?

Log messages are only part of the picture. **When events occur, how often they repeat, and which entities they relate to** can also help explain anomalies.

My master's research examined information that an existing **Log-Entity Graph** model did not fully capture:

- **Time intervals** between log events.
- **Burst patterns** and changes in event frequency.
- **Log levels** such as INFO, WARN, and ERROR.
- **Relationships** between logs and system entities.

I incorporated these signals into graph representations and tested time-aware connections and attention weights on **BGL, Thunderbird, and HDFS**.

> **Key finding**  
> The most effective design differed by dataset, but time intervals between logs repeatedly helped improve anomaly detection.

The goal was to understand **which signals helped, why they helped, and whether their value held across datasets**.

---

## Experience

### Software Development

**Java / Spring web systems** · About 3 years and 4 months

- Maintained web systems and implemented user requests.
- Investigated errors across the UI, request handling, Java code, SQL, data, and application logs.
- Checked related functionality and the impact of changes after fixes.

### Data Science & Research

**Master's studies in Data Science** · Log anomaly detection

- Studied statistics, machine learning, deep learning, NLP, and computer vision.
- Built graph-based anomaly detection experiments with **Python and PyTorch**.
- Evaluated how timing, occurrence patterns, and entity relationships affected detection across datasets.

## Selected Projects

### [NetFlow Port Scan Detection](https://github.com/prosild/netflow_portscan_detection)

Port scan detection using **rules and FlowTransformer**.

- Trained and evaluated models on CIDDS-002.
- Connected NAS packet collection with PC-based inference.
- Stored detection results for use in a web dashboard.

`Python` `PyTorch` `FastAPI` `Network Security`

### [NexusPortal](https://github.com/prosild/NexusPortal)

A Spring MVC portal migrated to **Java 17 and Spring Boot**.

- Updated authentication and integrated PostgreSQL.
- Added a dashboard for the NetFlow project's detection results.
- Connected backend development with security data analysis.

`Java` `Spring Boot` `MyBatis` `PostgreSQL`

## Tech Stack

| Area | Technologies |
| :--- | :--- |
| **Languages** | Python · Java · SQL · JavaScript |
| **AI / Data** | PyTorch · scikit-learn · pandas · NumPy |
| **Backend / Web** | Spring / Spring Boot · MyBatis · jQuery · HTML / CSS |
| **Database / Infrastructure** | CUBRID · PostgreSQL · JBoss · Git · Linux |

---

## Currently Exploring

- **Dynamic & Temporal Graphs** — Modeling changes in system behavior.
- **Security & AIOps** — Connecting anomaly detection with investigation.
- **MLOps** — Reproducible experiments and consistent training and inference.
- **LLM-assisted Analysis** — Log and security analysis grounded in system data.
