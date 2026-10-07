<div align="center">

# Gilsu Park

### AI / ML Engineering · Anomaly Detection · ML Systems

I work with **operational data such as system logs and network flows**, focusing on how abnormal behavior can be detected, evaluated, and connected to real systems.

My background in Java/Spring web systems led me to graduate study in Data Science, where I researched **log anomaly detection under interleaving** and the role of temporal and structural signals in graph-based models.

<br>

<img src="https://img.shields.io/badge/Research-Log%20Anomaly%20Detection-245B6B?style=flat-square" alt="Log Anomaly Detection">
<img src="https://img.shields.io/badge/ML-Graph%20Learning%20%7C%20Time%20Series-3F6273?style=flat-square" alt="Graph Learning and Time Series">
<img src="https://img.shields.io/badge/Engineering-ML%20Systems-536A78?style=flat-square" alt="ML Systems">

</div>

---

## 👋 About

I started in **Java / Spring-based web systems**, working with application logic, databases, and logs in operational environments.

That experience led me to data science and eventually to **anomaly detection**: instead of only finding where a failure occurred, I became interested in which patterns in operational data can explain abnormal behavior and whether those patterns remain useful when the environment changes.

I earned a **master's degree through the Department of Data Science at Kookmin University** and now focus on problems around **log anomaly detection, graph learning, time-series behavior, security analytics, and ML systems**.

---

## 🔬 Research

### Interleaved Log Anomaly Detection

In large systems, logs from many concurrent tasks can be mixed together on the same timeline.  
This **interleaving problem** makes it difficult to determine which events actually belong to the same execution context.

My thesis studied the adjacency structure of a **Log-Entity Graph**, where log events and entities are modeled together.  
The main question was:

> **What information should determine how strongly two log events are connected?**

```mermaid
flowchart LR
    A["Interleaved<br/>Logs"] --> B["Log-Entity<br/>Graph"]
    B --> C{"Adjacency<br/>Design"}

    C --> D1["Time"]
    C --> D2["Burst"]
    C --> D3["Level"]
    C --> D4["Top-k"]

    D1 --> E["BGL · Thunderbird · HDFS"]
    D2 --> E
    D3 --> E
    D4 --> E

    classDef base fill:#f6f8fa,stroke:#8c959f,color:#24292f;
    classDef focus fill:#eef4f7,stroke:#587384,color:#243746;
    classDef signal fill:#f8fafb,stroke:#a3adb5,color:#34404a;

    class A,B,E base;
    class C focus;
    class D1,D2,D3,D4 signal;
```

I compared four adjacency strategies while keeping the rest of the model and data pipeline fixed.

| Signal | Idea |
| --- | --- |
| **Temporal proximity** | Strengthen relationships between logs that occur close in time |
| **Burst behavior** | Emphasize locally dense log activity |
| **Log severity** | Reflect the different importance of INFO, WARN, ERROR, and FATAL |
| **Top-k sparsification** | Remove weaker edges from dense log subgraphs |

### Result

Across the three evaluated datasets, **temporal-weighted adjacency showed consistent F1 improvements over the baseline**.

| Dataset | Baseline F1 | Temporal Weight F1 |
| --- | ---: | ---: |
| BGL | 0.9268 | **0.9307** |
| Thunderbird | 0.9580 | **0.9602** |
| HDFS | 0.8174 | **0.8282** |

These results suggest that **temporal proximity can provide a stable and useful signal for interleaved log anomaly detection**.

**Master's Thesis**  
*인터리빙 환경에서 로그-엔티티 그래프 인접 구조 설계의 비교 분석*  
Kookmin University · Department of Data Science · 2026

