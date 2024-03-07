# Purchase propensity modeling
created:: 2022-08-31 05:17
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/gnosis
kind:: #zettel 
status:: #status/seed
parent:: [[propensity model]]
***

## Question

How would you build a model to calculate a customer's propensity to buy a particular item? What are some pros and cons of your approach?

## Answer/Discussion

The standard approach is to:

1. Construct a large dataset with the variable of interest (purchase or not), along with relevant covariates (age, gender, income, etc.) for a sample of users on the platform.
2. Build a model to calculate the probability of purchase of each item.

In deciding a model, a [[logistic regression]] offers a straightforward solution with an interpretable outcome: the resulting log-odds is a **probability score** for buying a particular item. However, it cannot capture complex interaction effects between different variables and also might be numerically unstable under certain conditions (correlated covariates and a small user base).

An alternative to using logistic regression would be to use a more complex model such as a [[neural networks|neural network]] or [[support vector machine]]. Both are great with dealing with high-dimensional data, and capturing complex interactions that logistic regression cannot. However, in both cases, they lack explainability in the model and generally require a large amount of data for better performance gains versus logistic regression.


## External Resources


