# Diabetic-Retinopathy-Classification
**Analyzing the Effect of Lightweight Attention Modules on Fundus Images**

This project evaluates **ResNet-18** and its attention-enhanced variants for **binary diabetic retinopathy classification (DR vs No_DR)** using the *Diagnosis of Diabetic Retinopathy* dataset from Kaggle:  https://www.kaggle.com/datasets/pkdarabi/diagnosis-of-diabetic-retinopathy.

---

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

### Data Augmentation

To improve generalization and reduce overfitting, several data augmentation techniques were applied during training.
All training images were resized to 256×256 and randomly cropped to 224×224. Random horizontal flipping was used to increase invariance to left–right orientation. A RandomAffine transformation was applied with rotation up to ±15°, translation up to 5%, and scaling between 0.9 and 1.1. ColorJitter was also used to simulate real-world illumination variations by adjusting brightness, contrast, saturation, and hue. Finally, RandomErasing (p = 0.25) was applied to improve robustness against occlusion and missing retinal features.
For validation and testing, only deterministic preprocessing was used: resizing to 256×256 followed by center cropping to 224×224, tensor conversion, and normalization.

---

### Model

In this project, three lightweight attention mechanisms were integrated into the ResNet-18 backbone to enhance feature representation while keeping the model computationally efficient. The attention modules used are Squeeze-and-Excitation (SE), Convolutional Block Attention Module (CBAM), and Efficient Channel Attention (ECA). These modules help the network focus on the most informative retinal features by refining channel-wise and/or spatial feature responses. All attention-based models were evaluated and compared against the baseline ResNet-18 using the same training and testing protocol.

- **ResNet-18:**  https://arxiv.org/pdf/1512.03385
- **SE:**         https://arxiv.org/abs/1709.01507
- **CBAM:**       https://openaccess.thecvf.com/content_ECCV_2018/papers/Sanghyun_Woo_Convolutional_Block_Attention_ECCV_2018_paper.pdf
- **ECA:**        https://arxiv.org/abs/1910.03151

---
### Training Setup

All models were trained using a custom PyTorch training loop with validation after every epoch. The best model checkpoint is saved automatically based on the highest validation accuracy.

- **Loss:** CrossEntropyLoss(label_smoothing=0.1)
- **Optimizer:** AdamW(lr=1e-4, weight_decay=0.01)
- **Scheduler:** CosineAnnealingLR(T_max=num_epochs, eta_min=1e-6)
- **Best model saved by:** Validation Accuracy

---

### Performance Comparison

| Model | Accuracy | Precision | Recall | Specificity | F1-score | AUC |
|------|----------|----------|--------|-------------|----------|-----|
| ResNet-18 | 0.9654 | 0.9508 | 0.9831 | 0.9469 | 0.9667 | **0.9900** |
| ResNet-18 + SE | 0.9697 | 0.9587 | 0.9831 | 0.9558 | 0.9707 | 0.9859 |
| ResNet-18 + CBAM | 0.9697 | **0.9664** | 0.9746 | 0.9646 | 0.9705 | 0.9891 |
| **ResNet-18 + ECA** | **0.9784** | 0.9748 | **0.9831** | **0.9735** | **0.9789** | 0.9774 |

---

### Discussion

- The **baseline ResNet-18** already achieved strong performance (**96.54% accuracy**, **AUC = 0.99**), indicating the model learns discriminative DR features effectively.
- Adding attention modules consistently improved performance by reducing misclassification errors.
- **SE and CBAM** produced similar improvements in accuracy (**96.97%**), while CBAM provided slightly better specificity.
- **ECA achieved the best overall performance**, improving accuracy to **97.84%**, with the highest specificity (**97.35%**) and F1-score (**97.89%**).

---

### Best Model

**ResNet-18 + ECA** is selected as the best-performing model due to:
- Highest accuracy (**97.84%**)  
- Highest F1-score (**97.89%**)  
- Best specificity (**97.35%**)  
- Lowest total errors (**5 misclassifications out of 231 samples**)  

