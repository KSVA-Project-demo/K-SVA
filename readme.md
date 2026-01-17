# Grounding Before Reasoning: Structural Hallucination Mitigation via Sequential Multi-modal Knowledge Graph Pruning

<div align="center">

[![Paper](https://img.shields.io/badge/Paper-Anonymous-red)](Coming_Soon)
[![License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Framework](https://img.shields.io/badge/PyTorch-2.0-orange.svg)](https://pytorch.org/)

**Anonymous Authors**

</div>

---

## 📖 Abstract

Multi-modal Large Language Models (MLLM) frequently suffer from object hallucinations, where generated responses drift from visual reality due to the entanglement of perception and generation. In this paper, we reduce the mitigation of hallucinations to a process of structural denoising on **Multi-modal Knowledge Graphs** and propose the **Grounding Before Reasoning** framework. 

We introduce the **Knowledge-guided Structural Verification Agent (K-SVA)**, a neuro-symbolic architecture that treats the initial visual parse as a **noisy graph-structured hypothesis space**. By formulating grounding as a sequential decision-making process driven by a **Mixture of Pruning Experts (MoPE)**, our agent dynamically executes **knowledge graph pruning** to isolate a minimal sufficient evidence chain. This mechanism structurally filters the propagation of hallucinatory signals before generative reasoning begins.

Extensive experiments across **six benchmarks** (ScienceQA, GeoQA, VizWiz, TextVQA, POPE, etc.) demonstrate that our method significantly reduces hallucination rates while achieving state-of-the-art reasoning accuracy.

---

## 🚀 Key Features

### 1. Subtractive Paradigm Shift
Unlike traditional additive retrieval (e.g., GraphRAG) that accumulates noise, K-SVA adopts a **subtractive paradigm**, physically removing ungrounded nodes to prevent hallucination propagation.

![Paradigm Comparison](assets/paradigm.png)
*Figure 1: Comparison between Additive Retrieval (Left) and our Subtractive Grounding Paradigm (Right).*

### 2. K-SVA Architecture
The agent leverages a **Mixture of Pruning Experts (MoPE)** to evaluate node validity from three dimensions:
- **👁️ Visual Expert ($E_{vis}$)**: Detects object existence via fine-grained cross-modal alignment.
- **🧠 Logic Expert ($E_{log}$)**: Identifies semantic drift and logical violations (inspired by TransE).
- **🕸️ Topology Expert ($E_{topo}$)**: Assesses structural support and redundancy via GAT.

![Architecture](assets/framework.png)
*Figure 2: The pipeline of the K-SVA framework, illustrating the MoPE module and the sequential pruning process.*

---

## 📊 Main Results

K-SVA achieves consistent improvements across reasoning, robustness, and hallucination evaluation benchmarks.

| Category | Method | ScienceQA (Reasoning) | VizWiz (Robustness) | POPE (Hallucination) |
| :--- | :--- | :---: | :---: | :---: |
| **LMMs** | LLaVA-1.5 | 89.8 | 57.2 | 83.5 |
| **RAG (SOTA)** | PathRAG | 90.6 | 59.2 | 83.5 |
| **Ours** | **K-SVA** | **92.8** | **63.5** | **88.2** |

> **Note**: For full experimental results, please refer to the main paper.

![Results Analysis](assets/results.png)
*Figure 3: Sensitivity analysis and robustness comparison under varying noise levels.*

---

## 🛠️ Installation

1. **Clone the repository** (Anonymous link):
   ```bash
   git clone [https://anonymous.4open.science/r/KSVA-Project-XXXX](https://anonymous.4open.science/r/KSVA-Project-XXXX)
   cd KSVA-Project-XXXX