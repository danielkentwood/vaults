# AdaBoost (adaptive boosting)

[[Gradient boosting]]

Weighted error of the $j^{th}$ predictor:

$$
r_j=\quad
\frac{
\sum\limits_{\mathclap{\substack{i=1\\
\hat{y}_j^{(i)}\neq y^{(i)}}}}^m w^{(i)}
}
{\sum\limits_{i=1}^m w^{(i)}}

$$

where $y_j^{(i)}$ is the $j^{th}$ predictor's prediction for the $i^{th}$ instance.

Predictor weight:

$$
\alpha_j=\eta \ log\frac{1-r_j}{r_j}
$$

Weight update rule:

for $i=1,2,...,m$

$$
w^{(i)}\leftarrow\Bigg\{\begin{matrix}{
w^{(i)}\quad \textrm{if}\quad \hat{y}_j^{(i)}= y^{(i)}} \\{
w^{(i)} e^{\alpha_j} \quad \textrm{if} \quad \hat{y}_j^{(i)}\neq y^{(i)}} \end{matrix}
$$

AdaBoost predictions:

$$
\hat{y}(x) = \arg \max_k\quad\sum\limits_{\mathclap{\substack{
j=1\\
\hat{y}_j(x)=k}}}
^N
\alpha_j
$$
