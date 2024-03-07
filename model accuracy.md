# model accuracy
created:: 2022-08-31 05:16
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/gnosis
kind:: #zettel 
status:: #status/seed
parent:: [[model evaluation metrics]]
***


- brief description

Accuracy is a measurement of model performance. It is the percentage of correctly labeled observations. In other words, it is the sum of the true positives and true negatives, divided by the total number of observations.

- formula

$$
\text{ACC}=\frac{\text{TP + TN}}{N}
$$

where $N$ is the total population.

Here it is in the context of a [[confusion matrix]]

![F1%20Score%2013829d2ecac54e43a0902525fe68164a/confusion_matrix.png](confusion_matrix.png)

