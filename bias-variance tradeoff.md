# bias-variance tradeoff

[[ML optimization]]

**The bias-variance tradeoff is literally the [[faith versus good faith]] distinction applied to models.** 

**Bias** = how poorly the model fits the data. If you're biased, you're ignoring the data and underfitting. You have a model that ignores the relevant signal in the data. This leads to **underfitting**.

**[[variance]]** = magnitude of change in the model based on changes in the data. Sometimes you're not biased enough. You pay too much attention to the data, introducing too much variance into the model itself. This leads to **overfitting**.

As the number of parameters in a model increases, the variance tends to increase. 

Too much of either bias or variance results in generalization error (underfitting or overfitting). The optimal model is one that balances bias and variance by decreasing (via [[regularization]] and other forms of [[dimensionality reduction]]) or increasing (via [[feature engineering]], etc.) the number of parameters.

- draw it
    
    ![bias-variance%20tradeoff%2070a8df1eb73b4795a140779005f00e98/IMG_3930.jpg](IMG_3930.jpg)

