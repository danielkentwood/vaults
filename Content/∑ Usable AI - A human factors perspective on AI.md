# Usable AI: A human factors perspective on artificial intelligence

Human Factors is the study of the interaction between humans and their environment. These interactions give rise to a range of potential human actions, commonly referred to as *affordances.* Although remember that an affordance is a property of an object that arises out of its interaction with the perceiver's body and it environment.

What do AI models afford?

Models are typically not embodied, so the environment that they interact with is not the physical world. There are notable exceptions to this, like robotics and *maybe* voice assistants like Siri or Alexa. However, in these cases, their embodiment facilitates a kind of affordance that is governed by the interaction between the physical human body, the physical characteristics of the algorithm's embodiment, and the physical characteristics of their shared environment. This class of physical affordance is familiar to the field of human factors.

It is important to distinguish between 

- *User interface and experience* (UI/UX): principles of visual design and usability
    - What part of the human are we trying to fit?
        - Visual perception (e.g., gestalt principles)
        - Information seeking characteristics (e.g., explore/exploit profile, capacity limits)
    
- *Ergonomics*: principles of physical design and usability.
    - What part of the human are we trying to fit?
        - Physical/physiological characteristics.
    - Poor ergonomics can result in:
        - Injury to user
        - Damage to product
    - Good ergonomics can result in:
        - comfort for user
        - increased effectiveness of tool
        
- *Explainable AI* ([[XAI]]): principles of algorithmic design and usability
    - What part of the human are we trying to fit?
        - Cognitive characteristics (limitations and strengths), especially our decision-making processes

![Usable%20AI%20A%20human%20factors%20perspective%20on%20artificia%20be34bd1cfa9144a1a7fb569bbc32b0e9/HF_venn.svg](HF_venn.svg)

![Usable%20AI%20A%20human%20factors%20perspective%20on%20artificia%20be34bd1cfa9144a1a7fb569bbc32b0e9/untitled.svg](untitled.svg)

Critical idea: 

Even in the parts of the venn diagram where these 3 fields overlap, a product will have, for example, UI elements that are not impacted by the model being deployed, and it will have some UI elements that are.

The main point of this article is to expand our ideas about what XAI entails, and this includes a discussion of how XAI constrains design in the domains of UI/UX and ergonomics.

**Usable AI (UAI) is the intersection of XAI with UI/UX and ergonomics.**

A black box is not inherently bad. Indeed, much of what constitutes "good design" is an effective hiding of the parts of the product that are superfluous from a usability perspective. Good usability brings out only the mechanics of the product that are necessary to help the product serve its purpose, and stuffs everything else into a black box. 

Similarly, from a usability perspective, a deep learning model may not be very explainable, but it may be very usable, depending on its purpose. If the purpose of the model is to help a doctor gain confidence in medical diagnoses or prescriptions, part of the model designer's job is to facilitate an understanding of why the model produced a given output. This can include designing elements that provide intuition about the model architecture and function, elements that rank feature importance for the model in general and for that output in particular (e.g., Shapley values).

Models in production are typically involved in classifying current data (e.g., stratifying users for targeted ads), predicting future data (e.g., stock market forecasting), or generating novel data (e.g., deepfake).

Google rolled out its use of BERT in the Google Search in October 2019

[https://searchengineland.com/faq-all-about-the-bert-algorithm-in-google-search-324193#:~:text=BERT%2C%20which%20stands%20for%20Bidirectional,of%20words%20in%20search%20queries.](https://searchengineland.com/faq-all-about-the-bert-algorithm-in-google-search-324193#:~:text=BERT%2C%20which%20stands%20for%20Bidirectional,of%20words%20in%20search%20queries.)

The elegant interface for the Google search engine hides the fact that the user is interacting with a massive database and one of the most complex language models developed in recent times.

## Topics

- **Trust in automation**
- **NLP**
    - Interaction with bots
    - Google
    - 
    
- **Automation in industrial settings**
    - 
- **HAV/ADAS**
- **Clinical Decision Support**
    - [https://medium.com/chilmark-research/fda-guidance-on-clinical-decision-support-peering-inside-the-black-box-of-algorithmic-intelligence-1d24a143faa7](https://medium.com/chilmark-research/fda-guidance-on-clinical-decision-support-peering-inside-the-black-box-of-algorithmic-intelligence-1d24a143faa7)
    - 
- **Human understanding of machine intelligence**
    - Interpretable AI
        - [https://christophm.github.io/interpretable-ml-book/](https://christophm.github.io/interpretable-ml-book/)
        - [https://medium.com/this-week-in-machine-learning-ai/human-factors-in-machine-intelligence-with-james-guszcza-b61e022afa0e](https://medium.com/this-week-in-machine-learning-ai/human-factors-in-machine-intelligence-with-james-guszcza-b61e022afa0e)
            - Model optimization: there are many different constraints that one can use to optimize a model, and some of them are essentially human-centric (i.e., ethical considerations, interpretability, etc.)
        - Using neuroscience techniques to understand neural networks
            - Ablation techniques
            - Probing techniques
            - Konrad's paper: [https://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1005268](https://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1005268)
                - Causality
        - AutoML and abstraction away from the algorithm/decision process

NOTES:

- It seems that there are (at least) two areas in which human factors should constrain the deployment of AI.
    - First, if there is a need for transparency/interpretability in the decision process of the algorithm, then certain efforts must be made to educate the endpoint user about that decision process. It is a peek under the hood, so to speak, even if in layman’s terms.
    - Second, since the algorithms are typically complex and sometimes inscrutably so, we need to abstract away from the algorithm. We need to cover up the messiness and create an interface that distills the critical anthropocentric function of the algorithm in such a way that users immediately understand behavior of the model.