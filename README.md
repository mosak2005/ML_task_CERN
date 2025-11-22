assigned dataset: https://www.openml.org/search?type=data&sort=runs&id=24&status=active
assigned model: QDA (Quadratic Discriminant Analysis)

The goal of this project is to build a machine learning model capable of distinguishing between edible (e) and poisonous (p) mushrooms.
Given the high stakes of the problem (consuming a poisonous mushroom can be fatal), the primary objective was not just overall accuracy, but maximizing Recall (Sensitivity). We aimed to minimize False Negatives (poisonous mushrooms classified as edible) to zero.

The biggest obstacle encountered was selecting the appropriate encoder for categorical data. Initial tests with One-Hot Encoding resulted in multicollinearity issues, causing the QDA covariance matrix to become singular.
Ultimately, I selected the WOEEncoder (Weight of Evidence), which showed the best results. It successfully transformed categorical attributes into continuous values representing the log-odds of toxicity, aligning perfectly 
with QDA's mathematical assumptions.

The 'veil-type' feature was dropped due to zero variance. Subsequently, a StandardScaler was applied to normalize the feature values (mean=0, variance=1), ensuring numerical stability during the covariance matrix estimation.

Final benchmarks my model achieved on test set:

Accuracy:             1.0000
Precision:            1.0000  
Recall:               1.0000  
F1-Score:             1.0000
ROC AUC:              1.0000

Cross-validation also confirmed a stable Recall of 1.0.

While a perfect score of 1.0 often raises concerns about data leakage, extensive analysis confirmed that the dataset contains highly separable features
(such as 'Odor' and 'Spore-Print-Color'). The distinct biological rules governing mushroom toxicity allow for perfect classification when mapped correctly.
Feature importance analysis identified 'Odor', 'Spore-Print-Color', and 'Stalk-Root' as the top predictors. Notably, the presence of missing values ('?') in 
the 'Stalk-Root' category served as a strong statistical indicator of toxicity
