
Adversarial validation is a form of [[model validation]] that is actually, secretly, doing [[data validation]].

From [this article](https://blog.zakjost.com/post/adversarial_validation/) by Zak Jost:

> In short, we build a classifier to try to predict which data rows are from the training set, and which are from the test set. If the two datasets came from the same distribution, this should be impossible. But if there are systematic differences in the feature values of your training and test datasets, then a classifier will be able to successfully learn to distinguish between them. The better a model you can learn to distinguish them, the bigger the problem you have.
> 
> But the good news is that _you can analyze the learned model to help you diagnose the problem_. And once you understand the problem, you can go about fixing it.

In other words, if your model is able to correctly classify whether a sample came from the training or the test set, it means that the distributions are different in some way. This is bad because it will impair the ability of your model to generalize what it learned during training to the new test data. 

You'll want to discover which features are contributing most to the adversarial validation model, investigate what is different between the two distributions, and find a way to correct it. 

