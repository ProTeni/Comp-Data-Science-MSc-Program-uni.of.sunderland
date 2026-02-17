# Feed-Forward Neural Network for Bank Marketing Prediction

## 🎯 Project Overview

This project implements a binary classifier using a feed-forward artificial neural network (ANN) built with Keras/TensorFlow to predict whether bank customers will subscribe to a term deposit. The project demonstrates systematic hyperparameter exploration and evaluation of different neural network architectures for a real-world business problem.

**Dataset:** [Bank Marketing Dataset](https://archive.ics.uci.edu/dataset/222/bank+marketing) from UCI Machine Learning Repository

**Problem Type:** Binary Classification (Supervised Learning)

**Key Focus:** Exploring the impact of network depth (layers) and width (neurons) on model performance while keeping other hyperparameters constant.

---

## 📊 Dataset Details

- **Size:** 7,842 rows × 10 features (after preprocessing)
- **Target Variable:** Binary (0 = No subscription, 1 = Subscription)
- **Class Distribution:** Imbalanced dataset (requiring stratified splitting)
- **Features:** Customer demographics, contact information, campaign details

**Preprocessing Steps:**
1. **Feature Removal:**
   - `duration`: Removed to avoid data leakage (only known post-contact)
   - `contact`: Binary feature (cellular/telephone) with no predictive power
   - `marital` & `education`: Weak predictive indicators for financial decisions
   
2. **Feature Engineering:**
   - Applied **RobustScaler** (chosen after outlier analysis)
   - Encoded binary features (yes/no → 1/0)
   - No null values detected

3. **Data Splitting:**
   - Training: 80% (6,273 samples)
   - Validation: 10% (784 samples)  
   - Test: 10% (784 samples)
   - **Stratified splitting** to maintain class distribution

---

## 🧠 Model Architecture & Methodology

### Experimental Design

**Constant Hyperparameters:**
- Activation Function: **ReLU** (all hidden layers)
- Output Activation: **Sigmoid** (binary classification)
- Optimizer: **SGD** (Stochastic Gradient Descent)
- Learning Rate: Fixed
- Epochs: **100**
- Loss Function: Binary Crossentropy

**Variable Hyperparameters:**
- Number of layers (depth)
- Number of neurons per layer (width)

### Architecture Philosophy

Based on dataset scale heuristics:
- **Small dataset (<1,000):** Neurons [32, 16, 8]
- **Medium dataset (1,000-10,000):** Neurons [64, 32, 16] ← **This dataset**
- **Large dataset (10,000-100,000):** Neurons [128, 64, 32, 16]
- **Very Large dataset (>100,000):** Neurons [256, 128, 64, 32]

### 16 Architectures Tested:

**1. Baseline Models (Single Hidden Layer):**
- Baseline 128: [128] neurons
- Baseline 64: [64] neurons
- Baseline 32: [32] neurons
- Baseline 16: [16] neurons

**2. Pyramid Architectures (Decreasing Width):**
- Pyramid [64, 32]
- Pyramid [64, 16]
- Pyramid [32, 16]
- Pyramid [64, 32, 16]

**3. Constant Width Architectures:**
- Constant [64, 64]
- Constant [64, 64, 64]
- Constant [32, 32]
- Constant [32, 32, 32]
- Constant [16, 16]
- Constant [16, 16, 16]

**4. Experimental Architectures:**
- Hourglass (decoder-encoder style)
- Diamond (expanding then contracting)

---

## 📈 Model Performance Results

### Evaluation Metrics

**Primary Metrics:**
- **Balanced Accuracy:** Accounts for class imbalance
- **Recall (Sensitivity):** Critical for business context—minimizing False Negatives (missed customers)
- **Precision, F1-Score:** Secondary metrics

**Business Rationale for Recall:**
In banking, missing a customer who would subscribe (False Negative) is more costly than making an unnecessary call (False Positive). Therefore, **Recall is prioritized** over Precision.

### Top 3 Models by Balanced Accuracy:

| Rank | Architecture | Balanced Accuracy | Recall | Notes |
|------|-------------|-------------------|--------|-------|
| 🥇 | **Pyramid [64,16]** | **74.08%** | 48.04% | Best overall balance |
| 🥈 | Pyramid [64,32] | 73.57% | 53.63% | Strong recall performance |
| 🥉 | Pyramid [64,32,16] | 72.78% | 52.51% | Deeper but slightly lower |

### Top 3 Models by Recall:

| Rank | Architecture | Recall | Balanced Accuracy | Notes |
|------|-------------|--------|-------------------|-------|
| 🥇 | **Constant [64,64,64]** | **65.42%** | 66.88% | Highest recall |
| 🥈 | Pyramid [64,32] | 53.63% | 73.57% | Better balance |
| 🥉 | Pyramid [64,32,16] | 52.51% | 72.78% | Strong all-around |

### Sample Confusion Matrix (Pyramid [64,16]):
```
                 Predicted
                 No    Yes
Actual  No      570    35
        Yes      93    86
```
- **True Positives (TP):** 86
- **False Positives (FP):** 35  
- **True Negatives (TN):** 570
- **False Negatives (FN):** 93

---

## 💡 Key Insights & Findings

### 1. **Architecture Depth vs. Width Trade-off**
- **Shallower, wider networks** (like [64,16]) achieved better balanced accuracy
- **Deeper, constant-width networks** (like [64,64,64]) maximized recall but sacrificed overall balance
- **Lesson:** More layers ≠ better performance for small-medium datasets

### 2. **Pyramid Architectures Excel**
- Gradually decreasing neuron counts ([64→32→16]) consistently outperformed constant-width architectures
- Aligns with the principle of hierarchical feature learning (high-level → abstract)

### 3. **Business Context Matters**
- If the goal is **maximizing customer capture** → Choose [64,64,64] (65.42% recall)
- If the goal is **balanced performance** → Choose [64,16] (74.08% balanced accuracy)
- **There is no universal "best" model**—it depends on business priorities

### 4. **Computational Efficiency**
- All models trained in reasonable time (<5 minutes per architecture on CPU)
- Demonstrates that ANNs are practical for small-medium tabular datasets

### 5. **Data Quality Over Model Complexity**
- Feature engineering (dropping leaky/weak features) was as important as architecture
- Using **RobustScaler** for outlier-heavy data improved convergence

---

## 🛠️ Technical Stack

- **Language:** Python 3.10+
- **Deep Learning:** TensorFlow 2.x, Keras
- **Data Processing:** Pandas, NumPy
- **Preprocessing:** Scikit-learn (RobustScaler, train_test_split)
- **Evaluation:** Scikit-learn metrics (accuracy_score, recall_score, confusion_matrix, balanced_accuracy_score)
- **Visualization:** Matplotlib, Seaborn

---

## 📁 Repository Structure

```
FeedFowradNeural network on a Bank project/
├── code.ipynb                 # Main Jupyter notebook with full analysis
├── Bank.csv                   # Dataset
├── Read_Me.md                 # This file
├── LinkedIn_Post.md           # Professional summary for sharing
└── Images/                    # Visualizations and plots
```

---

## 🚀 How to Run

### Prerequisites:
```bash
pip install tensorflow pandas numpy scikit-learn matplotlib seaborn
```

### Steps:
1. Clone this repository
2. Ensure `Bank.csv` is in the project directory
3. Open `code.ipynb` in Jupyter Notebook/Lab
4. Run cells sequentially from top to bottom
5. Observe model training, evaluation, and comparison

**Note:** Training 16 models with 100 epochs each will take approximately 30-60 minutes on a standard CPU.

---

## 🔮 Future Work & Improvements

1. **Hyperparameter Tuning:**
   - Grid search or random search for learning rate, batch size, optimizer
   - Experiment with Adam, RMSprop optimizers

2. **Regularization:**
   - Add Dropout layers to prevent overfitting
   - Apply L1/L2 regularization

3. **Data Augmentation:**
   - SMOTE for handling class imbalance
   - Feature interaction terms

4. **Advanced Architectures:**
   - Residual connections (ResNet-style)
   - Batch normalization layers

5. **Model Deployment:**
   - Save best model and create inference API
   - A/B testing in production environment

---

## 📖 References

- Aurelien Geron - *Hands-On Machine Learning with Scikit-Learn, Keras & TensorFlow* (Chapter 10: Fine-tuning Neural Network Hyperparameters)
- UCI Machine Learning Repository - Bank Marketing Dataset

---

## 👨‍🎓 Author

This project was completed as part of my Master's program coursework, demonstrating practical application of neural networks to real-world business problems.

**Connect with me:** [Your LinkedIn/GitHub]

---

## 📄 License

This project is for educational purposes. Dataset source: [UCI Machine Learning Repository](https://archive.ics.uci.edu/)

---

**⭐ If you found this project helpful, please star it and share!**
