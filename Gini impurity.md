# Gini impurity

Gini impurity is a [[cost function]] used by the [[CART (classification and regression tree) algorithm]] for a classification [[decision tree]].

Gini impurity is a measure of how often a randomly chosen element from the set would be incorrectly labeled if it was randomly labeled according to the distribution of labels in the subset.

It reaches a minimum (zero) when all cases in the node fall into a single target category.

The gini impurity of a feature is:

$$
G=\sum_{i=1}^C P(i)\cdot(1-P(i))
$$

where $P(i)$ is the probability of a certain class $i$.
