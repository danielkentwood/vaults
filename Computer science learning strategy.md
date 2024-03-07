# Computer science learning strategy

[[∂ Career Dashboard]]
[[∂ Goal tracking]]
[[π Data Science Learning]]


**PORTFOLIO PROJECT 1. Py3DAllenConnect**

Skills/libraries employed: Python, image processing, API interaction, rendering engine

**PORTFOLIO PROJECT 2. Countdown**

Skills/libraries employed: scraping/curating CDC dataset,...

**PORTFOLIO PROJECT 3. SearchMoDB**

Skills/libraries employed: Python, NLP, MySQL, scraping (beautifulsoup, selenium), interactive web app with Dash, deployment to heroku

**PORTFOLIO PROJECT 4. Generic machine learning project**

Skills/libraries employed:

**PORTFOLIO PROJECT 5. Fixation prediction map**

Skills/libraries employed: openCV,...

**idea for a model:**

a model designed to satisfy needs by moving a "fovea" around an image.

features of model:

- fovea built up out of receptive fields mimicking the retina.
    - progagation of feedforward sensory information through successive maps, each with slightly different functions and RF arrangements.
- Need/skill competition model. There are competing needs that drive our eye movements, and we have skills for meeting these various needs. Start with just a few:
    - maximize information about potential search target during search
    - look at things that are highly conspicuous
- decaying VSTM. Assumes that you stitch together a representation of the scene by slowly building more detail, gradually revising the representation by replacing low frequency information with high frequency information, but the various features of this representation decay at different speeds. Objects decay the slowest. background textures, etc. decay the fastest.

**IDEAS**

Come up with a project that uses a MySQL database and a Keras implementation of a tensorflow server on google cloud servers ([https://blog.keras.io/keras-as-a-simplified-interface-to-tensorflow-tutorial.html#exporting-a-model-with-tensorflow-serving](https://blog.keras.io/keras-as-a-simplified-interface-to-tensorflow-tutorial.html#exporting-a-model-with-tensorflow-serving))

Come up with a project that uses a MongoDB database and a PyTorch model on AWS.

**Skills to develop/incorporate into the projects**

NLP

scraping (BeautifulSoup, Selenium, Scrapy)

databases (MySQL, MongoDB)

computer vision

This LDS general conference archive project potentially incorporates ALL of these skills into one project. I'll use scraping to store the conferences on [LDS.org](http://lds.org/) into a MySQL database. For the pre-1971 conference addresses on archive.org, I'll have to scrape the raw images, perform optical character recognition, clean up the text, add metadata, and store it in the database. After the database is complete, I'll analyze trends in messaging over time with various NLP techniques.

**SQL Course:**

**Deep Learning course:** [http://course.fast.ai/lessons/lesson1.html](http://course.fast.ai/lessons/lesson1.html)

**CERTIFICATIONS**

Amazon AWS Training: [https://www.aws.training/](https://www.aws.training/)

Google Cloud Training: [https://google.qwiklabs.com/home](https://google.qwiklabs.com/home)

Google AI training: [https://ai.google/education/](https://ai.google/education/)

**TensorFlow course**: [https://developers.google.com/machine-learning/crash-course/](https://developers.google.com/machine-learning/crash-course/), [https://github.com/tensorflow/workshops](https://github.com/tensorflow/workshops)

**COMPETITIONS AND SOCIAL LEARNING**

For computer science, math, algorithms: [https://www.hackerrank.com/dashboard](https://www.hackerrank.com/dashboard) **and** [https://www.topcoder.com/community/data-science/](https://www.topcoder.com/community/data-science/)

For machine learning: [https://www.kaggle.com/](https://www.kaggle.com/)

For algorithmic trading: [https://www.quantopian.com/home](https://www.quantopian.com/home)

**RESOURCES**

Free Code Camp: [https://learn.freecodecamp.org/](https://learn.freecodecamp.org/)

Scrimba (free lessons via webcasts): [https://scrimba.com/](https://scrimba.com/)

Elite Data Science: [https://elitedatascience.com/](https://elitedatascience.com/)

**JOB SEARCH**

[https://www.dataquest.io/blog/how-to-find-an-entry-level-job-in-data-science/](https://www.dataquest.io/blog/how-to-find-an-entry-level-job-in-data-science/)

**Trajectory**

**Computer Science:** Python ---> SQL ---> Hadoop ---> Spark ---> MongoDB ---> JavaScript ---> HTML/CSS/Jekyll ---> iOS (Swift)

**Machine learning:** TensorFlow ---> PyTorch

**Mathematics/Algorithms:** Bayesian statistics ---> Time Series ---> Linear algebra --->