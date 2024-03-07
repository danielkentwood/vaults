# LIME

Tags: [[XAI]]

LIME (Local Interpretable Model-Agnostic Explanations) is a method for explaining [[classification]] models. It can explain ***why*** a single data point was classified as a specific class without knowing ***how*** the model makes its predictions.

LIME objective (minimization function)

$$
\xi =  \underset{g\in G}\arg\min L(f,g,\pi_{x'})+\Omega(g)
$$

where $L$ is the loss function (pushes everything closer together), $\pi_{x'}$ is the local kernel (defines what local means), and $\Omega$ is the regularizer.

These are typically chosen heuristically.


### disadvantages
- Depends on the random sampling of new points, so it can be unstable. Not deterministic.
- Fit of linear model can be inaccurate.
	- But we can check the r-squared to know if that's the case.
- Relatively slow for a single observation, in particular with images.

### original paper
[LIME%20a5d31c8d6935454ab89ab7a6a7fd8148/1602.04938.pdf](1602.04938.pdf)

### useful resources
- [https://www.youtube.com/watch?v=C80SQe16Rao&ab_channel=PyData](https://www.youtube.com/watch?v=C80SQe16Rao&ab_channel=PyData)