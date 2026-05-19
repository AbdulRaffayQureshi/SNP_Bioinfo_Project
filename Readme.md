<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0a1628,40:005B60,100:0097a7&height=220&section=header&text=🧬%20SLC6A4%20Variant%20Pipeline&fontSize=52&fontColor=e0f7fa&fontAlignY=40&desc=Variant%20Detection%20%26%20Functional%20Interpretation%20using%20Simulated%20NGS%20Reads&descAlignY=62&descSize=15&descColor=90caf9&animation=fadeIn" width="100%"/>

<br/>

[![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://python.org)
[![Galaxy Server](https://img.shields.io/badge/Galaxy-Platform-276A8F?style=for-the-badge&logo=galaxy&logoColor=white)](https://usegalaxy.org)
[![Bowtie2](https://img.shields.io/badge/Bowtie2-Alignment%20Engine-189fdd?style=for-the-badge&logo=linux&logoColor=white)](https://bowtie-bio.sourceforge.net/bowtie2/index.shtml)
[![Cytoscape](https://img.shields.io/badge/Cytoscape-Web%20Visualization-ea580c?style=for-the-badge&logo=diagrams&logoColor=white)](https://cytoscape.org)

[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?style=for-the-badge&logo=jupyter&logoColor=white)](https://jupyter.org)
[![NCBI](https://img.shields.io/badge/NCBI-GenBank%20Data-ef5350?style=for-the-badge&logo=ncbi&logoColor=white)](https://www.ncbi.nlm.nih.gov/nuccore/NM_001045.5)
[![COMSATS](https://img.shields.io/badge/COMSATS-University%20Islamabad-42a5f5?style=for-the-badge&logo=university&logoColor=white)](https://comsats.edu.pk)
[![Group](https://img.shields.io/badge/Group-01__SLC6A4-ab47bc?style=for-the-badge&logo=users&logoColor=white)](#-team-and-academic-context)

<br/>

> ### 🎓 Bioinformatics Analysis Lab — Final Project
> Our major is **Bioinformatics (BSB)**. This repository houses an end-to-end computational genomics pipeline designed to simulate, map, and functionally evaluate single-nucleotide polymorphisms (SNPs) within the human **Serotonin Transporter (SLC6A4)** gene locus. Utilizing custom string algorithms, next-generation sequencing (NGS) window modeling, **Bowtie2 alignment engines**, and systems-level interaction topologies, we map genetic variation directly down to physical biochemical alterations.

<br/>

---

**[🏠 Pipeline Overview](#-pipeline-overview)** &nbsp;·&nbsp;
**[📦 Directory Structure](#-repository-directory-structure)** &nbsp;·&nbsp;
**[🔬 Methodology](#%EF%B8%8F-computational-methodology)** &nbsp;·&nbsp;
**[📊 Results & Matrices](#-pipeline-results--genomic-matrices)** &nbsp;·&nbsp;
**[🕸️ Network Topology](#%EF%B8%8F-systems-level-network-topology)** &nbsp;·&nbsp;
**[⚡ Getting Started](#-execution--getting-started)** &nbsp;·&nbsp;
**[👥 Academic Context](#-team-and-academic-context)**

---

</div>

## 🏠 Pipeline Overview

<table>
<tr>
<td width="55%">

### 🧠 The Biological Target
The ***SLC6A4*** gene (Chromosome 17q11.2) encodes the integral membrane serotonin transporter protein, which governs the magnitude and duration of serotonergic signaling by recycling serotonin ($5\text{-HT}$) from the synaptic cleft back into presynaptic neurons. 

Dysregulation of this apparatus is heavily implicated in major depressive disorder (MDD), clinical anxiety, obsessive-compulsive disorder (OCD), and differential pharmacological responsiveness to Selective Serotonin Reuptake Inhibitors (SSRIs).

### 💻 Our Computational Solution
We engineered a rigorous baseline simulation pipeline to model variant exposure. Point mutations were programmatically induced into the full-length coding sequence (CDS) transcript, verified via matrix string distance algorithms, sliced into overlapping high-coverage NGS fragments, globally mapped against an indexed reference utilizing **Bowtie2**, and traced up to a directed **Cytoscape interaction network** to map genotypes directly to functional phenotypes.

</td>
<td width="45%" align="center">

### 📊 Pipeline Performance Metrics

| Metric Component | Pipeline Attribute |
|:---|:---|
| 🧬 Target Locus | Human *SLC6A4* |
| 🔢 Sequence Length | **1,893 bp** (Full CDS) |
| 🛠️ Mutation Type | Point Substitutions (SNPs) |
| 📏 String Edit Distance | **Exactly 3** (Levenshtein) |
| 🎞️ Simulated Fragment Length | **50 bp** |
| 🔀 Step Shift Overlap | **10 bp** |
| 📦 Total Generated Reads | **185 synthetic fragments** |
| 🏆 Mapping Accuracy | **100% Successful** |
| 🟢 Alignment Engine State | `FLAG 0` (Forward Match) |
| 🎛️ Network Framework | Cytoscape Hierarchical Tree |

> 💡 **Pipeline Breakthrough:** Short-read alignment engines require unified alphabets. Running nucleotide fragments against protein coordinates results in unmapped states (`FLAG 4`). Resolving this via a pure DNA index guarantees perfect mapping execution.

</td>
</tr>
</table>

---

## 📦 Repository Directory Structure

> Keep this file tree structure unchanged so execution engines can locate reference headers and code targets cleanly.