Of course. Here is a draft README that captures the academic rigor and depth of your Master's project.

---

# **CIFAR-10 Image Classification: A Comparative Analysis of Machine Learning Paradigms**

## 📘 Project Overview

This repository contains the final project for the **CETM26: Machine Learning and Principles** module, a core component of my Master's degree. This project was not merely an implementation exercise but a deep, principled investigation into the performance, efficiency, and practical trade-offs of different machine learning families when applied to the classic CIFAR-10 image classification challenge.

The study systematically traces the evolution of ML approaches, from traditional algorithms to modern deep learning, providing a clear, empirical answer to a critical question: **When computational resources are constrained, which model architecture offers the best balance of accuracy and efficiency for image classification?**

## 🎯 Key Objectives & Philosophical Approach

The project was guided by a core principle: **understanding the "why" behind model performance is as important as the final accuracy score.** To this end, the investigation was structured to:

*   **Benchmark Traditional Models:** Establish strong baselines using Support Vector Machines (SVM) and k-Nearest Neighbours (KNN), evaluating them with and without Principal Component Analysis (PCA) for dimensionality reduction.
*   **Evaluate Neural Network Evolution:** Compare a basic Feed-Forward Neural Network (FFNN) against a Convolutional Neural Network (CNN) to isolate and quantify the performance gain provided by convolutional inductive biases.
*   **Analyze Computational Trade-offs:** rigorously document and analyze Training Time and Inference Time for every model, treating computational cost as a first-class metric alongside accuracy.
*   **Explore Advanced Optimization:** Design a hyperparameter tuning strategy using Keras Tuner to push the performance of an optimized CNN, confronting the real-world challenges of computational limits.
*   **Synthesize with Ensembling:** Develop a soft-voting ensemble that combines predictions from all top-performing models to investigate potential synergistic effects.

## 🧠 What This Project Taught Me (The Master's-Level Depth)

This module drilled me thoroughly, pushing beyond simple implementation to foster a deep, intuitive understanding of machine learning principles:

*   **The Inductive Bias Revolution:** I moved from theoretically understanding to *empirically proving* why CNNs dominate vision tasks. The `CNN_Baseline`'s 70.4% accuracy, achieved 1000x faster than a comparable SVM, was a revelation in how built-in assumptions about data structure (translation invariance, spatial hierarchies) lead to unparalleled efficiency and performance.
*   **The Pragmatics of the Feature Space:** I explored how algorithms interact with data representation. PCA was a double-edged sword: a vital tool for making SVM feasible (94% faster training) but a detriment to KNN, where it induced overfitting by creating a "memorizable" but non-generalizable feature space.
*   **Confronting the Hardware Reality:** The project was a brutal lesson in the practical constraints of machine learning. The failed `Optimized_CNN` hyperparameter search after 48+ hours of compute time was not a failure but a critical data point, teaching me to design experiments with resource boundaries in mind and to value model efficiency as much as accuracy.
*   **From Code to Critical Analysis:** I learned to frame computational limitations not as weaknesses but as key findings for discussion and future work, a essential skill for any practicing data scientist or ML engineer.

## 🏗️ Methodology & Experimental Design

The experimental design was built for a fair, comparative analysis:

1.  **Dataset:** CIFAR-10 (60,000 32x32 colour images in 10 classes).
2.  **Data Splitting:** 80% Training, 10% Validation, 10% Test.
3.  **Model Families:**
    *   **Traditional ML:** RBF-SVM and KNN, with and without PCA.
    *   **Deep Learning:** A custom FFNN, an AlexNet-inspired `CNN_Baseline`, and a hyperparameter-optimized CNN (via Keras Tuner).
    *   **Ensemble:** A soft-voting ensemble combining all successful models.
4.  **Evaluation Metrics:** Primary focus on **Validation Accuracy**, **Training Time**, and **Inference Time**.

## 📊 Key Findings & Results

The results painted a clear, hierarchical picture:

| Model | Validation Accuracy | Training Time | Inference Time | Key Takeaway |
| :--- | :--- | :--- | :--- | :--- |
| **CNN_Baseline** | **70.35%** | **2.45s** | **0.68s** | **The undisputed winner: optimal balance of high accuracy and high efficiency.** |
| SVM_PCA | 52.53% | 142.29s | 34.84s | The best traditional model; PCA made it computationally feasible. |
| SVM_Baseline | 52.57% | 2510.66s | 724.58s | Prohibitively slow, despite decent accuracy. |
| KNN_PCA | 39.47% | 1.27s | 0.32s | Fast to train but suffers from poor generalization. |
| FFNN_Baseline | 38.55% | 1.81s | 0.52s | Proof that neural networks without spatial biases struggle with image data. |

**The Final Hierarchy:** `CNN_Baseline` > `SVM_PCA` > `SVM_Baseline` > `KNN_PCA` > `FFNN_Baseline`

## 📁 Repository Structure

```
├── CIFAR10_ML_Comparison.ipynb  # Main Jupyter Notebook with full analysis
├── Read_Me.md                   
├── /Essay on CIFAR-10 Image Recognition Project
├── requirement.txt
└── /cnn tuning/                    Saved results and figures
```

## How to Run the Code

1.  **Prerequisites:** Ensure you have Python and Jupyter installed, along with the standard data science stack: `numpy`, `pandas`, `matplotlib`, `scikit-learn`, `tensorflow/keras`.
2.  **Open the Notebook:** Launch Jupyter Lab or Notebook and open `CIFAR10_ML_Comparison.ipynb`.
3.  **Run Sequentially:** Execute the cells from top to bottom. The notebook is structured to load data, preprocess, train models, and evaluate them in sequence.
4.  **Note on Hardware:** The `Optimized_CNN` tuning cell is computationally intensive and was designed for a GPU. It is commented out by default, with its results and implications discussed in the final report.

## 🔮 Future Work

Based on the findings and limitations encountered, logical next steps include:
*   Completing the `Optimized_CNN` hyperparameter search on a cloud GPU instance.
*   Implementing a more sophisticated ensemble, potentially using stacking with the `CNN_Baseline` features as meta-features.
*   Exploring transfer learning from large, pre-trained models (e.g., ResNet, EfficientNet) to achieve state-of-the-art performance with less training time.

## 👨‍🎓 Author

This project was completed as part of the Master's program at the University of Sunderland. It represents a significant journey in understanding not just how to build machine learning models, but how to think critically about their design, their trade-offs, and their place in solving real-world problems.