<div align="center">

# 🧬 SLC6A4 Variant Detection Pipeline

**Computational Pipeline for SNP Detection using Simulated NGS Reads**

*Bioinformatics Analysis Lab — Final Project | Group 01 | COMSATS University Islamabad*

---

[![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://python.org)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?style=for-the-badge&logo=jupyter&logoColor=white)](https://jupyter.org)
[![Galaxy](https://img.shields.io/badge/Galaxy-Platform-276A8F?style=for-the-badge&logo=data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyNCAyNCI+PHBhdGggZmlsbD0id2hpdGUiIGQ9Ik0xMiAyQzYuNDggMiAyIDYuNDggMiAxMnM0LjQ4IDEwIDEwIDEwIDEwLTQuNDggMTAtMTBTMTcuNTIgMiAxMiAyem0tMSAxNy45M1Y0LjA3YzMuOTQuNDkgNyAzLjg1IDcgNy45M3MtMy4wNiA3LjQ0LTcgNy45M3oiLz48L3N2Zz4=&logoColor=white)](https://usegalaxy.org)
[![Bowtie2](https://img.shields.io/badge/Bowtie2-Alignment-189fdd?style=for-the-badge&logo=linux&logoColor=white)](https://bowtie-bio.sourceforge.net/bowtie2)
[![Cytoscape](https://img.shields.io/badge/Cytoscape-Network-ea580c?style=for-the-badge&logo=cytoscape&logoColor=white)](https://cytoscape.org)
[![NCBI](https://img.shields.io/badge/NCBI-NM__001045.5-ef5350?style=for-the-badge&logo=ncbi&logoColor=white)](https://www.ncbi.nlm.nih.gov/nuccore/NM_001045.5)

---

| 🧬 Gene | 📏 CDS Length | ⚡ SNPs | 🎞️ Reads | 🏆 Alignment |
|:---:|:---:|:---:|:---:|:---:|
| **SLC6A4** | **2,102 bp** | **3** | **206** | **100%** |

</div>

---

## 📋 Table of Contents

- [Project Overview](#-project-overview)
- [Biological Background](#-biological-background)
- [Pipeline](#-pipeline)
- [Mutations Introduced](#-mutations-introduced)
- [Repository Structure](#-repository-structure)
- [Setup & Usage](#-setup--usage)
- [Results](#-results)
- [Network Topology](#-network-topology)
- [Team](#-team)

---

## 🔬 Project Overview

This repository contains an end-to-end computational genomics pipeline for simulating, mapping, and functionally evaluating **single-nucleotide polymorphisms (SNPs)** within the human **Serotonin Transporter (SLC6A4)** gene.

The pipeline covers the complete workflow required by the Bioinformatics Analysis Lab Final Project:

```
Sequence Acquisition → SNP Induction → Edit Distance → NGS Simulation
        → Bowtie2 Alignment → Variant Detection → ORF Prediction → Cytoscape Network
```

---

## 🧠 Biological Background

The **SLC6A4** gene (*Solute Carrier Family 6 Member 4*) on chromosome **17q11.2** encodes the **serotonin transporter protein (SERT)** — a 12-transmembrane domain integral membrane protein responsible for reuptaking serotonin (5-HT) from the synaptic cleft back into presynaptic neurons.

SERT is the **primary molecular target of SSRIs** (selective serotonin reuptake inhibitors). Dysregulation of this transporter is mechanistically implicated in:

- Major Depressive Disorder (MDD)
- Obsessive-Compulsive Disorder (OCD)
- Generalised Anxiety Disorder
- Differential SSRI pharmacological response

---

## ⚙️ Pipeline

### Step 1 — Sequence Acquisition
Retrieved **NM_001045.5** from NCBI GenBank in FASTA format. Full CDS: **2,102 bp**.

### Step 2 — SNP Introduction
Three point mutations introduced programmatically at positions **12**, **45**, and **78**:

```python
def introduce_snp(sequence, position, new_nucleotide):
    index = position - 1
    seq_list = list(sequence)
    seq_list[index] = new_nucleotide
    return "".join(seq_list)

mutated_sequence = introduce_snp(original_sequence, 12, 'T')  # A→T
mutated_sequence = introduce_snp(mutated_sequence, 45, 'G')   # T→G
mutated_sequence = introduce_snp(mutated_sequence, 78, 'C')   # A→C
```

### Step 3 — Edit Distance Validation
Hamming distance computed between original and mutated sequences:

```python
def calculate_edit_distance(seq1, seq2):
    distance = sum(1 for a, b in zip(seq1, seq2) if a != b)
    return distance

# Output: Edit Distance = 3 ✓
```

### Step 4 — NGS Read Simulation
Sliding window approach generating **50 bp reads** with **10 bp step size**:

```python
def simulate_ngs_reads(sequence, read_length=50, step_size=10):
    reads = []
    start = 0
    read_count = 1
    while start + read_length <= len(sequence):
        read_seq = sequence[start : start + read_length]
        reads.append(f">Read_{read_count}\n{read_seq}")
        start += step_size
        read_count += 1
    return reads

# Output: 206 synthetic reads ✓
```

### Step 5 — Alignment (Galaxy / Bowtie2)
Reads aligned against a **DNA reference index** using Bowtie2 on Galaxy.

> ⚠️ **Critical:** Use a DNA-alphabet index, not a protein index. Protein indexing yields `FLAG 4` (unmapped). DNA indexing yields `FLAG 0` (forward match) — 100% alignment.

### Step 6 — Variant Detection
Mismatches at positions **12, 45, 78** in SAM output confirm all three introduced SNPs.

### Step 7 — ORF Prediction
One ORF confirmed in frame +1: ATG (pos. 1) → TAA (pos. 2100). No premature stop codons introduced.

### Step 8 — Cytoscape Network
Directed network: **Gene → Variant → Effect → Function**

---

## ⚡ Mutations Introduced

| Position | Original | Mutant | Codon Change | Amino Acid Change | Type | Polarity Impact |
|:---:|:---:|:---:|:---:|:---:|:---:|:---|
| **12** | `A` | `T` | GAG → GAT | Glu → Glu | 🟢 Synonymous | No change |
| **45** | `T` | `G` | AAT → AAG | Asn → Lys | 🟠 Non-synonymous | Polar → Positively charged (+) |
| **78** | `A` | `C` | CGA → Pro | Arg → Pro | 🔴 Non-synonymous | Positive charge lost + helix disrupted |

### Special Task — Polarity & Charge Analysis

- **Position 12** — Silent mutation. No amino acid or charge change.
- **Position 45** — Asparagine (polar, uncharged) → Lysine (basic, +charged). Positive charge gain at SERT N-terminal region.
- **Position 78** — Arginine (positively charged) → Proline (nonpolar, helix-breaker). **Most impactful variant**: loss of electrostatic membrane interaction + α-helix disruption in transmembrane domain.

---

## 📁 Repository Structure

```
SNP_Bioinfo_Project/
│
├── 📓 BALabProject.ipynb               # Main pipeline notebook (all steps)
│
├── 🧬 slc6a4_original_sequence.txt     # Reference FASTA — NM_001045.5 (2102 bp)
├── ⚡ simulated_mutated_reads.txt      # 206 synthetic NGS reads (FASTA format)
│
├── 📄 Bioinformatics_Analysis_Report.docx  # Written report
├── 📋 Lab_Final_Project_Brief.pdf          # Assignment specification
│
└── 📖 README.md                        # This file
```

---

## 🚀 Setup & Usage

### Prerequisites

```bash
pip install jupyter notebook
```

### Run the Pipeline

```bash
git clone https://github.com/AbdulRaffayQureshi/SNP_Bioinfo_Project.git
cd SNP_Bioinfo_Project
jupyter notebook BALabProject.ipynb
```

### Run cells in order:
1. Load original SLC6A4 sequence
2. Introduce SNPs at positions 12, 45, 78
3. Compute edit distance (expected: `3`)
4. Simulate 206 NGS reads
5. Export `simulated_mutated_reads.fasta` + reference FASTA
6. Upload both to Galaxy → align with Bowtie2
7. Inspect SAM output for mismatches at 12, 45, 78

---

## 📊 Results

### Pipeline Summary

| Metric | Result |
|:---|:---|
| Sequence length | 2,102 bp |
| Edit distance (original vs mutated) | **3** |
| Total reads simulated | **206** |
| Read length | 50 bp |
| Step size | 10 bp |
| Reads aligned | **206 / 206** |
| Alignment rate | **100%** |
| SAM flag | **FLAG 0** (forward strand) |
| Premature stop codons | None |
| ORF frame | +1 (ATG pos.1 → TAA pos.2100) |

### Variant Summary

| SNP | Classification | Charge Effect |
|:---|:---|:---|
| pos. 12 A→T | Synonymous | None |
| pos. 45 T→G | Non-synonymous | Gains positive charge (Asn→Lys) |
| pos. 78 A→C | Non-synonymous | Loses positive charge + helix broken (Arg→Pro) |

> **2 of 3 SNPs are functionally significant** with direct polarity/charge consequences at the protein level.

---

## 🕸️ Network Topology

Cytoscape network following required **Gene → Variant → Effect → Function** topology:

```
                        SLC6A4
                       /   |   \
                      /    |    \
              SNP_12  SNP_45  SNP_78
                 |       |        |
             Silent  +Charge   -Charge
                         |     +HelixBreak
                         |        |
                    5-HT bind↓  TM misfolding
                              \     /
                           MDD Risk ↑ / SSRI Response ↓
```

---

## 👥 Team

| | Detail |
|:---|:---|
| **Group** | Group 01 — SLC6A4 |
| **Program** | BS Bioinformatics (BSB) |
| **University** | COMSATS University Islamabad |
| **Course** | Bioinformatics Analysis Lab |
| **Due Date** | 20th May 2026 |

---

## 📚 References

- Blakely, R.D. et al. (1991). Cloning and expression of a functional serotonin transporter from rat brain. *Nature*, 354, 66–70.
- Langmead, B. & Salzberg, S.L. (2012). Fast gapped-read alignment with Bowtie 2. *Nature Methods*, 9, 357–359.
- Lesch, K.P. et al. (1996). Association of anxiety-related traits with a polymorphism in the serotonin transporter gene regulatory region. *Science*, 274, 1527–1531.
- NCBI NM_001045.5: https://www.ncbi.nlm.nih.gov/nuccore/NM_001045.5

---

<div align="center">

*SLC6A4 Variant Detection Pipeline · Group 01 · Bioinformatics Analysis Lab · COMSATS University Islamabad · 2026*

</div>