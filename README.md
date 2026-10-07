<div align="center">

# Gilsu Park

### AI / ML Engineering · Anomaly Detection · ML Systems

I work on **anomaly detection for operational data** such as system logs and network flows,
with an interest in turning research ideas into systems that can be tested, served, and monitored in practice.

<br>

<img src="https://img.shields.io/badge/Research-Log%20Anomaly%20Detection-245B6B?style=flat-square" alt="Log Anomaly Detection">
<img src="https://img.shields.io/badge/ML-Graph%20%26%20Temporal%20Learning-3F6273?style=flat-square" alt="Graph and Temporal Learning">
<img src="https://img.shields.io/badge/Systems-AIOps%20%26%20Security-536A78?style=flat-square" alt="AIOps and Security">

</div>

---

## 👋 About

I began with **Java / Spring web systems**, where debugging meant following a problem through application logic, database queries, data, and logs rather than looking only at the visible symptom.

I later completed an **M.S. in Data Science at Kookmin University** and focused my research on **log anomaly detection**. Today, my main interest is the intersection of **anomaly detection, temporal/graph modeling, security data, and ML systems**.

I am particularly interested in problems where the model has to work with noisy operational data and eventually connect to a real pipeline—from data collection and preprocessing to inference, storage, and monitoring.

---

## 🔬 Research

### Interleaved Log Anomaly Detection

Large systems often run many tasks at the same time. Their logs become **interleaved**, meaning events from different tasks are mixed together on the same timeline.

My graduate research examined how the **adjacency structure of a Log-Entity Graph** should be designed so that it reflects more than shared entities.

| Signal | What it represents |
| --- | --- |
| **Temporal proximity** | Logs that occur close in time are more likely to belong to the same activity |
| **Burst behavior** | Dense log activity can indicate a state change or failure |
| **Log severity** | INFO, WARN, ERROR, FATAL carry different operational importance |
| **Top-k sparsification** | Removing weaker edges can reduce noise in dense subgraphs |

To compare these signals fairly, I kept the data pipeline and model settings fixed and changed only the adjacency design.

### Result

The **temporal-weighted adjacency** was the only strategy that improved F1 over the baseline on all three evaluated datasets.

| Dataset | Baseline | Temporal Weight |
| --- | ---: | ---: |
| BGL | 0.9268 | **0.9307** |
| Thunderbird | 0.9580 | **0.9602** |
| HDFS | 0.8174 | **0.8282** |

Burst weighting worked especially well on Thunderbird, while Top-k sparsification performed best on HDFS.  
This suggested that **temporal proximity was the most consistent signal**, while other structural signals were more dependent on the characteristics of each dataset.

**Master's thesis**  
*인터리빙 환경에서 로그-엔티티 그래프 인접 구조 설계의 비교 분석*  
Kookmin University · Department of Data Science · 2026

[![RISS](https://img.shields.io/badge/Thesis-RISS-2F6B8A?style=flat-square)](https://www.riss.kr/link?id=T17372490)

---

## 🧩 Selected Projects

### NetFlow Port Scan Detection

A network anomaly-detection system that combines **rule-based detection** with a **Transformer-based flow model**.

```text
Packet → Flow → Time Window → Rule + FlowTransformer → PostgreSQL → Dashboard
```

**What I built**

- packet collection and 5-tuple flow aggregation
- 30-second / up-to-32-flow detection windows
- rule-based detection for explicit scan patterns
- FlowTransformer for learned sequence patterns
- FastAPI-based inference interface
- PostgreSQL storage for flows, scores, evidence, and detection results
- dashboard integration for reviewing detection windows

**CIDDS-002 Week2 evaluation**

| Method | Precision | Recall | F1 |
| --- | ---: | ---: | ---: |
| Rule Detector | 79.16% | 50.08% | 61.35% |
| FlowTransformer | 87.86% | 89.47% | 88.66% |
| **Deep Learning + explicit scan rules** | **87.93%** | **90.24%** | **89.07%** |

The rule detector handles patterns that have clear signatures, while the learned model complements it on flow patterns that are harder to express with fixed thresholds.

[![Repository](https://img.shields.io/badge/GitHub-Repository-181717?style=flat-square&logo=github)](https://github.com/prosild/netflow_portscan_detection)

---

### NexusPortal

A modernization of a legacy Spring MVC application into a **Java 17 / Spring Boot 3.5** system, later connected to the port-scan detection pipeline.

**Key work**

- migrated XML-based Spring MVC configuration to Spring Boot
- migrated database logic to PostgreSQL
- reorganized authentication and web security
- connected port-scan detection results through application APIs and PostgreSQL
- built administrator and read-only views for detection results
- added Docker Compose deployment
- maintained automated tests with JUnit 5 and MockMvc

This project connects my web-development background with ML engineering: model outputs are stored, queried, exposed through APIs, and presented through an operational application.

[![Repository](https://img.shields.io/badge/GitHub-Repository-181717?style=flat-square&logo=github)](https://github.com/prosild/NexusPortal)

---

## 🧰 Tech Stack

<p>
  <img src="https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white" alt="Python">
  <img src="https://img.shields.io/badge/PyTorch-EE4C2C?style=flat-square&logo=pytorch&logoColor=white" alt="PyTorch">
  <img src="https://img.shields.io/badge/Java-ED8B00?style=flat-square&logo=openjdk&logoColor=white" alt="Java">
  <img src="https://img.shields.io/badge/Spring_Boot-6DB33F?style=flat-square&logo=springboot&logoColor=white" alt="Spring Boot">
  <img src="https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white" alt="FastAPI">
  <img src="https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white" alt="PostgreSQL">
  <img src="https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white" alt="Docker">
  <img src="https://img.shields.io/badge/Linux-FCC624?style=flat-square&logo=linux&logoColor=111111" alt="Linux">
</p>

| Area | Technologies |
| --- | --- |
| **ML / Data** | Python, PyTorch, scikit-learn, pandas, NumPy |
| **Backend** | Java, Spring Boot, MyBatis, FastAPI |
| **Database** | PostgreSQL |
| **Network / Security** | Scapy, NetFlow-based analysis |
| **Web** | JavaScript, HTML/CSS, JSP, jQuery, Bootstrap |
| **Tools / Ops** | Docker, Linux, Git, Conda, Maven, JUnit 5 |

---

## 🎯 Current Interests

- **Anomaly Detection** — system logs, network traffic, and security data
- **Graph & Temporal ML** — dynamic relationships and time-dependent behavior
- **Robust ML** — distribution shift and changing operational environments
- **AIOps** — ML for system monitoring and operational intelligence
- **ML Engineering / MLOps** — reproducible pipelines, serving, evaluation, and monitoring
- **LLM / RAG for Operations & Security** — using language models to support analysis and investigation

---

## 🚀 What I'm Building Toward

I want to build **anomaly-detection systems that remain useful outside an offline benchmark**.

That means working across three connected problems:

**1. Detect meaningful signals**  
Find which temporal, structural, and behavioral patterns actually distinguish abnormal system behavior.

**2. Make detection reliable**  
Evaluate how models behave when workloads, data distributions, and operating environments change.

**3. Connect models to real systems**  
Build the path from data collection and preprocessing to inference APIs, databases, dashboards, and monitoring.

My long-term direction is to work on **ML systems for reliability and security**, where anomaly-detection research can be translated into tools that are usable in real operational environments.
