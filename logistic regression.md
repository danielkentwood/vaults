# logistic regression


Tags: [[classification]]

- brief description

Logistic regression is a classification model that treats the target variable as a probability given by a logistic function of the input features and the weights. After the probability has been calculated, class membership can be assigned.

Logistic regression model estimated probability:

$$
\hat{p}=h_{\theta}(x)=\sigma(x^T\theta)
$$

Logistic function:

$$
\sigma(t) = \frac{1}{1+e^{-t}}=\frac{e^t}{1-e^t}
$$

Expanded logistic function to include weight parameters $\theta$:

$$
h(x^{(i)},\theta)=\frac{1}{1+e^{-\theta^Tx^{(i)}}}
$$

Logistic regression model prediction:

$$
\hat{y}=\Bigg\{\begin{matrix}{0\quad \textrm{if} \quad \hat{p} < 0.5}\\{1\quad \textrm{if}\quad\hat{p}\geq0.5} \end{matrix}
$$

Cost function of a single training instance in logistic regression:

$$
c(\theta)=\Bigg\{\begin{matrix}{-log(\hat{p})\quad \textrm{if}\quad  y=1}\\{-log(1-\hat{p})\quad  \textrm{if}\quad y=0} \end{matrix}
$$

Logistic regression cost function (log loss):

$$
J(\theta) = -\frac{1}{m}\sum_{i=1}^m \Big[y^{(i)}log(\hat{p}^{(i)})+(1-y^{(i)})log(1-\hat{p}^{(i)})\Big]
$$

Logistic cost function partial derivative:

$$
\frac{\delta}{\delta\theta_j}J(\theta)=\frac{1}{m}\sum_{i=1}^m(\sigma(\theta^Tx^{(i)})-y^{(i)})x_j^{(i)}
$$

