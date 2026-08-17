# Observations — Stroke Prediction Benchmark

## 1. Which model performed best on training data?

I observed that the best-performing models on the training set were the deep Decision Tree and Random Forest. Both reached an accuracy of 1.0, a precision of 1.0, recall of 1.0, F1 of 1.0, and ROC-AUC of 1.0. This shows that they fit the training data almost perfectly.

However, this level of performance is also a strong sign of overfitting. In other words, these models memorized the training patterns very well, but that does not necessarily mean they learned a pattern that would generalize well to unseen data.

## 2. Which model performed best on validation data?

On the validation set, the strongest model was Logistic Regression. It had the highest validation ROC-AUC, approximately 0.841, and its validation accuracy remained around 0.951. This made it the most stable model during validation.

Compared with the other models, Logistic Regression showed better balance between class separation and generalization. The other models either overfit the training data or failed to detect the positive stroke class effectively.

## 3. Which model generalized best to the final test set?

I concluded that Logistic Regression generalized best to the final test set. It had the highest test ROC-AUC at approximately 0.843 and maintained an accuracy of around 0.952. This was the most reliable result among the models I tested.

Even so, the final test results still showed a major issue: the recall for the positive class was extremely low. Many models had precision and recall values of 0.0 or near 0.0, which means they were mainly predicting the majority class and were not detecting stroke cases well enough. This is the main limitation of the current benchmark.

## 4. Which algorithm was most interpretable?

The most interpretable algorithm was the Decision Tree. It is easy to explain because the model makes predictions through a sequence of simple rules. A shallow Decision Tree is especially interpretable because it is shorter and easier for a person to follow.

Between the two tree settings, the shallow Decision Tree was more interpretable than the deep one. The deep tree may fit the training data better, but it becomes much harder to explain and understand.

## 5. Which algorithm was fastest at inference time?

The fastest model at inference time was the deep Decision Tree, followed closely by Logistic Regression. In the final output, the deep Decision Tree had the lowest inference time on the test set.

This difference is small, so I would not say that speed was the main deciding factor in this project. Predictive quality and class detection are far more important than small timing differences.

## 6. Which model would you choose if explainability were a requirement?

If explainability were the main requirement, I would choose the Decision Tree. It is the easiest model to explain because its decision process is transparent and can be followed using simple if-then rules.

However, I would only choose it if I accepted its weaker predictive behavior. The shallow tree was easy to explain, but it was also too simple to capture the data patterns well. So the trade-off is clear: better explanation, weaker prediction.

## 7. Which model would you choose if predictive performance were the primary objective?

If predictive performance were the main objective, I would choose Logistic Regression as the best overall option in this benchmark. It showed the strongest and most stable generalization behavior on the validation and test sets, with the highest ROC-AUC values among the models.

At the same time, I would not call it a strong stroke-detection model in a practical sense because the positive-class recall was still very low. This means the model is not yet good enough for a real medical prediction task without deeper tuning and class imbalance handling.

## 8. Did any model show signs of high bias or high variance?

Yes. I observed both patterns clearly.

- High bias: The shallow Decision Tree and the larger KNN models showed signs of underfitting. They were too simple and could not capture enough of the underlying pattern. Their training and validation performance stayed poor.
- High variance: The deep Decision Tree and Random Forest showed clear signs of overfitting. They reached near-perfect training scores, but their validation and test performance dropped sharply.

This contrast is important because it shows that the problem is not simply a matter of using one algorithm. The data is difficult, the class distribution is uneven, and the models are struggling to learn the minority class consistently.

## Final conclusion

I concluded that the benchmark was successful in showing the full model comparison process, but it also showed a very important limitation: the dataset is imbalanced and the positive class is difficult to detect. The models could achieve high accuracy, but that accuracy was misleading because it was driven by the majority class.

If I answer the assignment questions directly, my final view is:

- Best on training data: deep Decision Tree and Random Forest
- Best on validation data: Logistic Regression
- Best generalization to the final test set: Logistic Regression
- Most interpretable: Decision Tree
- Fastest at inference: deep Decision Tree
- Best choice for explainability: Decision Tree
- Best choice for predictive performance: Logistic Regression (with caution)
- Signs of high bias: shallow Decision Tree and large-k KNN
- Signs of high variance: deep Decision Tree and Random Forest

Overall, the main conclusion is that model performance is limited by class imbalance and the structure of the stroke dataset, not only by the choice of classifier. This is the central observation from the benchmark.
