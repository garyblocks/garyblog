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

#### Tradeoff
\\[
    Y = f(X) + e
\\]
\\[
    Err(x) = E[(Y - \hat{f}(x))^2]
    = (E[\hat{f}(x)]-f(x)])^2 + E[(\hat{f}(x) - E[\hat{f}(x)])^2] +  \sigma^2_e,
\\]
\\[
    Err(x) = Bias^2 + Variance + Irreducible Error
\\]

* underfitting:
	* happens when a model unable to capture the underlying pattern of the data.
	* These models usually have high bias and low variance.
	* It happens when we have very less amount of data to build an accurate model or when we try to build a linear model with a nonlinear data. 
* overfitting 
	* happens when our model captures the noise along with the underlying pattern in data.
	* These models have low bias and high variance. 
	* It happens when we train our model a lot over noisy dataset.

	