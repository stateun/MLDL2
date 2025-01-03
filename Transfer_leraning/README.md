# MLDL2
Machine Learning &amp; Deep Learning for Data Science 2

## Transfer Learning for CUB-200 Dataset

This project focuses on improving test performance for the **CUB-200 dataset** using transfer learning. The approach excludes ImageNet pre-training and instead leverages CIFAR-10 and CIFAR-100 datasets. Below is a detailed summary of the process, results, and conclusions.

---

## Objective
To enhance the test accuracy of the **CUB-200 dataset**, a 200-class classification problem, by exploring fine-tuning strategies, data augmentation, and ensemble methods. The challenges stem from the smaller number of classes in CIFAR-10 (10 classes) and CIFAR-100 (100 classes), making transfer learning less effective.

---

## Approach

### 1. **Model Architecture**
- **Base Models:**
  - ResNet-18
  - ResNet-34
- **Modifications:**
  - Fully connected layers adapted to 200-class output for CUB-200.

### 2. **Training Details**
- **Loss Function:** CrossEntropyLoss
- **Optimizer:** Adam
- **Scheduler:** MultiStepLR (milestones: `[25, 45]`, gamma: `0.1`)
- **Epochs:** 50, 100

### 3. **Fine-Tuning**
- **Head-Only Fine-Tuning:** Adjusted only the fully connected layers.
  - **Result:** Poor performance (~6–7% validation accuracy).
- **Full Fine-Tuning:** Trained the entire model.
  - **Result:** Slight improvement but suboptimal compared to training solely on CUB-200.

### 4. **Data Augmentation**
- Techniques applied:
  - Random flipping
  - Cropping
  - Normalization
- **Observation:** Combined augmentations were ineffective, and even individual methods showed limited improvement.

### 5. **Ensemble Learning**
- **Method:**
  - Trained 10 models of the same architecture (ResNet-18 and ResNet-34).
  - Selected the best-performing model based on validation accuracy.
  - Combined predictions through averaging.
- **Results:**
  - ResNet-18 Ensemble: Validation accuracy ~36.7%. See the plot below:
    ![ResNet-18 Ensemble](Plot/ResNet-18%20Ensemble.png)
  - ResNet-34 Ensemble: More stable training but no significant accuracy gain. See the plot below:
    ![ResNet-34 Ensemble](Plot/ResNet-34%20Ensemble.png)

---

## Key Observations
1. Fine-tuning the entire model yielded better results than head-only tuning but still fell short of expectations.
2. Data augmentation techniques did not provide significant benefits.
3. The ensemble method (10 models) significantly improved performance, proving to be an effective strategy for enhancing test accuracy.
4. Transfer learning on CUB-200 was less effective due to the larger number of classes (200) compared to CIFAR-10 (10 classes) and CIFAR-100 (100 classes). This highlights the challenge of adapting knowledge from datasets with fewer classes to datasets with significantly more classes.

---

## Challenges
1. **Overfitting:** 
   - Models achieved 100% train accuracy but struggled on validation, indicating overfitting.
2. **Limited Augmentation Effectiveness:** 
   - Augmentations failed to enhance model learning significantly.
3. **Computational Constraints:** 
   - Limited resources restricted experimentation with larger ensembles.

---

## Future Work
1. **Data Augmentation Optimization:**
   - Experiment with more sophisticated augmentation techniques.
2. **Alternative Architectures:**
   - Explore models beyond ResNet for potential performance gains.
3. **Hyperparameter Tuning:**
   - Optimize learning rates, scheduler settings, and augmentation parameters.

---

## Conclusion
This study highlighted the challenges of transfer learning on the CUB-200 dataset without ImageNet pre-training. Ensemble methods (10 models) provided the best performance and proved to be an effective approach for boosting test accuracy. However, the gap in class distribution between CIFAR datasets and CUB-200 limited the effectiveness of transfer learning.

