# Geoscience Machine Learning: Lithology Prediction

## 📌 Project Overview

This project applies machine learning techniques to predict lithology (e.g., sand vs. shale) using well log data. Multiple models were developed, evaluated, and compared to determine which approach performs best for subsurface classification.

The workflow includes data preprocessing, feature engineering, statistical analysis, and implementation of both traditional machine learning and deep learning models.

---

## 📂 Dataset

The dataset consists of well log measurements from three wells:

- Well 1  
- Well 4  
- Well 7  

### Input features:
- SP (Spontaneous Potential)
- GR (Gamma Ray)
- LLD (Deep Resistivity)
- LLS (Shallow Resistivity)
- DEN (Density)
- AC (Acoustic)

### Target:
- Lithology (categorical)

---

## ⚙️ Data Preprocessing

- Fixed inconsistent column names (e.g., `litholody → lithology`)
- Removed missing lithology values
- Filled missing feature values using mean imputation
- Standardized feature selection across models
- Used both:
  - ✅ Well-based split (realistic)
  - ✅ Random split (for CNN)

---

## 🤖 Models Implemented

### 1. Random Forest
- Ensemble tree-based model
- Best overall performance
- Accuracy: **~91%**

---

### 2. Decision Tree
- Interpretable rule-based classifier
- Accuracy: **~90%**

Example rule:
if GR > X → shale
if GR ≤ X → sand

---

### 3. Logistic Regression
- Linear classification model with statistical interpretation
- Accuracy: **~88%**

Key findings:
- GR and DEN strongly influence shale prediction
- LLD was not statistically significant

---

### 4. Linear Regression (AC Prediction)
- Predicted acoustic log (AC) using other logs
- R² ≈ **0.54**

#### VIF Analysis:
- LLD and LLS showed high multicollinearity (>13)
- Removing LLS reduced VIF values significantly
- Final clean model used:
  - SP, GR, LLD, DEN

---

### 5. Convolutional Neural Network (CNN)
- Deep learning model applied to tabular data
- Used random train-test split

Accuracy: **~86.7%**

Observations:
- Performs well but slightly below tree-based models
- Less interpretable
- More computationally intensive

---

## 📊 Model Comparison

| Model                  | Performance |
|----------------------|------------|
| Random Forest         | ~91% ✅ (Best) |
| Decision Tree         | ~90% |
| Logistic Regression   | ~88% |
| CNN                   | ~86.7% |
| Linear Regression     | R² ~0.54 |

---

## 🔍 Key Insights

- **Gamma Ray (GR)** is the most important feature for lithology classification
- **Density (DEN)** also plays a major role
- **Resistivity logs (LLD & LLS)** are redundant → multicollinearity
- Tree-based models outperform linear and deep learning models
- CNN improves with random splitting but introduces data leakage

---

## ⚠️ Important Considerations

- Well-based splitting provides realistic model evaluation  
- Random splitting can inflate performance due to data leakage  
- Feature selection improves model stability and interpretability  

---

## ✅ Conclusion

Tree-based models (Random Forest and Decision Tree) provide the best combination of accuracy and interpretability for lithology prediction. Logistic regression offers statistical insights, while CNN demonstrates the ability of deep learning to capture complex relationships, though with limited advantage for tabular data.

---

## 📁 Repository Structure

---

## 🚀 Technologies Used

- Python  
- Pandas, NumPy  
- Scikit-learn  
- Statsmodels  
- TensorFlow / Keras  
- Matplotlib  

---

## 👨‍💻 Author

**Isaiah Daum**  
Machine Learning in Geosciences Project

---

## Disclaimer and Acknowledgement

Artificial intelligence tools were used to assist in structuring, refining, and articulating portions of this project, including explanations, summaries, and code organization. All underlying work, data processing, model implementation, and analysis were conducted by the author, and the use of AI served only as a support tool to enhance clarity and presentation.
This project was completed as part of Dr. Bo Zhang’s “Machine Learning in Geosciences” course at The University of Alabama during the Fall 2021 semester. The concepts, methodologies, and techniques applied in this work were learned through course instruction and associated materials.