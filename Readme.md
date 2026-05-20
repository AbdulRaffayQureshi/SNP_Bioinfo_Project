<div align="center">

<!-- ANIMATED WAVE HEADER -->
<img src="https://capsule-render.vercel.app/api?type=waving&color=0:050e1a,40:005B60,100:0097a7&height=240&section=header&text=🧬%20SLC6A4%20Variant%20Pipeline&fontSize=48&fontColor=e0f7fa&fontAlignY=42&desc=SNP%20Detection%20%7C%20NGS%20Simulation%20%7C%20Bowtie2%20Alignment%20%7C%20Cytoscape%20Network&descAlignY=62&descSize=15&descColor=90caf9&animation=fadeIn" width="100%"/>

<!-- TYPING SVG -->
<a href="https://github.com/AbdulRaffayQureshi/SNP_Bioinfo_Project">
  <img src="https://readme-typing-svg.demolab.com?font=Fira+Code&weight=600&size=22&pause=1000&color=00D4FF&center=true&vCenter=true&width=700&lines=Computational+Genomics+Pipeline+%F0%9F%A7%AC;SLC6A4+%E2%80%94+Serotonin+Transporter+Gene;3+SNPs+%7C+206+NGS+Reads+%7C+100%25+Alignment;Group+01+%C2%B7+COMSATS+University+Islamabad" alt="Typing SVG"/>
</a>

<br/>

<!-- BADGES -->
<p>
  <img src="https://img.shields.io/badge/Python-3.10+-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Python"/>
  <img src="https://img.shields.io/badge/Jupyter-Notebook-F37626?style=for-the-badge&logo=jupyter&logoColor=white" alt="Jupyter"/>
  <img src="https://img.shields.io/badge/Bowtie2-Alignment-189fdd?style=for-the-badge&logo=linux&logoColor=white" alt="Bowtie2"/>
  <img src="https://img.shields.io/badge/Galaxy-Platform-276A8F?style=for-the-badge&logoColor=white" alt="Galaxy"/>
</p>
<p>
  <img src="https://img.shields.io/badge/Cytoscape-Network-ea580c?style=for-the-badge&logoColor=white" alt="Cytoscape"/>
  <img src="https://img.shields.io/badge/NCBI-NM__001045.5-ef5350?style=for-the-badge&logoColor=white" alt="NCBI"/>
  <img src="https://img.shields.io/badge/Gene-SLC6A4-ab47bc?style=for-the-badge&logoColor=white" alt="Gene"/>
  <img src="https://img.shields.io/badge/Group-01__SLC6A4-00897b?style=for-the-badge&logoColor=white" alt="Group"/>
</p>

<br/>

<!-- STAT CHIPS -->
<img src="https://img.shields.io/badge/🧬%20CDS%20Length-2%2C102%20bp-005B60?style=flat-square&labelColor=0a1a2e" alt="CDS"/>
<img src="https://img.shields.io/badge/⚡%20SNPs%20Introduced-3-cc6600?style=flat-square&labelColor=0a1a2e" alt="SNPs"/>
<img src="https://img.shields.io/badge/🎞️%20Reads%20Generated-206-189fdd?style=flat-square&labelColor=0a1a2e" alt="Reads"/>
<img src="https://img.shields.io/badge/🏆%20Alignment%20Rate-100%25-00897b?style=flat-square&labelColor=0a1a2e" alt="Alignment"/>
<img src="https://img.shields.io/badge/🏳️%20SAM%20Flag-FLAG%200-ab47bc?style=flat-square&labelColor=0a1a2e" alt="Flag"/>

<br/><br/>

<!-- SNAKE ANIMATION -->
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/platane/snk/output/github-contribution-grid-snake-dark.svg"/>
  <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/platane/snk/output/github-contribution-grid-snake.svg"/>
  <img alt="github contribution grid snake animation" src="https://raw.githubusercontent.com/platane/snk/output/github-contribution-grid-snake.svg" width="80%"/>
</picture>

</div>

---

## 📋 Table of Contents

