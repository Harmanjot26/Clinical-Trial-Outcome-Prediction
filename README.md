# Clinical Trial Outcome Prediction with XGBoost & Hybrid Features

This project predicts the success or failure of **Phase 3 clinical trials** using a hybrid machine learning approach that merges **chemical structure features** with **text-derived clinical context features**. The model is trained on the **Therapeutics Data Commons (TDC) – Trial Outcome Prediction** dataset.

---

## 📈 Feature Importance

<img width="798" height="435" alt="image" src="https://github.com/user-attachments/assets/52971c1e-dfe5-4eee-b1b9-ac8ec29b4d68" />


## 🔑 Key Features

### **Hybrid Feature Engineering**

#### **Chemical Features**
- 2048-bit **Morgan Fingerprints** created using **RDKit** from drug SMILES strings.

#### **Textual Features**
A lightweight NLP scanner analyzes eligibility criteria for specific **risk** and **safe** keywords.

- **Risk Keywords:** `tumor`, `metastatic`, `unresectable`, `refractory`, `relapsed`
- **Safe Keywords:** `pain`, `infection`, `healthy`, `volunteer`, `mild`

These are converted into numeric **Risk_Keyword_Score** and **Safe_Keyword_Score**, which significantly boost model interpretability.

---

## 🤖 Model Overview
- Uses **XGBClassifier** (XGBoost).
- Implements **scale_pos_weight** to address class imbalance.
- Outputs a **success probability** for each trial.

### **Key Insight**
The custom **Risk_Keyword_Score** emerges as the *most important predictor*, validating the usefulness of simple textual heuristics.

---

## 🧬 Dataset
- Source: **Therapeutics Data Commons (TDC)**
- Task: **Trial Outcome Prediction — Phase 3**
- Includes drug SMILES, eligibility text, trial metadata, and binary success/failure labels.

The dataset downloads automatically upon script execution.

---

## 🚀 Getting Started

### **Prerequisites**
- Python **3.7+**

### **Installation**
Clone the repository:

```bash
git clone <your-repo-url>
cd <your-repo-directory>
```

Install the dependencies:

```bash
pip install -r requirements.txt
```

---

## ▶️ Running the Analysis

Execute the main script:

```bash
python predict_trial_outcome.py
```

The script will:
1. Download and load the dataset
2. Generate chemical + text features
3. Train the XGBoost classifier
4. Output evaluation metrics
5. Save visualizations locally

---

## 🔮 Example Predictions

### **Scenario A: Low Risk**
- **Drug:** Ibuprofen  
- **Protocol:** "Healthy volunteers with mild pain. Exclusion: Infection."  
- **Keywords:** 0 Risk / 5 Safe  
- **Success Probability:** **49.01%**

---

### **Scenario B: High Risk**
- **Drug:** Doxorubicin  
- **Protocol:** "Patients with metastatic tumor. Disease must be refractory or relapsed."  
- **Keywords:** 4 Risk / 0 Safe  
- **Success Probability:** **25.45%**

---

## 📊 Evaluation Results
```
--- 4. EVALUATION ---
ROC-AUC Score: 0.6144
F1 Score: 0.7874

Classification Report:
              precision    recall  f1-score   support

     Failure       0.54      0.39      0.30       384
     Success       0.72      0.87      0.79       774

    accuracy                           0.68      1158
   macro avg       0.63      0.59      0.59      1158
weighted avg       0.66      0.68      0.63      1158
```

---

## 📂 Project Structure
```
project/
│
├── predict_trial_outcome.py      # Core model training & inference script
├── requirements.txt              # Python dependencies
├── images/
│   └── feature_importance.png    # Upload generated plot here
├── README.md                     # Documentation
└── data/                         # Auto-downloaded dataset
```

---

## ⚠️ Limitations
- Uses **keyword-based NLP**, which is lightweight but limited.
- Morgan Fingerprints are **general-purpose**; task-specific embeddings may improve results.
- Dataset imbalance still affects minority (failure) predictions.
- Moderate ROC-AUC (~0.61) indicates room for deeper modeling.

---

## 🔭 Future Work
- Upgrade to **BioBERT / ClinicalBERT** embeddings.
- Integrate **molecular transformers** (ChemBERTa, Mol2Vec).
- Add metadata (trial size, sponsor type, geography).
- Train a **multi-modal neural network** combining molecules + text.
- Conduct hyperparameter tuning with **Optuna**.
- Build an interactive **web dashboard** for predictions.

---



