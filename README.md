# 🏥 Applied Prompt Engineering for Healthcare Using LLMs
### Medical Note Simplification — A Step-by-Step Tutorial

![Python](https://img.shields.io/badge/Python-3.10-blue?logo=python)
![OpenAI](https://img.shields.io/badge/OpenAI-GPT--3.5--turbo-412991?logo=openai)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange?logo=jupyter)
![License](https://img.shields.io/badge/License-MIT-green)
![University](https://img.shields.io/badge/UT%20Austin-AI%20in%20Healthcare-bf5700)

---

## 📌 Overview

Medical notes and clinical abstracts are written for trained professionals. Patients — who have a legal right to understand their own health — often find these notes confusing and overwhelming.

This tutorial demonstrates how **Large Language Models (LLMs)** combined with advanced **prompt engineering techniques** can automatically simplify medical notes for three different patient literacy levels:

| Audience | Description |
|---|---|
| 👶 **5th Grade** | Patient with no medical background — simple words, no jargon |
| 🎓 **High School** | Educated patient — some terms okay, always explained |
| 👨‍⚕️ **Medical Professional** | Nurse or intern — structured, concise, clinical bullets |

---

## 🎯 What This Tutorial Covers

| # | Method | What It Does |
|---|---|---|
| 1 | **Zero-Shot Prompting** | Baseline — no examples, GPT relies on pre-trained knowledge |
| 2 | **Few-Shot / In-Context Learning** | 2 examples guide the model's expected style and format |
| 3 | **Chain-of-Thought (CoT)** | Forces step-by-step reasoning before producing the final answer |
| 4 | **Tree-of-Thought (ToT)** | Explores 3 expert reasoning paths simultaneously, selects the best |
| 5 | **Tabular → Text Conversion** | Converts raw patient CSV data into readable medical summaries |
| 6 | **LLM-as-Judge Evaluation** | Uses GPT itself to score and compare all method outputs |

---

## 🗂️ Datasets Used

### 1. EBM-NLP — Evidence Based Medicine NLP
- Collection of clinical trial abstracts from PubMed
- Dense medical language covering diabetes, hypertension, depression, asthma and COVID-19
- Used for: Zero-Shot, Few-Shot, CoT and ToT simplification tasks
- 🔗 [github.com/bepnye/EBM-NLP](https://github.com/bepnye/EBM-NLP)

### 2. Synthea — Synthetic Patient Data by MITRE Corporation
- 100 synthetic but clinically realistic patients
- CSV files: patients.csv, conditions.csv, medications.csv
- Used for: Tabular to Text conversion, CoT and ToT patient profiling
- 🔗 [synthea.mitre.org/downloads](https://synthea.mitre.org/downloads)

> ⚠️ All data used in this tutorial is **synthetic or publicly available**. No real patient data is used. This project complies with OpenAI's usage policies.

---

## 🔁 End-to-End Pipeline

| Stage | Details |
|---|---|
| **Data Sources** | EBM-NLP text notes + Synthea patient CSVs (both used in CoT and ToT) |
| **Preprocessing** | Load text into Python list / Merge CSVs into patient profile |
| **Zero-Shot Input** | Clinical note + instruction (simplify for X level) |
| **Few-Shot Input** | Clinical note + instruction + example 1 + example 2 |
| **CoT Input** | Clinical note + instruction + step 1 + step 2 + step 3 |
| **ToT Input** | Clinical note + instruction + expert 1 path + expert 2 path + expert 3 path |
| **GPT API Call 1** | gpt-3.5-turbo via client.chat.completions.create() — simplification |
| **Output** | 3 versions — 5th grade / high school / medical professional |
| **GPT API Call 2** | LLM-as-Judge — scores clarity, accuracy, appropriateness (1-10) |
| **Winner** | Tree-of-Thought — 27/30 |

---

## 🏆 Evaluation Results

Outputs scored by GPT-as-Judge on 3 criteria — Clarity, Accuracy and Appropriateness (each out of 10):

| Method | Clarity | Accuracy | Appropriateness | Total /30 |
|---|---|---|---|---|
| Zero-Shot | 7 | 7 | 6 | 20 |
| Few-Shot (ICL) | 8 | 8 | 8 | 24 |
| Chain-of-Thought | 8 | 9 | 8 | 25 |
| **🏆 Tree-of-Thought** | **9** | **9** | **9** | **27** |

**Key Finding:** Tree-of-Thought outperformed all methods. Multi-expert reasoning produced the most thorough, accurate and patient-appropriate simplifications across all literacy levels.

---

## ⚙️ Setup & Usage

### Prerequisites
- Google Colab account (free)
- OpenAI API key with minimum $5 credits — [platform.openai.com](https://platform.openai.com)
- Synthea 100-patient dataset — [download here](https://synthea.mitre.org/downloads)

### Step 1 — Open Notebook in Colab
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/mdfrahim1/Applied-Prompt-Engineering-for-Healthcare-using-LLMs/blob/main/AI_Healthcare_LLM_Tutorial.ipynb)

### Step 2 — Set Up API Key Securely
1. Go to [platform.openai.com](https://platform.openai.com) and create a new API key
2. In Colab click the 🔑 Secrets icon in the left sidebar
3. Add a new secret named exactly: OPENAI_API_KEY
4. Paste your key as the value and toggle Notebook access ON

### Step 3 — Add Synthea Data to Google Drive
1. Download the 100-patient sample from [synthea.mitre.org/downloads](https://synthea.mitre.org/downloads)
2. Unzip and upload these 3 files to your Google Drive folder: AI - Healthcare - LLM Tutorial
   - patients.csv
   - conditions.csv
   - medications.csv

### Step 4 — Mount Drive and Run
1. In Colab run the Drive mount cell first
2. Then go to Runtime → Run All

---

## 📁 Repository Structure

| File | Description |
|---|---|
| AI_Healthcare_LLM_Tutorial.ipynb | Main tutorial notebook with all code and markdown |
| AI_Healthcare_LLM_Tutorial.pptx | Presentation slides summarizing the tutorial |
| README.md | You are here |

---

## 💡 Key Learnings

- Zero-Shot is a fast baseline but produces inconsistent outputs
- Few-Shot and ICL significantly improve consistency with minimal added complexity
- Chain-of-Thought produces more accurate outputs by making reasoning transparent
- Tree-of-Thought is the most thorough method — worth the extra token cost for high-stakes tasks
- LLM-as-Judge is a viable automated evaluation strategy when human raters are unavailable
- LLMs can successfully convert raw tabular EHR data into readable, clinically accurate narratives

---

## 💡 Ideas for Future Improvement

- Human evaluation by real doctors and patients for more reliable scoring
- Flesch-Kincaid readability scores for objective literacy level measurement
- Fine-tuned healthcare-specific LLMs such as PMC-LLaMA instead of general-purpose GPT
- Multilingual support for non-English speaking patient populations
- A production web UI for real physician note simplification workflows

---

## 📚 References

1. Wei et al. (2022). Chain-of-Thought Prompting Elicits Reasoning in Large Language Models. Google Brain.
2. Yao et al. (2023). Tree of Thoughts: Deliberate Problem Solving with Large Language Models. Princeton and Google.
3. Brown et al. (2020). Language Models are Few-Shot Learners. OpenAI.
4. Singhal et al. (2023). Large Language Models Encode Clinical Knowledge. Nature.
5. Synthea Synthetic Patient Generator — [synthea.mitre.org](https://synthea.mitre.org)
6. EBM-NLP Corpus — [github.com/bepnye/EBM-NLP](https://github.com/bepnye/EBM-NLP)

---

## 📄 License
This project is licensed under the MIT License — free to use, modify and share with attribution.

---

*Built as part of the AI in Healthcare course — University of Texas, Austin*