- [Project Overview](#-project-overview)
- [Biological Background](#-biological-background)
- [Pipeline](#%EF%B8%8F-pipeline)
- [Mutations Introduced](#-mutations-introduced)
- [Repository Structure](#-repository-structure)
- [Setup & Usage](#-setup--usage)
- [Results](#-results)
- [Network Topology](#%EF%B8%8F-network-topology)
- [Team](#-team)
- [References](#-references)

---

## 🔬 Project Overview

This repository contains an end-to-end computational genomics pipeline for simulating, mapping, and functionally evaluating **single-nucleotide polymorphisms (SNPs)** within the human **Serotonin Transporter (SLC6A4)** gene.

<div align="center">

```
Sequence Acquisition ──► SNP Induction ──► Edit Distance ──► NGS Simulation
                                                                     │
          Cytoscape Network ◄── ORF Prediction ◄── Variant Detection ◄── Bowtie2 Alignment
```

</div>

---

## 🧠 Biological Background

<img align="right" src="https://readme-typing-svg.demolab.com?font=Fira+Code&size=13&pause=2000&color=00897B&center=true&vCenter=true&width=280&lines=Chr+17q11.2+%F0%9F%A7%AC;12-TM+Domain+Protein;SSRI+Primary+Target;MDD+%7C+OCD+%7C+Anxiety" alt="bio"/>

The **SLC6A4** gene (*Solute Carrier Family 6 Member 4*) on chromosome **17q11.2** encodes the **serotonin transporter protein (SERT)** — a 12-transmembrane domain integral membrane protein responsible for reuptaking serotonin (5-HT) from the synaptic cleft.

SERT is the **primary molecular target of SSRIs**. Dysregulation is implicated in:

- 🧠 Major Depressive Disorder (MDD)
- 🔁 Obsessive-Compulsive Disorder (OCD)
- 😰 Generalised Anxiety Disorder
- 💊 Differential SSRI pharmacological response

<br clear="right"/>

---

## ⚙️ Pipeline

### Step 1 — Sequence Acquisition
Retrieved **NM_001045.5** from NCBI GenBank in FASTA format. Full CDS: **2,102 bp**.

### Step 2 — SNP Introduction

```python
def introduce_snp(sequence, position, new_nucleotide):
    index = position - 1
    seq_list = list(sequence)
    seq_list[index] = new_nucleotide
    return "".join(seq_list)

mutated_sequence = introduce_snp(original_sequence, 12, 'T')  # A→T
mutated_sequence = introduce_snp(mutated_sequence,  45, 'G')  # T→G
mutated_sequence = introduce_snp(mutated_sequence,  78, 'C')  # A→C
```

### Step 3 — Edit Distance Validation

```python
def calculate_edit_distance(seq1, seq2):
    distance = sum(1 for a, b in zip(seq1, seq2) if a != b)
    return distance

# Output ✓  →  Edit Distance = 3
```

### Step 4 — NGS Read Simulation

```python
def simulate_ngs_reads(sequence, read_length=50, step_size=10):
    reads = []
    start, read_count = 0, 1
    while start + read_length <= len(sequence):
        reads.append(f">Read_{read_count}\n{sequence[start:start+read_length]}")
        start += step_size
        read_count += 1
    return reads

# Output ✓  →  206 synthetic reads generated
```

### Step 5 — Alignment (Bowtie2 on Galaxy)

> ⚠️ **Critical:** Build the reference index from the **DNA sequence**, not protein.
> Protein-alphabet indexing → `FLAG 4` (unmapped). DNA indexing → `FLAG 0` (100% aligned ✓)

### Step 6 → Variant Detection &nbsp;|&nbsp; Step 7 → ORF Prediction &nbsp;|&nbsp; Step 8 → Cytoscape Network

---

## ⚡ Mutations Introduced

<div align="center">

| Position | Original | Mutant | Amino Acid Change | Classification | Polarity Impact |
|:---:|:---:|:---:|:---:|:---:|:---|
| **12** | `A` | `T` | Glu → Glu | 🟢 **Synonymous** | No change |
| **45** | `T` | `G` | Asn → Lys | 🟠 **Non-synonymous** | Polar → Positively charged (+) |
| **78** | `A` | `C` | Arg → Pro | 🔴 **Non-synonymous** | +Charge lost · α-helix disrupted |

</div>

### 🔍 Special Task — Polarity & Charge Analysis

| | Position 12 | Position 45 | Position 78 |
|:---|:---:|:---:|:---:|
| **Change** | A → T | T → G | A → C |
| **Codon** | GAG → GAT | AAT → AAG | CGA → Pro |
| **Amino Acid** | Glu = Glu | Asn → Lys | Arg → Pro |
| **Charge** | Neutral | Gains **+** | Loses **+** |
| **Structure** | ✅ Intact | ✅ Intact | ❌ Helix broken |
| **Impact** | Silent | Moderate | **High** |

> 🔴 **Position 78 is the highest-impact variant** — Proline is a helix-breaker that disrupts the α-helical transmembrane domain of SERT, potentially causing misfolding, reduced 5-HT binding affinity, and impaired SSRI efficacy.

---

## 📁 Repository Structure

```
SNP_Bioinfo_Project/
│
├── 📓 BALabProject.ipynb                    # Main pipeline (all 8 steps)
│
├── 🧬 slc6a4_original_sequence.txt          # Reference FASTA — NM_001045.5 (2102 bp)
├── ⚡ simulated_mutated_reads.txt           # 206 synthetic NGS reads (FASTA)
│
├── 📄 Bioinformatics_Analysis_Report.docx   # Written report
├── 📋 Lab_Final_Project_Brief.pdf           # Assignment specification
│
└── 📖 README.md                             # This file
```

---

## 🚀 Setup & Usage

### Prerequisites

```bash
pip install jupyter notebook
```

### Clone & Run

```bash
git clone https://github.com/AbdulRaffayQureshi/SNP_Bioinfo_Project.git
cd SNP_Bioinfo_Project
jupyter notebook BALabProject.ipynb
```

### Execute cells in order

```
[1]  Load original SLC6A4 sequence (2102 bp)
[2]  Introduce SNPs at positions 12, 45, 78
[3]  Compute edit distance  →  Expected: 3
[4]  Simulate 206 NGS reads (50 bp, step 10)
[5]  Export simulated_mutated_reads.fasta + reference FASTA
[6]  Upload to Galaxy → align with Bowtie2 (DNA index!)
[7]  Inspect SAM output → mismatches at 12, 45, 78  ✓
```

---

## 📊 Results

<div align="center">

<img src="https://img.shields.io/badge/Edit%20Distance-3%20%E2%9C%93-005B60?style=for-the-badge&labelColor=0a1a2e" alt="Edit Distance"/>
<img src="https://img.shields.io/badge/Reads%20Simulated-206-189fdd?style=for-the-badge&labelColor=0a1a2e" alt="Reads"/>
<img src="https://img.shields.io/badge/Alignment%20Rate-100%25%20%E2%9C%93-00897b?style=for-the-badge&labelColor=0a1a2e" alt="Alignment"/>
<img src="https://img.shields.io/badge/SAM%20Flag-FLAG%200-ab47bc?style=for-the-badge&labelColor=0a1a2e" alt="Flag"/>
<img src="https://img.shields.io/badge/Premature%20Stop%20Codons-None%20%E2%9C%93-00897b?style=for-the-badge&labelColor=0a1a2e" alt="Stop"/>
<img src="https://img.shields.io/badge/ORF%20Frame-%2B1%20(ATG%20%E2%86%92%20TAA)-cc6600?style=for-the-badge&labelColor=0a1a2e" alt="ORF"/>

</div>

<br/>

### Full Pipeline Summary

| Metric | Result |
|:---|:---|
| Sequence length | 2,102 bp |
| Edit distance (original vs mutated) | **3** ✓ |
| Total reads simulated | **206** |
| Read length / Step size | 50 bp / 10 bp |
| Reads aligned | **206 / 206** |
| Alignment rate | **100%** |
| SAM flag | **FLAG 0** (forward strand) |
| Premature stop codons | **None** |
| ORF | Frame +1 · ATG pos.1 → TAA pos.2100 |

### Variant Classification Summary

| SNP | Classification | Charge Effect | Structural Effect |
|:---|:---|:---|:---|
| pos. 12 · A→T | 🟢 Synonymous | None | None |
| pos. 45 · T→G | 🟠 Non-synonymous | Gains + charge (Asn→Lys) | Minor |
| pos. 78 · A→C | 🔴 Non-synonymous | Loses + charge (Arg→Pro) | α-helix disrupted |

---

## 🕸️ Network Topology

Cytoscape network following the required **Gene → Variant → Effect → Function** hierarchy:

```
                            ┌─────────┐
                            │ SLC6A4  │   ← Gene
                            └────┬────┘
               ┌─────────────────┼─────────────────┐
               ▼                 ▼                 ▼
          ┌─────────┐      ┌─────────┐      ┌─────────┐
          │ SNP·12  │      │ SNP·45  │      │ SNP·78  │  ← Variants
          │  A → T  │      │  T → G  │      │  A → C  │
          └────┬────┘      └────┬────┘      └────┬────┘
               ▼                ▼                ▼
           [Silent]       [+Charge           [-Charge +
                           Asn→Lys]           Helix Break]  ← Effects
                               │                  │
                               ▼                  ▼
                         [5-HT Bind↓]     [TM Misfolding]  ← Function
                                    \          /
                                     ▼        ▼
                               [MDD Risk↑ / SSRI Response↓]
```

---

## 👥 Team

<div align="center">

| | |
|:---|:---|
| **Group** | Group 01 — SLC6A4 |
| **Program** | BS Bioinformatics (BSB) |
| **University** | COMSATS University Islamabad |
| **Course** | Bioinformatics Analysis Lab — Final Project |
| **Submission** | 20th May 2026 |

</div>

---

## 📚 References

- Blakely, R.D. et al. (1991). Cloning and expression of a functional serotonin transporter from rat brain. *Nature*, 354, 66–70.
- Langmead, B. & Salzberg, S.L. (2012). Fast gapped-read alignment with Bowtie 2. *Nature Methods*, 9, 357–359.
- Lesch, K.P. et al. (1996). Association of anxiety-related traits with a polymorphism in the serotonin transporter gene regulatory region. *Science*, 274, 1527–1531.
- NCBI NM_001045.5: https://www.ncbi.nlm.nih.gov/nuccore/NM_001045.5
- Shannon, P. et al. (2003). Cytoscape. *Genome Research*, 13, 2498–2504.

---

<!-- ANIMATED FOOTER WAVE -->
<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0097a7,60:005B60,100:050e1a&height=120&section=footer&animation=fadeIn" width="100%"/>

*🧬 SLC6A4 Variant Detection Pipeline · Group 01 · Bioinformatics Analysis Lab · COMSATS University Islamabad · 2026*

</div>