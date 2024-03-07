# Shapley values

links:: [[XAI]]

- brief description
    
    Shapley Additive Explanations
    
    Like [[LIME|LIME]], Shapley is an example of an [[additive feature attribution method]], where the local explanation is a linear function of the features.
    
    In a linear model, we attribute credit to a particular feature based on the learning of weights.
    
    ![Output is a linear function of features times weights.](Untitled%2019.png)
    
    Output is a linear function of features times weights.
    
    For many models, we don't have direct access to the transformations that condition our input features in order to produce an output. 
    
    ![In some models, output is a combination of features, but the transformations of those features are often opaque.](Untitled%201%207.png)
    
    In some models, output is a combination of features, but the transformations of those features are often opaque.
    
    Additive Feature Attribution methods introduce at the local level some function that assigns credit for the output to each feature.
    
    ![In AFA, output is a linear combination of features multiplied by some transformation that ultimately signifies the credit that is attributed to feature X_m.](Untitled%202%202.png)
    
    In AFA, output is a linear combination of features multiplied by some transformation that ultimately signifies the credit that is attributed to feature X_m.
    
    For Shapley Values, the $\phi$ is baed on game theory.
    
    To get the importance of feature $X\{i\}$:
    
    - Get all subsets of features $S$ that do not contain $X\{i\}$
    - Compute the effect on our predictions of adding $X\{i\}$ to all those subsets.
    
    Shapley Properties
    
    1. Local accuracy (additivity): the sum of the local feature attributions equals the difference between the base rate and the model output.
        
        $$
        f(x) = E[f(x)]+\sum_{i=1}^M \phi_i
        $$
        
    2. Consistency (monotonicity): If you change the original model such that a feature has a larger impact in every possible ordering, then that input's attribution should not decrease. 
        - Violating consistency means you can't trust feature orderings based on your attributions, even within the same model.
    
    Shapley values result from averaging over all N! possible orderings of features. 
    
    - * This is obviously going to get computationally intractable very fast, especially with a large number of features.
    
    Options for NP-hard problems
    
    1. Prove that P=NP.
    2. Find an approximate solution. 
    
- formula
- draw it
    
    [https://app.diagrams.net/#](https://app.diagrams.net/#)
    
- implementation
    
    
- implementation from scratch
- when should this be used?
- advantages
- disadvantages
    - It can be computationally expensive, but SHAP has different optimizations for different models (linear, trees, etc)
        - TreeExplainer
            - Only for tree based models
            - Works with scikit-learn, xgboost, lightgbm, catboost
        - KernelExplainer
            - model agnostic explainer
- Helpful resources
    - Open the Black Box: Intro to Model Interpretability
        - [https://www.youtube.com/watch?v=C80SQe16Rao&ab_channel=PyData](https://www.youtube.com/watch?v=C80SQe16Rao&ab_channel=PyData)
    - Explainable AI for Science and Medicine
        - [https://www.youtube.com/watch?v=B-c8tIgchu0&t=414s&ab_channel=MicrosoftResearch](https://www.youtube.com/watch?v=B-c8tIgchu0&t=414s&ab_channel=MicrosoftResearch)