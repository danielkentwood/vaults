# Unifying intuitions for hypothesis testing
Allen Downey has a few articles that attempt to contextualize the historically motivated apparent differences between the various hypothesis testing approaches that we learn in school. Essentially, these articles attempt to argue that the parametric approach of naming tests after the test statistic unnecessarily obfuscates the underlying logic that drives all hypothesis testing. 

1. [There is only one test!](http://allendowney.blogspot.com/2011/05/there-is-only-one-test.html)
2. [There is still only one test](http://allendowney.blogspot.com/2016/06/there-is-still-only-one-test.html)

His point is that if we look at [[hypothesis testing]] from a simulation perspective, all hypothesis tests have the same logic. The framework looks like this:

![[Pasted image 20220707141927.png]]

Here is a more detailed breakdown of the framework:

> 1) Given a dataset, you compute a **test statistic** that measures the size of the apparent effect.  For example, if you are describing a difference between two groups, the test statistic might be the absolute difference in means.  I'll call the test statistic from the observed data 𝛿*.  
>   
> 2) Next, you define a **null hypothesis**, which is a model of the world under the assumption that the effect is not real; for example, if you think there might be a difference between two groups, the null hypothesis would assume that there is no difference.  
>   
> 3) Your model of the null hypothesis should be stochastic; that is, capable of generating random datasets similar to the original dataset.  
>   
> 4) Now, the goal of classical hypothesis testing is to compute a p-value, which is the probability of seeing an effect as big as 𝛿* under the null hypothesis.  You can estimate the p-value by using your model of the null hypothesis to generate many simulated datasets.  For each simulated dataset, compute the same test statistic you used on the actual data.  
>   
> 5) Finally, count the fraction of times the test statistic from simulated data exceeds 𝛿*.  This fraction approximates the p-value.  If it's sufficiently small, you can conclude that the apparent effect is unlikely to be due to chance ([if you don't believe that sentence, please read this](http://allendowney.blogspot.com/2015/05/hypothesis-testing-is-only-mostly.html)).


***

Here is a nice Medium article that was inspired by the Downey articles:

[Data Scientists Need to Know Just One Statistical Test](https://medium.com/towards-data-science/data-scientists-need-to-know-just-one-statistical-test-3115b2ff26fd)

Here is the algorithm, copy-pasted from the article:

> 1. Define a function `draw_random_outcome`. This function should return the outcome of a random trial, given that the null hypothesis is true. It may be a single number, an array, a list of arrays, an image, practically anything: it depends on the specific case.
> 2. Define a function `unexp_score` (which stands for “unexpectedness score”). The function should take an experiment outcome as input, and return a single number. This number must be a score of how unexpected the outcome is, assuming it was generated under the null hypothesis. The score may be positive, negative, integer, or float, it doesn’t matter. The only property it must have is the following: **the unlikelier the outcome is, the higher this score must be**.
> 3. Run many times (e.g. 10,000 times) the function `draw_random_outcome` (defined at point 1) and, for each random outcome, compute its `unexp_score` (defined at point 2). Store all the scores in an array called `random_unexp_scores`.
> 4. Compute `unexp_score` of the observed outcome, and call it `observed_unexp_score`.
> 5. Compute how many random outcomes are more unexpected than the observed outcome. That is to say, count how many elements of `random_unexp_scores` are higher than `observed_unexp_score`. This is the p-value.

The first two steps require some creativity. The last 3 are always the same.

The author applies this algo to 4 different examples, showing how it generalizes. 
