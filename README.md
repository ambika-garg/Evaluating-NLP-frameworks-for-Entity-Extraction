# MIMIC NLP: Clinical Entity Extraction for CHF Patients

## 📋 Project Overview

An end-to-end Natural Language Processing pipeline for extracting and analyzing medical entities from clinical notes of Congestive Heart Failure (CHF) patients using the MIMIC-III database.

## 🎯 Rationale

Medical notes represent a critical yet underutilized component of Electronic Health Records (EHR). Despite containing rich clinical insights about patient history, diagnoses, treatments, and outcomes, these unstructured text documents are often ignored in healthcare analytics due to:

- **Complexity Barrier**: High learning curve for understanding and applying NLP technologies to clinical text
- **Domain Specificity**: Standard NLP tools fail to capture medical terminology and context
- **Lack of Structure**: Free-text format makes systematic analysis challenging

### Why This Matters

This project addresses these challenges by demonstrating how modern NLP technologies can:

1. **Unlock Hidden Insights**: Extract structured entities (diseases, medications, procedures) from unstructured notes
2. **Enable Machine Learning**: Generate embeddings and features for predictive modeling (e.g., readmission risk, treatment outcomes)
3. **Bridge the Gap**: Connect raw clinical documentation to actionable data science applications

**Impact**: Extracted entities and embeddings become powerful features for downstream machine learning algorithms, enabling more comprehensive EHR-based predictive models.

## 🎯 Objectives

- Extract medical entities (diseases, medications, procedures) from discharge summaries
- Compare general-purpose vs. domain-specific NER models
- Generate medical word embeddings for semantic similarity analysis
- Visualize entity relationships using dimensionality reduction
- **Demonstrate end-to-end workflow** from raw notes to ML-ready features

## 📊 Dataset

**Source**: MIMIC-III Clinical Database  
**Focus**: Congestive Heart Failure (ICD-9 code: 428.0)  
**Note Type**: Discharge Summaries  
**Reasoning**: Most comprehensive documentation covering diagnosis, procedures, medications, and outcomes

## 🔧 Methodology

### 1. Named Entity Recognition (NER)

| Model | Type | Strengths | Limitations |
|-------|------|-----------|-------------|
| **spaCy (en_core_web_sm)** | General-purpose | Fast, lightweight | Misses clinical entities |
| **SciSpacy (en_core_sci_md)** | Biomedical | Trained on PubMed | Broader scientific focus |
| **SciSpacy (en_ner_bc5cdr_md)** | Clinical-specific | Identifies diseases & chemicals | Best for clinical text |

### 2. Word Embeddings (Word2Vec)

- **Architecture**: Skip-gram model
- **Training Data**: 1,000 and 2,000 CHF discharge summaries
- **Vector Dimension**: 300
- **Purpose**: Capture semantic relationships between medical terms

### 3. Contextual Analysis (medSpaCy)

Extracted contextual attributes for each entity:
- **Negation**: "No chest pain" → negated
- **Temporality**: "History of pneumonia" → historical
- **Family History**: "Family history of CAD" → family
- **Section Classification**: Past medical history, medications, etc.

### 4. Visualization (t-SNE)

Dimensionality reduction to visualize:
- Entity clustering by semantic similarity
- Model comparison (spaCy vs. SciSpacy)
- Corpus size impact (1K vs. 2K notes)

## 🏆 Key Findings

### NER Performance
✅ **SciSpacy bc5cdr** significantly outperforms general spaCy  
✅ Successfully extracted diseases (CHF, hypertension, CAD) and chemicals  
❌ General spaCy failed to recognize medical entities  

### Word2Vec Results
✅ **2,000-note model** shows better semantic clustering than 1,000-note model  
✅ Similar terms cluster together: "pain" → "discomfort", "ache"  
✅ Context-aware: captured medical relationships  

### t-SNE Visualizations
✅ SciSpacy (2K) shows **tight, meaningful clusters**  
✅ Words with 0.70+ similarity to target terms group together  
❌ General spaCy shows scattered, weakly related terms  

## ⚠️ Limitations

- Trained only on CHF patients (limited generalizability)
- Requires MIMIC-III access credentials
- Limited to English clinical text

## 📚 References

- MIMIC-III Clinical Database: https://mimic.physionet.org/
- SciSpacy: https://allenai.github.io/scispacy/
- medSpaCy: https://github.com/medspacy/medspacy

## 👤 Author

**Ambika Garg**  
*Submitted as part of Medical NLP research*

---

**Note**: This project uses de-identified MIMIC-III data. All patient information is anonymized per HIPAA requirements.
