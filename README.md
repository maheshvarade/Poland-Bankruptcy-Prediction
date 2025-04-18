# Poland-Bankruptcy-Prediction
🏦 Poland Bankruptcy Prediction (2009)
This project aims to predict whether a Polish company went bankrupt in 2009 based on its financial data. The dataset contains several features derived from companies' balance sheets, and the goal is to build models that can identify bankruptcy effectively — despite the challenge of high class imbalance.

📁 Dataset Overview
Source: poland-bankruptcy-data-2009.json

Objective: Predict bankruptcy (bool classification: 0 = False, 1 = True)

Imbalance: Approx. 90% non-bankrupt vs. 10% bankrupt

Missing Data:

Missing values in many features

One feature (feat_37) has 4478 missing values → removed due to excessive missingness

Other missing values handled using median imputation (could also use SimpleImputer)

🧪 Data Preprocessing
Removed feat_37 due to excessive missing values

Replaced all other missing values with the median of the respective feature


Target column (bankrupt) has no missing values

📉 Dealing with Imbalanced Data
Due to the high class imbalance, we applied various resampling techniques:

Regular Training Data (no resampling)

Random Under-Sampling

Random Over-Sampling

SMOTE (Synthetic Minority Over-sampling Technique)

🔍 Dimensionality Reduction
Correlation analysis was not effective due to the structure of the data

Instead, we used Principal Component Analysis (PCA) to visualize and understand feature relationships

🌳 Models Used
Decision Tree Classifier

Random Forest Classifier (performed better than Decision Tree)

Each model was trained using all four versions of the training data (original, under-sampled, over-sampled, and SMOTE-enhanced).

⚙️ Evaluation Approach
For each model and resampling strategy:

python
Copy
Edit

High accuracy does not imply a good model in imbalanced datasets.

📊 Confusion Matrix Insights
The models perform very well on the majority class (0)

They struggle significantly to identify the minority class (1)

Very low recall and precision for class 1, despite high overall accuracy

✅ Best Result: Random Forest
Took longer to train, but yielded better balance in results

ROC Curve shows improvement

AUC = 0.86:

0.5 = Random guessing

1.0 = Perfect classification

0.86 = Excellent discriminatory power

📈 ROC Curve Interpretation
The top-left point on the ROC curve:

TPR ≈ 1: Almost all positives correctly identified

FPR ≈ 0: Very few false positives

This point represents optimal model performance

Our ROC curve hugs the top-left, showing the model learns well

🔚 Conclusion
Handling imbalanced data is crucial for accurate minority class predictions

Random Forest with SMOTE or Class Weights provided the best performance

Evaluating with precision, recall, F1-score, and AUC is more meaningful than accuracy in this scenario

💡 Future Improvements
Try ensemble methods like BalancedBaggingClassifier or EasyEnsembleClassifier

Optimize threshold tuning for better recall on class 1

Experiment with LightGBM or XGBoost with scale_pos_weight

