<div align="center">

# Gilsu Park

**ML / MLOps Engineer · Security & Log Anomaly Detection**

I build ML systems that detect abnormal behavior in operational data — system logs and network flows — and connect the models to real collection, serving, and storage pipelines.

[![Email](https://img.shields.io/badge/Email-pgilsu93%40gmail.com-245B6B?style=flat-square&logo=gmail&logoColor=white)](mailto:pgilsu93@gmail.com)
[![About Me](https://img.shields.io/badge/Portfolio-alephtasks.vercel.app-3F6273?style=flat-square)](https://alephtasks.vercel.app/)
[![Thesis](https://img.shields.io/badge/Thesis-RISS-536A78?style=flat-square)](https://www.riss.kr/link?id=T17372490)

<br>

<a href="#tech-stack"><img src="https://skillicons.dev/icons?i=python,pytorch,sklearn,fastapi,postgres,docker,linux,git,java,spring&perline=10" alt="Python, PyTorch, scikit-learn, FastAPI, PostgreSQL, Docker, Linux, Git, Java, Spring" /></a>

</div>

---

## At a Glance

- **3+ years in operations** — maintained a public-sector Java/Spring (eGovFrame) system; traced incidents across screens, server logic, SQL, data, and WAS logs
- **Master's degree, Kookmin University Graduate School (Data Science major)** — graph-based log anomaly detection using how logs occur in operation (timing, burst, severity)
- **End-to-end detection system** — NetFlow port-scan detector from packet collection on a NAS to PyTorch/FastAPI inference and a review dashboard (**F1 89.07%** on CIDDS-002 Week2)

---

## Now

- **Course:** SKT K-New Deal Academy · ALEPH — security operations fundamentals, until Dec 2026
- **Side project:** going beyond the course material, I'm building my own security ML pipeline — from raw network traffic to a served detection model:
  - [ ] PCAP → Zeek JSON logs, reproducible with Docker
  - [ ] Data validation and label alignment (pandas)
  - [ ] PySpark preprocessing and time-window aggregation → Parquet
  - [ ] Unsupervised baseline with experiment tracking (scikit-learn, MLflow)
  - [ ] Inference API and storage (FastAPI, PostgreSQL, Docker Compose) with CI
  - [ ] Dynamic graph anomaly detection as the main model

---

## Research · Log Anomaly Detection

**Premise:** the same log message can mean different things about the system depending on **when** it occurs, **how densely** it appears, and **how severe** it is.

**Gap:** Lograph learns log content and the relations between logs through shared entities (IDs, addresses, components) in a Log-Entity Graph. But its log adjacency is just the number of shared entities, so information about **how logs actually occur in operation** is left out.

**Approach:** I redesigned the log adjacency matrix to include that occurrence context, and compared each design under a controlled setup — same data, splits, model, and training, with only the adjacency changed.

```mermaid
%%{init: {"flowchart": {"nodeSpacing": 14, "rankSpacing": 36, "padding": 6}, "themeVariables": {"fontSize": "13px"}}}%%
flowchart LR
    A["Lograph adjacency<br/>shared-entity count"]

    subgraph C["Occurrence context"]
        T["When · temporal weight"]
        B["How densely · burst score"]
        L["How severe · log-level weight"]
    end

    K["Which edges · Top-k sparsification"]

    A --> T
    A --> B
    A --> L
    A --> K

    T --> E
    B --> E
    L --> E
    K --> E

    E["Compared one by one<br/>BGL · Thunderbird · HDFS"]

    classDef base fill:#f6f8fa,stroke:#8c959f,color:#24292f;
    classDef ctx fill:#eef4f7,stroke:#587384,color:#243746;
    class A,E,K base;
    class T,B,L ctx;
    style C fill:#fbfcfd,stroke:#a3adb5,color:#34404a;
```

| Design | Question it encodes | How |
| --- | --- | --- |
| Temporal weight | *When* did the two logs occur? | Logs closer in time are connected more strongly |
| Burst score | *How densely* did logs occur? | Emphasize logs inside short, dense bursts — often around state changes or failures |
| Log level | *How severe* were the logs? | Weight pairs by severity (DEBUG 0.8 → FATAL 2.0) |
| Top-k | *Which* connections matter? | Keep only the strongest edges per log to remove dense, noisy links |

**F1-score** (single run per setting; best per dataset in bold)

| Dataset | Baseline | Temporal | Burst | Level | Top-k |
| --- | ---: | ---: | ---: | ---: | ---: |
| BGL | 0.9268 | **0.9307** | 0.9263 | 0.9230 | 0.9094 |
| Thunderbird | 0.9580 | 0.9602 | **0.9769** | 0.9630 | 0.9588 |
| HDFS | 0.8174 | 0.8282 | 0.8178 | 0.8172 | **0.8342** |

- **Temporal weighting was the only design that beat the baseline on all three datasets** in this setup — *when* a log occurs was the most robust occurrence signal.
- The other designs helped on some datasets and hurt on others, so the right adjacency depends on the data's characteristics.
- Next: repeated runs with mean ± std, and combining signals.

*인터리빙 환경에서 로그-엔티티 그래프 인접 구조 설계의 비교 분석* · Master's thesis · Kookmin University Graduate School, Data Science · 2026

---

## Project · NetFlow Port Scan Detection

Explicit scan rules plus a lightweight Transformer that classifies 30-second flow windows.  
Collection and storage run always-on on a NAS; training and inference run on a GPU PC.

```mermaid
flowchart BT
    subgraph NAS["NAS · Collection & Storage"]
        direction LR
        A["Packets"] --> B["5-tuple Flow"] --> G[("PostgreSQL")] --> H["Dashboard"]
    end

    subgraph PC["GPU PC · Inference"]
        direction LR
        C["30s window<br/>≤ 32 flows"]
        D["Rule Detector"]
        E["Lightweight<br/>Transformer"]
        F["Decision<br/>Alert / Review / Normal"]
        C --> D --> F
        C --> E --> F
    end

    NAS -- flows --> PC
    PC -- scores · evidence --> NAS

    classDef nas fill:#f6f8fa,stroke:#8c959f,color:#24292f;
    classDef ml fill:#eef4f7,stroke:#587384,color:#243746;
    class A,B,G,H nas;
    class C,D,E,F ml;
    style NAS fill:#fbfcfd,stroke:#a3adb5,color:#34404a;
    style PC fill:#fbfcfd,stroke:#a3adb5,color:#34404a;
```

<!-- Add one dashboard screenshot or GIF here, e.g. ![Dashboard](docs/dashboard.png) -->

**What I built:** Scapy packet collection and 5-tuple flow aggregation · queue + batch writer to decouple capture from DB writes · per-source windows · rule detector · Transformer encoder (PyTorch) · FastAPI inference · PostgreSQL storage for flows, scores, and rule evidence · Spring Boot dashboard

**Design decisions**

- **Leakage-free evaluation** — normalization fitted on Week1 train only; Week1 for train/validation, Week2 for test
- **Window as the decision unit** — flows grouped per source IP into 30-second windows of up to 32 flows, so the model sees scan *behavior*, not single flows
- **Rules and model have separate roles** — rules catch clear signatures fast; the model covers slow or varied scans that fixed thresholds miss
- **Simplified model** — inspired by FlowTransformer-style sequence modeling, not a reproduction of the original

**Evaluation · CIDDS-002 Week2**

| Method | Precision | Recall | F1 |
| --- | ---: | ---: | ---: |
| Rule detector | 79.16% | 50.08% | 61.35% |
| Lightweight Transformer | 87.86% | 89.47% | 88.66% |
| **Transformer + explicit scan rules** | **87.93%** | **90.24%** | **89.07%** |

**Limitations:** CIDDS-002 is a simulated dataset, and evaluation on live traffic (false-positive rate, latency) is the next step.

[![Repository](https://img.shields.io/badge/Detection-Repository-181717?style=flat-square&logo=github)](https://github.com/prosild/netflow_portscan_detection)
[![Dashboard](https://img.shields.io/badge/Dashboard-Repository-181717?style=flat-square&logo=github)](https://github.com/prosild/NexusPortal)
[![Demo](https://img.shields.io/badge/Live-Dashboard-2F6B8A?style=flat-square)](https://psdev93.synology.me/portfolio/portscan)

---

## Tech Stack

| Area | Technologies | Where I used them |
| --- | --- | --- |
| **ML / Data** | Python, PyTorch, scikit-learn, pandas, NumPy | Thesis models and experiments; Transformer training and preprocessing in the port-scan project |
| **Network** | Scapy | Packet capture, 5-tuple flow aggregation, test traffic generation |
| **Serving / Data store** | FastAPI, PostgreSQL | Real-time detection API; storage for flows, scores, and rule evidence |
| **Infra / Tools** | Docker, Docker Compose, Linux, Git, Conda, CUDA | Collector and DB on a Synology NAS; GPU inference on a PC |
| **Backend** | Java, Spring Boot, MyBatis, SQL | 3+ years of public-sector system maintenance; detection dashboard |

---

## Interests

Log and network anomaly detection · graph learning on operational data · robustness under distribution shift · reproducible ML pipelines, serving, and monitoring for security operations
