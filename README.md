# Clinical_trial_Matching

# 🧠 Clinical Trial Matching AI

This project builds an intelligent agentic system to match real-world patient records with clinical trials from [ClinicalTrials.gov](https://clinicaltrials.gov/). It uses multiple NLP techniques and large language models (LLMs) to extract patient data, semantically filter trials, and generate explainable match decisions.

---

## 🧾 Project Goals

- ✅ Extract structured information from unstructured clinical notes
- ✅ Retrieve and rank relevant clinical trials
- ✅ Use LLMs like Claude to evaluate eligibility and explain trial matches
- ✅ Enable clinicians to review and query patient-trial matches interactively

---

## 📦 Data Sources

- **Patients Dataset**: [PMC-Patients-V2](https://huggingface.co/datasets/zhengyun21/PMC-Patients) — contains clinical notes, demographics
- **Clinical Trials**: Fetched from [ClinicalTrials.gov API v2](https://clinicaltrials.gov/api/v2/) or loaded from `ctg-studies.json`

---

## 🧰 Techniques & Tools Used

### 🔍 Named Entity Recognition (NER)
- **Stanza** — Extracts `PROBLEM`, `TEST`, `TREATMENT`
- **AWS Comprehend Medical** — Extracts `MEDICAL_CONDITION`, `MEDICATION`, `TEST_TREATMENT_PROCEDURE`
- **Claude LLM** — Zero-shot structured extraction: demographics, conditions, medications, history

### 🧠 Semantic Matching
- **Mistral Embeddings** — Used for patient/trial vector similarity
- **Keyword Matching** — Rule-based match between patient and trial eligibility
- **Cosine Similarity** — For ranking matched trials

### 💬 LLM Reasoning
- **Anthropic Claude 3 (via Bedrock)** — Determines final eligibility decision with reasoning based on inclusion/exclusion criteria

---

## ⚙️ How It Works

1. **Extract** structured patient data from clinical notes using NER and Claude
2. **Filter** and **embed** clinical trials using Mistral or Claude embeddings
3. **Match** trials using:
   - Cosine similarity
   - Shared keywords
   - LLM-based eligibility evaluation
4. **Explain** matches with Claude: generates a score + reasoning

---

## 📊 Output Example

Each patient receives a ranked list of trials with:
- `trial_id`
- `title`
- `match_score`
- `match: YES/NO`
- `explanation`: natural language rationale

---

## 🔒 Security & Credentials

- AWS credentials required for:
  - `boto3` access to **Bedrock Claude**
  - **Comprehend Medical** usage
- Use `.env` or environment variables in Colab:
  ```python
  os.environ["AWS_ACCESS_KEY_ID"] = "..."
  os.environ["AWS_SECRET_ACCESS_KEY"] = "..."
