# Observations — Stroke Prediction Benchmark

## What I observed

I ran the benchmark on the stroke dataset and compared the outputs across the models. The most important observation is that accuracy looks high for most models, but it is not a reliable indicator in this problem because the dataset is imbalanced. A model can achieve around 95% accuracy while still failing to identify the actual stroke cases. That means the benchmark must be judged mainly by recall, precision, and class-level behavior, not only by overall accuracy.

The strongest evidence from the results is that the positive class was very weakly detected. In the test results, many models had precision of 0.0, recall of 0.0, or F1 close to 0.0. This shows that the models were mostly predicting the majority class and not learning the stroke pattern effectively.

## Basic findings from the results

I observed the following points from the actual test results:

- Logistic Regression reached an accuracy of 0.952, but its recall was only 0.02 and F1 was 0.039. Its precision was 1.0, which means it was very conservative and only predicted the positive class in a very small number of cases.
- Gradient Boosting reached 0.950 accuracy, but recall stayed at 0.02 and F1 at 0.038. This indicates that the model ranked the classes somewhat well, but the decision threshold still caused poor positive detection.
- KNN models delivered accuracy around 0.946–0.951, but their recall and F1 were 0.0 in test performance. This suggests poor separation of the minority class.
- Random Forest and XGBoost also remained weak on the stroke class, with accuracy near 0.945 but precision and recall close to 0.0.
- The deep Decision Tree had a test accuracy of 0.907, but its precision, recall, and F1 were still low. This is a sign of overfitting and weak generalization for the minority class.

## Strong reasoning behind these results

The main reason is class imbalance. The positive class is much smaller than the negative class, so a model can gain high accuracy simply by predicting the non-stroke class most of the time. In this dataset, that problem is serious because the score is not only looking at a global accuracy value, but at whether the model can actually catch the patients with stroke.

The second reason is the default decision threshold. Most models were evaluated using a 0.5 cutoff. If the predicted probabilities for stroke cases are low, the model will not classify them as positive even when its ranking ability is not terrible. This is why ROC-AUC can look moderately acceptable while recall remains poor.

The third reason is overfitting. The deep Decision Tree showed high training performance and then weaker validation/test performance. This tells me the model learned the training data too specifically and could not generalize well. The same pattern is visible in other tree-based models, where the training patterns look stronger than the actual test behavior.

## Model-specific observations

### Logistic Regression
I found Logistic Regression to be the most stable baseline. Its ROC-AUC was around 0.843, which is stronger than several other models. However, the recall remained too low for real use. This tells me that the model has some ability to separate classes overall, but it still needs threshold tuning or class balancing to make it useful for stroke detection.

### KNN
KNN did not perform well for the positive class. With both k=5 and k=25, the recall stayed at 0.0 on the test set. This suggests that the distance-based method was dominated by the majority class and could not identify stroke cases reliably in this setting.

### Tree-based models
The deep Decision Tree and Random Forest showed the clearest signs of overfitting. Their training results were stronger than their test results, which tells me that they were memorizing patterns rather than learning a robust decision boundary. The shallow Decision Tree also underfit, which is a useful contrast: it was too simple to capture the pattern properly.

### Gradient Boosting and XGBoost
These models had better probability ranking than some of the simpler alternatives, but they still did not convert that into useful positive detection at the default threshold. This suggests that the class imbalance remains the central challenge, and more targeted handling is needed before these models can become truly useful.

## What I would conclude

From the results, I conclude that the benchmark worked as intended, but the dataset structure makes the task difficult. The models are not completely failing because they are badly built; they are failing because the positive class is too small and the evaluation is too dependent on accuracy. For this type of medical classification task, the important question is not whether the overall accuracy is high, but whether the model can detect the actual stroke patients.

If this project were improved further, I would focus on class weighting, threshold tuning, and stronger handling of imbalance before making final conclusions about model quality. Without that, many models will look good in summary but still fail in the most important part of the task.

## Final takeaway

My main conclusion is that the project is successful in showing the benchmark process, but the real challenge is not just model selection. The main issue is imbalance and decision thresholding. The results show that the dataset is harder than it appears from accuracy alone, and the benchmark demonstrates that the chosen models do not reliably detect the stroke-positive class under the current setup.
