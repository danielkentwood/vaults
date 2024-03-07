# variational inference

links:: [[bayesian statistics]]

### brief description
We want to find the posterior distribution
It is hard to estimate the marginal distribution in many case.
So we create a variational distribution over latent (unknown) variables.

### algorithm




### formula
(1) We want to get the variational distribution over the latent variables:

$$
q(z_{1:m}|v)
$$

where $z$ are the latent variables, and $v$ are the variational parameters.

We want to find the settings of $v$ such that $q$ is close to the posterior $p$. If $q==p$, then this is vanilla EM (expectation maximization).

(2) We measure the closeness of the distributions using Kullback-Leibler (KL) divergence:

$$
KL(q\|p)\equiv \mathbb{E}_q \bigg[\text{log}\frac{q(Z)}{p(Z|x)} \bigg]
$$

where $\mathbb{E}$ is the expectation.

Notice the following:

- If q and p are high, you get a low divergence. They are close to each other.
- If q is high and p isn't, you pay a price.
- If q is low, we don't care what is happening with p.
- If KL = 0, the two distributions are equal.

This behavior is called "mode splitting": we want a good solution, not every solution.

This isn't finished yet. See [https://www.youtube.com/watch?v=2pEkWk-LHmU&ab_channel=JordanBoyd-Graber](https://www.youtube.com/watch?v=2pEkWk-LHmU&ab_channel=JordanBoyd-Graber) to continue with more concepts like ELBO (evidence lower bound) and plugging conditional probability into KL divergence, etc.

#### draw it

[https://app.diagrams.net/#](https://app.diagrams.net/#)
- implementation
- implementation from scratch
- when should this be used?
- advantages
- disadvantages
- notes

see these high-level notes: [https://www.cs.jhu.edu/~jason/tutorials/variational.html](https://www.cs.jhu.edu/~jason/tutorials/variational.html)

variational inference is a flavor of bayesian inference
in bayesian inference, we want to infer the posterior distribution. This is equal to the joint distribution divided by the marginal distribution of the evidence. *Problem: for many useful models, the marginal distribution of the evidence is hard or impossible to calculate analytically.*

Modes of bayesian inference:
- conjugate models with closed-form posteriors
- MCMC algorithms
- Approximate Bayesian computation
- Distributional approximations
	- Laplace approximations, INLA
	- Variational inference