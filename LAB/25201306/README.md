Wine Quality Prediction Analysis

1. Easy: Linear Regression

Goal: Predict wine quality score (numeric).
Model: Linear Regression.
Metric: RMSE = 0.6165.
Reasoning:
 We treated quality as a continuous variable. Linear Regression was chosen as a baseline to establish the linear relationship between chemical features (like alcohol) and quality. An RMSE of 0.62 indicates the model's predictions are, on average, within 0.62 points of the true score. Furthermore, the model's coefficients provide direct interpretability, allowing us to quantify exactly how much a one-unit increase in a feature like 'volatile acidity' negatively impacts the wine's rating. However, this baseline approach assumes a strict linear dependency, potentially missing complex non-linear chemical interactions that could better explain the variance in quality scores.


2. Moderate: Logistic Regression

Goal: Classify wines as Good (Quality >= 6) or Bad.
Model: Logistic Regression.
Metric: F1 Score = 0.7905.
Reasoning:
 The problem was converted to binary classification. Logistic Regression is the standard baseline for probability-based classification. We optimized for the F1 Score (0.79) rather than accuracy because it balances Precision and Recall, which is crucial when identifying "Good" wines correctly without missing too many. Additionally, the logistic model outputs probability scores rather than just hard classifications, enabling us to adjust the decision threshold (e.g., requiring >70% confidence) if we want to be stricter about what we label as 'Good'. However, since Logistic Regression relies on a linear decision boundary, it may struggle to perfectly separate the classes if the high-quality wines are intertwined with lower-quality ones in a complex, non-linear pattern.


3. Hard: SVM + Feature Engineering
Goal: Improve classification using interaction features and SVM.
Model: Support Vector Machine (Linear Kernel).
Metric: ROC-AUC = 0.8336.
Reasoning:
 1. Feature Engineering: We created interaction features (e.g., `Alcohol * Sulphates`) to capture combined chemical effects that single features miss.
 2. Scaling: Data was standardized (StandardScaler) because SVMs are sensitive to feature magnitude.
 3. Result: The SVM achieved a higher ROC-AUC (0.8336) compared to Logistic Regression (0.8208), proving that the engineered features and the SVM's margin-maximization capability provided a better separation between Good and Bad wines.

 By manually creating interaction terms, we effectively expanded the feature space, allowing the Linear SVM to establish a decision boundary that accounts for the synergistic effects of chemical components (e.g., high alcohol balancing out acidity). Additionally, unlike Logistic Regression which calculates probabilities based on all data points, the SVM constructs its boundary based primarily on the 'support vectors'—the most ambiguous and difficult-to-classify examples—making the model more robust in defining the separation between similar wine qualities.