# MLDL2
Machine Learning &amp; Deep Learning for Data Science 2

## Knowledge Distillation on CIFAR-100

This project implements Knowledge Distillation using the CIFAR-100 dataset, where a pretrained teacher model is used to guide the training of a smaller student model. Below is a summary of the process and results.

### Teacher Model
- **Architecture:** Pretrained ResNet-18
- **Dataset:** CIFAR-100
- **Purpose:** Provides softened outputs (logits) to train the student model effectively.
- **Pretrained Weights:** Loaded from a checkpoint (`pretrained_teacher.pth`).

### Student Model
- **Architecture:** A smaller variant of ResNet-18 with reduced layers.
- **Modifications:**
  - Removed the last block (`layer4`) for a more compact model.
  - Adjusted the fully connected layer for CIFAR-100 classification (100 classes).

### Training Process
1. **Dataset Preparation:**
   - Applied standard transformations including normalization, random cropping, and flipping.
2. **Loss Function:**
   - Used a custom distillation loss combining CrossEntropyLoss and KLDivergence.
   - Parameters:
     - Temperature (`T`): 4
     - Alpha: 0.5
3. **Optimizer:**
   - Stochastic Gradient Descent (SGD) with momentum (0.9) and weight decay (1e-4).
   - Learning rate: 0.1
4. **Training:**
   - Balanced supervised and distillation losses using the predefined `alpha` and `T`.
   - Dynamic learning rate adjustment was applied based on epochs.

### Results
- **Best Student Model:**
  - Validation Accuracy: 59.80%
  - Achieved using ensemble methods with ResNet-14.
- **Challenges:**
  - Overfitting was mitigated through label smoothing and regularization techniques.
  - CUDA out-of-memory errors limited ensemble size for ResNet-18.

### Key Takeaways
1. Knowledge distillation improved student model accuracy significantly compared to independent training.
2. Ensemble methods further enhanced performance but were computationally intensive.
3. The study identified potential for exploring feature-based distillation and optimizing loss weightings for future work.

### Future Work
- **Feature-based Knowledge Distillation:** Evaluate the effectiveness compared to response-based methods.
- **Loss Optimization:** Experiment with different lambda values to balance losses.
- **Efficient Ensembles:** Investigate ways to maintain performance while reducing computational overhead.

### Conclusion
The project demonstrates the effectiveness of Knowledge Distillation on CIFAR-100, leveraging teacher-student architectures and ensemble methods for enhanced performance. The findings provide a foundation for future research into more efficient and scalable distillation techniques.
