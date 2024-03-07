# recall

Tags: [[model evaluation metrics]], [[classification]]



Recall or sensitivity is the ability of the model to correctly identify positive cases. Out of all the actual positive cases, how true positives did our model correctly label? It is also known as the True Positive Rate.


$$
\text{TPR}=\frac{\text{TP}}{\text{CONDITION POS}}
$$



![F1%20Score%2013829d2ecac54e43a0902525fe68164a/confusion_matrix.png](confusion_matrix.png)

- when should this be used?

Recall (or sensitivity) should be used when you don't want to mislabel positive cases (i.e. you want to capture as much of the positive class as possible). For example, if you are trying to predict a very deadly disease, you want to err on the side of caution and tune your model so that it has high recall (without giving up too much precision, of course)

