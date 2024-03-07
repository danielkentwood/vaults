# isolation forest

Isolation forest is an algorithm for [[outlier detection]]. It involves a [[random forest]] in which each [[decision tree]] is grown randomly.

Approach:

- At each node, a tree picks a feature randomly and then picks a random threshold value (between min and max values) to split the data set in two.
- Repeat this until all instances are isolated from other instances.
- Across all decision trees, outliers tend to be isolated in fewer steps than other instances.

It works particularly well in high-dimensional datasets.

