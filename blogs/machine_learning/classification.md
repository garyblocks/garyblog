# Classification
## Metrics
### Precision
* Definition: TP / (TP + FP)
* Use case: What proportion of positive identifications was actually correct?
* notes:
	* the amount of positive predictions that are real
	* precision and recall are related, increase one may decrease the other

### Recall
* Definition: TP / (TP + FN)
* Use case: What proportion of actual positives was identified correctly?
* notes:
	* the amount of positives that the model can capture.
	* also called sensitivity or TPR(True positive Rate).

### AUC
* Definition: Area Under the Curve, the area under the ROC(Receiver Operating Characteristics) curve
* Use case: What proportion of actual positives was identified correctly?
* notes:
	* also written as AUROC.


### Specificity
* Definition: TN / (TN + FP)
* Use case: What proportion of actual negative was identified correctly?
* notes:
	* it’s the recall for negatives.
	* always used together with sensitivity(recall).

## Model Fitting

### Bias Variance Tradeoff
#### Bias
* Definition: the difference between the average prediction of our model and the correct value which we are trying to predict
* notes:
	* Model with high bias pays very little attention to the training data and oversimplifies the model. It leads to high error on both training and test data.

#### Variance
* Definition: the variability of model prediction for a given data point.
* notes:
	* Model with high variance pays a lot of attention to training data and does not generalize on the data which it hasn’t seen before. Such models perform very well on training data but has high error rates on test data.
	* A value which tells us the spread of our data
