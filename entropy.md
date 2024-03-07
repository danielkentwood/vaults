# entropy

In [[information theory]], the entropy of a random variable is the average level of "information", 'surprise", or "uncertainty" inherent in the variable's possible outcomes.

(1) The entropy of $X$ is defined as:

$$
H(X) = -\sum_{i=1}^n P(x_i)\cdot\text{log}P(x_i)
$$

where P(x) is the probability of observing category x in the current sample X.

The choice of base for the logarithm varies between different applications. Base 2 gives the unit of bits (or "shannons"). Base $e$ gives the "natural units" $nat$. Base 10 gives a unit called "dits", "bans", or "hartleys". 

Entropy is often used as a [[cost function]] for [[decision tree|decision trees]]

Intuitions behind Shannon's entropy: [https://towardsdatascience.com/the-intuition-behind-shannons-entropy-e74820fe9800](https://towardsdatascience.com/the-intuition-behind-shannons-entropy-e74820fe9800)