
Authors:
- Bilal Haroon
- Nathan Butler
- Michael Sheehey
# ⚛️ CERN Collider Event Classifier (Signal vs. Background) DATA 3403 Final Project

## 🎯 Project Goal

To develop a Deep Neural Network (DNN) model capable of classifying rare **Signal** events (class 1) from overwhelming **Background** events (class 0) using high-energy physics data from a particle collider.

## 💾 Data Summary

* **Data Source:** Simulated/Real data from a particle collider experiment (e.g., LHC).

* **Target Variable (Y):** Binary (0 for Background, 1 for Signal).

* **Key Preprocessing:**
  * **Scaling:** All feature data (`X`) was **Standardized** (Zero Mean, Unit Variance) using `StandardScaler` to optimize DNN convergence.

  * **Dataset Split:** Approximately 80% Training, 20% Test/Validation.
  
  * **Missing Value Imputation:** Missing values in the features were handled using mean imputation. For every column that had missing values, a new binary indicator column was created to flag which rows had an imputed value.

## 🧠 Model Architecture (Deep Neural Network)

| Layer | Type | Configuration | Activation |
| :--- | :--- | :--- | :--- |
| **Input** | Dense | `input_dim` (Number of features) | - |
| **Hidden Layers** | Dense (3-4 Layers) | Typical layers of e.g., 64, 32, 16 neurons | ReLU |
| **Output Layer** | Dense (1 Neuron) | Outputs a probability | **Sigmoid** |

The model was compiled with **`loss='binary_crossentropy'`** and trained using an **Adam optimizer** with a **reduced learning rate** to prevent exploding gradients and ensure stable convergence.

## 📈 Performance Summary

The model's performance on the unseen **Test Set** demonstrated strong capability in discriminating Signal from Background.

| Metric | Score | Interpretation |
| :--- | :--- | :--- |
| **Accuracy** | $\approx 84.7\%$ | The model correctly classified the overall event type 84.7% of the time. |
| **AUC (Area Under ROC Curve)** | $\approx 0.926$ | The model has excellent discriminative power (92.6% chance of correctly ranking a Signal event above a Background event). |
| **Signal Purity (Precision)** | $\approx 84.7\%$ | Out of all events predicted as Signal, 84.7% were truly Signal. |
| **Signal Efficiency (Recall)** | $\approx 82.0\%$ | The model successfully identified 82.0% of all true Signal events present in the test set. |

### Confusion Matrix (Test/Validation Set)

| | Predicted Background (0) | Predicted Signal (1) |
| :---: | :---: | :---: |
| **True Background (0)** | 20,824 (TN) | 3,086 (FP) |
| **True Signal (1)** | 3,738 (FN) | 17,067 (TP) |

## ✅ Conclusion

The DNN successfully learned the non-linear relationship required for event classification, achieving a high AUC and a strong balance between Signal Purity and Efficiency, making it a viable tool for selecting Signal candidates in physics analysis.
