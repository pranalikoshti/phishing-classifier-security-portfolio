# AI-Powered Phishing & Spam Email Classifier

**Author:** Pranali Koshti  
**Date:** April 2026  
**Role Target:** SOC Analyst · Network Security Engineer  
**Tools:** Python · scikit-learn · NLTK · TF-IDF · pandas · matplotlib · seaborn  

---

## Project Overview

This project builds an NLP-based machine learning classifier that detects 
phishing and spam messages with high accuracy. The model is trained on 5,500+ 
real labeled SMS and email messages from the UCI SMS Spam Collection dataset.

The project demonstrates AI-assisted threat detection — automating the kind 
of pattern recognition that a Tier 1 SOC analyst performs manually during 
phishing triage, and directly addresses the 2026 threat landscape where 
vishing and SMS-based social engineering attacks are surging per Google 
Mandiant M-Trends 2026.

---

## Results

**Best model:** Random Forest
**Final accuracy:** [97.8]%  
**Phishing recall:** [83.2]%  
**False negative rate:** [90.8]%  


---

## Key Security Insight

Several phishing messages in this dataset would score low on 
signature-based detection tools because they use no known-bad URLs 
or IPs — they rely purely on social engineering language. The model 
catches them through linguistic pattern recognition alone.

Top phishing indicator words identified by the model:
- win
- prize
- servic
- text
- repli
- mobil
- claim
- free
- call
- txt

These map directly to MITRE ATT&CK T1566 (Phishing) — specifically 
the lure content, urgency, and credential harvesting sub-techniques.

The false negatives — phishing messages the model missed — were 
predominantly BEC-style messages using professional language with 
no obvious phishing keywords. This demonstrates why human-in-the-loop 
validation remains essential even in AI-assisted SOC triage.

---

## MITRE ATT&CK Coverage

| Technique ID | Technique Name | Tactic | Relevance |
|-------------|----------------|--------|-----------|
| T1566 | Phishing | Initial Access | Primary detection target |
| T1566.001 | Spearphishing Attachment | Initial Access | Email-based lures |
| T1566.002 | Spearphishing Link | Initial Access | URL-based phishing |
| T1598 | Phishing for Information | Reconnaissance | Credential harvesting messages |

---

## Visualizations

### Dataset Analysis
![Dataset Analysis](screenshots/dataset-analysis.png)

### Model Comparison
![Model Comparison](screenshots/model-comparison.png)

### Confusion Matrix
![Confusion Matrix](screenshots/confusion-matrix.png)

### Feature Importance — Top Phishing Indicator Words
![Feature Importance](screenshots/feature-importance.png)

### Live Classifier Demo
![Classifier Demo](screenshots/classifier-demo.png)

---

## Project Architecture

Raw SMS/Email Text
↓
Text Cleaning (lowercase, remove URLs, remove punctuation, stopwords, stemming)
↓
TF-IDF Vectorization (5000 features, unigrams + bigrams)
↓
Train/Test Split (80/20, stratified)
↓
Model Training (Naive Bayes, Logistic Regression, Random Forest)
↓
Evaluation (Accuracy, Precision, Recall, F1, Confusion Matrix)
↓
Best Model Selection (by F1 score)
↓
Feature Importance Analysis (top phishing indicator words)
↓
Live Demo (paste any message, get prediction + trigger words)

---

## Why F1 Score and Not Just Accuracy

The dataset has a class imbalance — approximately 87% legitimate and 
13% phishing. A model that always predicts legitimate would achieve 
87% accuracy while catching zero phishing messages.

F1 score balances precision and recall:
- Precision — of all messages flagged as phishing, how many were actually phishing
- Recall — of all actual phishing messages, how many did the model catch

In a security context recall matters most. Missing a phishing email 
in a CFO inbox is worse than generating a false alarm that gets 
reviewed and cleared. The model is optimized accordingly.

---

## How to Run

### Option 1 — Google Colab (recommended, no installation needed)
1. Open Google Colab at colab.research.google.com
2. Upload the phishing_classifier.ipynb notebook
3. Runtime → Run All
4. All libraries install automatically

### Option 2 — Local installation
```bash
git clone https://github.com/[your-username]/ai-phishing-email-classifier
cd ai-phishing-email-classifier
pip install -r requirements.txt
jupyter notebook phishing_classifier.ipynb
```

---

## Dataset

Source: UCI SMS Spam Collection Dataset  
Size: 5,572 labeled messages  
Classes: ham (legitimate) — 4,825 messages · spam (phishing) — 747 messages  
Loaded directly from URL — no download required  

---

## Technologies Used

- Python 3.x
- scikit-learn — TF-IDF vectorization, model training, evaluation metrics
- NLTK — stopwords, stemming, text tokenization
- pandas — data loading and manipulation
- numpy — numerical operations
- matplotlib + seaborn — confusion matrix and model comparison charts
- WordCloud — phishing word visualization

---

## Skills Demonstrated

- Natural Language Processing (NLP)
- Machine Learning model training and evaluation
- Feature engineering for text classification
- Security-focused model evaluation (precision vs recall trade-off)
- AI-assisted threat detection automation
- MITRE ATT&CK framework mapping
- Python scripting and data visualization

---

## Connection to Real Security Work

At Samsung Electronics I manually investigated suspicious network 
traffic patterns and anomalous behavior across live production 
infrastructure. This project automates the first layer of that 
pattern recognition — catching phishing attempts at the delivery 
stage before they become incidents.

The same pipeline logic applies directly to enterprise email security 
tooling and Agentic SOC alert triage, where AI models handle initial 
classification and human analysts focus on ambiguous or high-severity cases.

---

## About

Built as part of my cybersecurity portfolio while completing my MS in 
Management Information Systems (cybersecurity concentration) at the 
University at Buffalo, graduating May 2026.

3 years of production network security experience at Samsung Electronics 
including SIRT operations, IAM design for 10,000+ node nationwide 
deployments, and Wireshark-based security testing of India's national 
Emergency Alert System.

Connect: linkedin.com/in/pranalikoshti
