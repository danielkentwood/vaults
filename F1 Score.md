# F1 Score
parent:: [[model evaluation metrics]]

- brief description

F1 score (or, more generally, the F-score) is a measure of a binary classification model's performance on a dataset. The standard F1 score is the harmonic mean of precision and recall. 

- formula

**Standard F1 score:**

$$
F1=2\ \cdot\ \frac{precision\ \cdot\ recall}{precision\ + \ recall}
$$

Generalized F score:

$$
F_\beta=(1+\beta^2)\ \cdot\ \frac{precision\ \cdot\ recall}{(\beta^2\ \cdot\ precision) + \ recall}=\frac{(1+\beta^2)tp}{(1+\beta^2)tp+\beta^2fn+fp}
$$

where $\beta$ is a factor that describes how much more weight than [[model precision]] we want [[model recall]] to have. For example, if we think recall is twice as important as precision, we set $\beta=2$. If we think recall is half as important as precision, we set $\beta=0.5$.


![F1%20Score%2013829d2ecac54e43a0902525fe68164a/confusion_matrix.png](confusion_matrix.png)

- implementation
- implementation from scratch
- when should this be used?

When there are class imbalances.

- advantages

The F1 score is robust to class imbalances in the data. 

- disadvantages