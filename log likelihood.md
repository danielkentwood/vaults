# log likelihood

[[likelihood]]
[[probability]]

Likelihoods often include the multiplication of multiple probabilities, and many of these probabilities are very small. When you multiply these together, the product can get so small that it is unstable in floating point precision. To keep things computationally tractable, we use log likelihood instead. This will preserve the relationships between variables that make up the probabilities, but it will be transformed into a scale that is more computationally stable.

