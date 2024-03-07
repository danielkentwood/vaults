# Laplace (additive) smoothing

Tags: [[NLP]]

A form of smoothing that imputes a non-zero probability to out-of-sample items (e.g., in Naive Bayes classification).

Formula for smoothing a probability of an element $W_{pos}$:

$$
P(W_{pos})=\frac{freq_{W_{pos}}+1}{N_{pos}+V}
$$
where:

- $W_{pos}$ is an element is the $pos$ class.
- $freq_{W_{pos}}$ is the frequency of a given element in the $pos$ class.
- $N_{pos}$ is the total number of elements in the $pos$ class.
- $V$ is the number of unique elements in the dataset, across all classes.
