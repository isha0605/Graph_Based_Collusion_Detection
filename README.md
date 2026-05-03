# Graph-Based Collusion Detection for Financial Fraud

## Overview

Most fraud detection systems analyze transactions individually.

This project takes a different approach — it focuses on **relationships between accounts**.

Instead of asking:
> *“Is this transaction suspicious?”*

It asks:
> *“Is this account part of a suspicious network?”*



## Approach

- Model transactions as a **graph**
  - **Nodes** → Accounts  
  - **Edges** → Money transfers  

- Apply **Louvain community detection** to identify tightly connected groups

- Score each community using structural features:
  - **Density**
  - **Reciprocity**
  - **Circular transaction patterns**

### Key Insight

- Fraud rings → **dense, highly connected clusters**  
- Normal users → **sparse, loosely connected networks**



## Results

### Dataset A (Clean Signal)

- ~4K accounts, 73K transactions  
- 12 fraud rings  
- **Graph Recall:** 100%  
- **Precision:** ~80%+  

Clear separation between fraud and normal communities  



### Dataset B (Noisy / Realistic)

- ~5K accounts, 84K transactions  
- 14 fraud rings (192 accounts)  
- **Graph Recall:** 100% (192/192)  
- **Precision:** 3.7%  

### Trade-off

- High recall → **no missed fraud rings**  
- Lower precision → **more false positives (needs filtering)**  



## Why It Matters

### Traditional ML (Random Forest, etc.)
- Works well for obvious fraud  
- Misses coordinated behavior  

### Graph-Based Detection
- Detects **collusion and fraud rings**  
- Identifies fraud even when individual transactions look normal  



## System Design

**Tier 1 — Real-time (ML Model)**
- Fast transaction scoring  
- Detects individual anomalies  

**Tier 2 — Batch (Graph Detection)**
- Runs periodically  
- Identifies fraud rings  

**Tier 3 — Analyst Review**
- Investigates high-risk communities  



## Tech Stack

- Python  
- NetworkX  
- Louvain Community Detection  
- scikit-learn  
- pandas  



## Key Takeaway

> Fraud rings don’t look suspicious individually.  
> They look suspicious **together**.

---
