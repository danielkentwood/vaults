# maximum likelihood estimation (MLE)

parent:: [[parameter estimation]]


The formula for a [[normal distribution]] is a conditional probability. It is the probability of $x$ given a particular mean $\mu$ and a particular [[standard deviation]] $\sigma$:

$$
P(x|\mu,\sigma)=\frac{1}{\sqrt{2\pi\sigma^2}}e^{-(x-\mu)^2/2\sigma^2}
$$

The formula for the likelihood of a given parameter uses exactly the same formula, but the conditional probability is now different. 

Let's say you want to estimate the mean of the normal distribution. Instead of asking what the value of $x$ is given $\mu$ and $\sigma$, we ask what $\mu$ is, given $x$ and $\sigma$. 

$$
L(\mu|x,\sigma)=\frac{1}{\sqrt{2\pi\sigma^2}}e^{-(x-\mu)^2/2\sigma^2}
$$

Now we can hold $\sigma$ and $x$ constant while we vary $\mu$. This will give us a distribution of likelihoods for $\mu$ (instead of a distribution of probabilities for $x$). The value of $\mu$ that results in the maximum likelihood value is most likely to be the true mean of the distribution.

But what if the value of $\sigma$ that you held constant was not accurate? How does that affect the MLE for the mean? 

