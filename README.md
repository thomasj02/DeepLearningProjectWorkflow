# Deep Learning Project Workflow

This document attempts to summarize Andrew Ng's recommended machine learning workflow from his ["Nuts and Bolts of Applying Deep Learning"](https://www.youtube.com/watch?v=F1ka6a13S9I&t=4192s) talk at Deep Learning Summer School 2016. Any errors or misinterpretations are my own.


# Start Here
1. Measure Human-level performance on your task ([More](#measuring-human-level-performance))
2.  Do your training and test data come from the same distribution?
    * [Yes](#if-your-training-and-test-data-are-from-the-same-distribution)
    * [No](#if-your-training-and-test-data-are-not-from-the-same-distribution)

***

# Measuring Human Level Performance
The real goal of measuring human-level performance is to estimate the [Bayes Error Rate](https://en.wikipedia.org/wiki/Bayes_error_rate). Knowing your Bayes Error Rate helps you figure out if your model is underfitting or overfitting your training data. More specifically, it will let us measure 'Bias' (as Ng defines it), which we use later in the workflow.
***
# If Your Training and Test Data Are From the Same Distribution

#### 1. Shuffle and split your data into Train / Dev / Test Sets
Ng recommends a Train / Dev / Test split of approximately 70% / 15% / 15%.

#### 2. Measure Your Training Error and Dev Set Error, and Calculate Bias and Variance
Calculate your bias and variance as:
* Bias = (Training Set Error) - (Human Error)
* Variance = (Dev Set Error) - (Training Set Error)

#### 3. Do You Have High Bias? [Fix This First.](#how-to-fix-high-bias)
An example of high bias:

Error Type | Error Rate
----|----
Human Error | 1%
Training Set Error | 5%
Dev Set Error | 6%

[Fix high bias](#how-to-fix-high-bias) before going on to the next step.

#### 4. Do You Have High Variance? [Fix High Variance](#how-to-fix-high-variance).

An example of high variance:

Error Type | Error Rate
----|----
Human Error | 1%
Training Set Error | 2%
Dev Set Error | 6%

Once you [fix your high variance](#how-to-fix-high-variance) then you're done!

***
# If Your Training and Test Data Are Not From the Same Distribution

#### 1. Split Your Data

If your train and test data come from different distributions, make sure at least your dev and test sets are from the same distribution. You can do this by taking your test set and using half as dev and half as test. 

Carve out a small portion of your training set (call this _Train-Dev_) and split your Test data into _Dev_ and _Test_:
```
|---------------------------------|-----------------------|
|     Train (Distribution 1)      | Test (Distribution 2) |
|---------------------------------|-----------------------|
|  Train              | Train-Dev |  Dev      |    Test   |
|---------------------------------|-----------------------|

```

#### 2. Measure Your Errors, and Calculate the Relevant Metrics

Calculate these metrics to help know where to focus your efforts:

Error Type | Formula
----|----
Bias | (Training Error) - (Human Error)
Variance | (Train-Dev Error) - (Training Error)
Train/Test Mismatch | (Dev Error) - (Train-Dev Error)
Overfitting of Dev | (Test Error) - (Dev Error)

#### 3. Do you have High Bias? [Fix Your High Bias](#how-to-fix-high-bias).

An example of high bias:

Error Type | Error Rate
----|----
Human Error | 1%
Training Set Error | 10%
Train-Dev Set Error | 10.1%
Dev Set Error | 10.2%

[Fix high bias](#how-to-fix-high-bias) before going on to the next step.


#### 4. Do You Have High Variance? [Fix Your High Variance](#how-to-fix-high-variance).

An example of high variance:

Error Type | Error Rate
----|----
Human Error | 1%
Training Set Error | 2%
Train-Dev Set Error | 10.1%
Dev Set Error | 10.2%

[Fix your high variance](#how-to-fix-high-variance) before going on to the next step.


#### 4. Do You Have Train/Test Mismatch? [Fix Your Train/Test Mismatch](#how-to-fix-traintest-mismatch).

An example of train/test mismatch:

Error Type | Error Rate
----|----
Human Error | 1%
Training Set Error | 2%
Train-Dev Set Error | 2.1%
Dev Set Error | 10%


[Fix your train/test mismatch](#how-to-fix-traintest-mismatch) before going on to the next step.


#### 5. Are you Overfitting Your Dev Set? [Fix Your Overfitting](#how-to-fix-overfitting-of-your-dev-set)

An example of overfitting your dev set:

Error Type | Error Rate
----|----
Human Error | 1%
Training Set Error | 2%
Train-Dev Set Error | 2.1%
Dev Set Error | 2.2%
Test Error | 10%

Once you [fix your dev set overfitting](#how-to-fix-overfitting-of-your-dev-set), you're done!

***

# How to Fix High Bias
Ng suggests these ways for fixing a model with high bias:
* **Try a bigger model**
* Try training longer
* Try a new model architecture (this can be hard)

# How to Fix High Variance
Ng suggests these ways for fixing a model with high variance:
* **Get more data**
  * This includes data synthesis and data augmentation
* Try adding regularization
* Try early stopping
* Try new model architecture (this can be hard)



# How to Fix Train/Test Mismatch

Ng suggests these ways for fixing a model with high train/test mismatch:
* Try to get more data similar to your test data
* Try data synthesis and data augmentation
* Try new model architecture (this can be hard)

# How to Fix Overfitting of Your Dev Set

Ng suggests only one way of fixing dev set overfitting:
* Get more dev data

Presumably this would include data synthesis and data augmentation as well.