[![RISS](https://img.shields.io/badge/Thesis-RISS-2F6B8A?style=flat-square)](https://www.riss.kr/link?id=T17372490)

---

## 🛠️ Project

### NetFlow Port Scan Detection

A network anomaly-detection pipeline that combines explicit scan rules with a **lightweight Transformer model for flow-window classification**.

The Transformer component is a simplified implementation inspired by FlowTransformer-style sequence modeling rather than a direct reproduction of the original architecture.

The system separates **always-on collection and storage on the NAS** from **model training and inference on the PC**, where more compute is available.

```mermaid
flowchart LR
    subgraph NAS["NAS · Collection & Storage"]
        A["Packets"] --> B["5-tuple<br/>Flow"]
        G[("PostgreSQL")]
        H["Dashboard"]
        G --> H
    end

    subgraph PC["PC · Training & Inference"]
        C["30s Window<br/>max 32 flows"]
        D["Rule<br/>Detector"]
        E["Lightweight<br/>Transformer"]
        F["Decision"]

        C --> D
        C --> E
        D --> F
        E --> F
    end

    B --> C
    F --> G

    classDef nas fill:#f6f8fa,stroke:#8c959f,color:#24292f;
    classDef ml fill:#eef4f7,stroke:#587384,color:#243746;

    class A,B,G,H nas;
    class C,D,E,F ml;
```

### What I implemented

- packet collection and **5-tuple flow aggregation**
- memory queue + batch writer for separating collection from DB writes
- source-based detection windows of up to **32 flows within 30 seconds**
- rule-based detection for explicit scan patterns
- lightweight Transformer encoder for learned flow-sequence patterns
- **FastAPI** inference interface
- **PostgreSQL** storage for flows, model scores, rule evidence, and decisions
- dashboard integration for reviewing detection windows

The project uses **Scapy** for packet collection and controlled test traffic, but keeps packet handling separate from the ML inference pipeline.

### Evaluation

On the CIDDS-002 Week2 evaluation used in the project:

| Method | Precision | Recall | F1 |
| --- | ---: | ---: | ---: |
| Rule Detector | 79.16% | 50.08% | 61.35% |
| Lightweight Transformer | 87.86% | 89.47% | 88.66% |
| **Transformer + explicit scan rules** | **87.93%** | **90.24%** | **89.07%** |

The rules handle patterns with clear signatures, while the learned model complements them on flow patterns that are harder to describe with a fixed threshold.

[![Repository](https://img.shields.io/badge/GitHub-Repository-181717?style=flat-square&logo=github)](https://github.com/prosild/netflow_portscan_detection)

---

## 🧰 Tech Stack

<p>
  <img src="https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white" alt="Python">
  <img src="https://img.shields.io/badge/PyTorch-EE4C2C?style=flat-square&logo=pytorch&logoColor=white" alt="PyTorch">
  <img src="https://img.shields.io/badge/Java-ED8B00?style=flat-square&logo=openjdk&logoColor=white" alt="Java">
  <img src="https://img.shields.io/badge/Spring-6DB33F?style=flat-square&logo=spring&logoColor=white" alt="Spring">
  <img src="https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white" alt="FastAPI">
  <img src="https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white" alt="PostgreSQL">
  <img src="https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white" alt="Docker">
  <img src="https://img.shields.io/badge/Linux-FCC624?style=flat-square&logo=linux&logoColor=111111" alt="Linux">
  <img src="https://img.shields.io/badge/Git-F05032?style=flat-square&logo=git&logoColor=white" alt="Git">
</p>

| Area | Technologies |
| --- | --- |
| **ML / Data** | Python, PyTorch, scikit-learn, pandas, NumPy |
| **Backend / API** | Java, Spring, MyBatis, FastAPI |
| **Database** | PostgreSQL |
| **Web** | JavaScript, HTML/CSS, JSP, jQuery, Bootstrap |
| **Engineering** | Docker, Linux, Git, Conda |

---

## 🎯 Interests

<table>
<tr>
<td width="50%" valign="top">

### Modeling

- Log anomaly detection
- Network / security anomaly detection
- Graph learning
- Time-series modeling
- Distribution shift
- Robust anomaly detection

</td>
<td width="50%" valign="top">

### ML Engineering

- Operational ML pipelines
- Model serving and evaluation
- API / database integration
- Monitoring and failure analysis
- AIOps applications
- LLM-assisted log / security analysis

</td>
</tr>
</table>

---

## 🚀 What I Want to Work On

My near-term goal is to work as an **AI / ML engineer building anomaly-detection systems for operational data**.

I am especially interested in environments where logs, network traffic, or system events need to be analyzed continuously and where a model has to work as part of a larger software system.

### 1. Detect meaningful abnormal behavior

I want to model temporal, structural, and behavioral patterns in operational data and identify which signals remain useful when the environment changes.

### 2. Build reliable ML pipelines

Beyond offline model performance, I want to work with the engineering around the model:

```text
Operational Data
      ↓
Preprocessing / Feature Construction
      ↓
ML Model
      ↓
Inference API
      ↓
Database / Application
      ↓
Monitoring / Investigation
```

### 3. Apply ML to real operational problems

My main application interests are **system reliability, anomaly detection, and security-oriented operational data**.

I see **AIOps as a natural application area for anomaly detection**, while my engineering focus is on building the practical capabilities needed to use ML in real systems: reproducible pipelines, serving, evaluation, deployment, and monitoring.
