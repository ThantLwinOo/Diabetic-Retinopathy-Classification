# Diabetic-Retinopathy-Classification
Analyzing the Effect of Lightweight Attention Modules on Fundus Images

This project evaluates **ResNet-18** and its attention-enhanced variants for **binary diabetic retinopathy classification (DR vs No_DR)** using the *Diagnosis of Diabetic Retinopathy* dataset from Kaggle:  https://www.kaggle.com/datasets/pkdarabi/diagnosis-of-diabetic-retinopathy

Dataset is originally splited into three parts.

**Train set Distribution**
- **Dr:** 1050
- **No_DR:** 1026

**Validaition set Distribution**
- **DR:** 245
- **NO_DR:** 286
  
**Test set distribution**
- **DR:** 113 samples  
- **No_DR:** 118 samples  

---

### Performance Comparison

| Model | Accuracy | Precision | Recall | Specificity | F1-score | AUC |
|------|----------|----------|--------|-------------|----------|-----|
| ResNet-18 | 0.9654 | 0.9508 | 0.9831 | 0.9469 | 0.9667 | **0.9900** |
| ResNet-18 + SE | 0.9697 | 0.9587 | 0.9831 | 0.9558 | 0.9707 | 0.9859 |
| ResNet-18 + CBAM | 0.9697 | **0.9664** | 0.9746 | 0.9646 | 0.9705 | 0.9891 |
| **ResNet-18 + ECA** | **0.9784** | 0.9748 | **0.9831** | **0.9735** | **0.9789** | 0.9774 |

---
