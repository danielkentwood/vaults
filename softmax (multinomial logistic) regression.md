# softmax (multinomial logistic) regression


Tags: [[regression]]


The softmax function converts any vector of K real values into a vector of K real values that are between 0 and 1, and that sum to 1. This lets you interpret them as probabilities.

**Relationship to the sigmoid function:** 

The sigmoid function is a special case of the softmax function for a classifier with only two input classes. Also, the softmax function operates on a vector while the sigmoid function operates on a scalar. 

**score for class k:**

$$
s_k(x) = x^T\theta^{(k)}
$$

**Softmax function:**

$$
\hat{p}_k=\sigma(s(x))_k=\frac{e^{s_k(x)}}{\sum_{j=1}^Ke^{s_j(x)}}
$$

where $K$ is the number of classes, $s(x)$ is a vector containing scores of each class for the instance $x$, and $\sigma(s(x))_k$ is the estimated probability that the instance $x$ belongs to the class $k$, given the scores of each class for that instance.

Another, more general way of formulating it is as follows:

$$
\sigma(\vec{z})_i=\frac{e^{z_i}}{\sum_{j=1}^Ke^{z_j}}
$$

Here, $\vec{z}$ is just the input vector to the softmax function. In the upper formulation, it is equal to $s_k(x)$, which is the predicted score for an instance of class $k$ (see above).

**Softmax regression classifier prediction:**

$$
\hat{y}=\arg\max_k\ \sigma(s(x))_k=\arg\max_k\ s_k(x)=\arg\max_k\ \big(\big(\theta^{(k)}\big)^Tx\big)
$$

**Cross entropy cost function:**

$$
J(\Theta)=-\frac{1}{m}\sum_{i=1}^Ky_k^{(i)}log(\hat{p}_k^{(i)})
$$

where $y_k^{(i)}$ is the target probability that the $i^{th}$ instance belongs to class $k$. 

**Cross entropy gradient vector:**

$$
\nabla_{\theta^{(k)}}J(\Theta)=\frac{1}{m}\sum_{i=1}^m\big(\hat{p}_k^{(i)}-y_k^{(i)}\big)x^{(i)}
$$

where $\Theta$ is the parameter matrix.
