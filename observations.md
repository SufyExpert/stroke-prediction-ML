# Observations — Stroke Prediction Benchmark

## What I observed

I ran the benchmark with the stroke dataset and compared the model outputs directly. The most important thing I noticed is that the overall accuracy looks strong for almost every model, but that is misleading because the dataset is imbalanced. Many models are predicting the majority class most of the time and therefore look good on accuracy without actually detecting the stroke cases properly.

The precision and recall for the positive class were very weak in most runs. In a lot of models, the recall for the stroke class was effectively zero, which means the model was not identifying the actual positive cases in a useful way. This is the main issue I would focus on if I were improving the project further.

## My basic findings

- **Accuracy is not the right metric alone.** The dataset is imbalanced, so a model can look good on accuracy while missing the stroke cases almost entirely.
- **Positive-class recall is the real weakness.** The models are not capturing real stroke cases well enough at the default threshold.
- **Tree-based models overfit.** The deep decision tree and random forest perform nearly perfectly on training data but lose a lot of performance on validation and test data.
- **Logistic Regression is the most stable baseline.** It had a relatively better ROC-AUC than several other models and gave a cleaner behaviour compared with the more complex classifiers.

## Strong reasons behind this

The reason this happens is not random. The dataset has a clear class imbalance, and many models are trained with the default threshold of 0.5. If the model is conservative and rarely predicts the positive class, its accuracy can still be high because the negative class dominates the dataset. This is why I looked beyond raw accuracy and paid attention to recall, precision, F1, and ROC-AUC.

The deep tree and random forest also show clear overfitting. They memorize the training data almost perfectly, but their validation and test results are noticeably worse. This is a classic sign that the model has too much variance for the data size and class structure in this problem.

Another important point is that the positive class is relatively uncommon, so small changes in threshold or class handling can have a big impact on the final observations. If I were improving this further, my first step would be to use class weights or threshold tuning instead of relying only on default prediction probabilities.

## Which models stood out for me

- **Logistic Regression** looked like the most reasonable baseline and had the strongest overall behavior among the simpler models.
- **Gradient Boosting** and **XGBoost** had stronger ranking ability in the probability space, but they still had difficulty when the decision threshold was kept at the default value.
- **KNN** did not perform well for the positive class and was not robust enough for this dataset.
- **SVM** was not particularly effective under the default setup and was sensitive to the scaling decisions.
- **The deep tree** was the clearest example of overfitting in this experiment.

## What I would do next

If I were continuing this project, I would do the following in order:

1. Use class weighting or a higher positive-class penalty to make the models care more about missing stroke cases.
2. Tune the decision threshold instead of leaving it at 0.5.
3. Compare precision-recall curve results instead of relying only on accuracy.
4. Regularize tree-based models more aggressively to reduce overfitting.
5. Re-run the benchmark with these changes and report recall and precision for the minority class as the main decision metrics.

This is the part I would focus on because in a real medical classification task, catching real stroke patients matters more than showing a high overall accuracy based mostly on the majority class.

## Final takeaway

My overall conclusion from the run is that the benchmark is working as intended, but the main problem is not model choice alone — it is the class imbalance and the default classification threshold. The models are not failing because they are badly coded; they are failing because the positive class is too small and the evaluation needs to reflect that specific problem more directly.

For this assignment, I would treat the class imbalance issue as the main takeaway and the biggest improvement area, rather than focusing only on whether accuracy is high.
