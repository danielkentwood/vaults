# π Data Science Skill Checklist

##### Metadata
created:: 2022-08-31 05:16
modified:: <%+ tp.file.last_modified_date() %>
mode:: #mode/management
kind:: #project 
status:: #status/raw
parent:: [[π Data Science Learning]]
ignoreTasks:: True
***
## Project Summary

***
## Rollups
### Subprojects
```dataview
TABLE
FROM #project 
WHERE contains(parent, link(this.file.name))
```

### Task backlog
```dataviewjs

let curr = dv.current();
let curr_nm = curr.file.name;

let proj_pages = dv.pages('#project')
	.where(p => 
		dv.array(p.parent).includes(dv.current().file.link) ||
		p.file.name == curr_nm
	)
	.file.link

let all_tasks = dv.pages().file.tasks
	.where(t => t.project)
	.where(t => proj_pages.includes(t.project)
	)

let done_tasks = all_tasks.where(t => t.completed)
let still_tasks = all_tasks.where(t => !t.completed)
	
dv.header(4, 'Remaining tasks:')	
if (still_tasks.length > 0){
    for (let group of still_tasks
		    .groupBy(t => t.project)
		){
			dv.header(5, group.key)
			dv.taskList(group.rows, false)
		}
} else {
	dv.el("em", "No pending tasks")
}

dv.paragraph('<br><hr>')
dv.header(4, 'Completed tasks:')	
if (done_tasks.length > 0){
    for (let group of done_tasks
		    .groupBy(t => t.project)
		){
			dv.header(5, group.key)
			dv.taskList(group.rows, false)
		}
} else {
	dv.el("em","No completed tasks")
}
```
***
### Meetings
```dataview
table created
from #meeting and #mode/management and #aetna
where contains(parent, link(this.file.name))
sort created asc
```

### Contextual Notes
```dataviewjs
let curr = dv.current()

let pages = dv.pages("#periodic/daily and -#project")
	.where(p => {
		if (p.sendto) {
			let sendto = dv.isArray(p.sendto) ? 
				p.sendto : 
				dv.array(p.sendto);
			if (sendto.some(str => str.includes(curr.file.name))) {
				return true
			}
		}		
	})
	.sort(p => p.file.cday, "asc")

function formatLinks(page) {
	let st_arr = dv.isArray(page.sendto) ?
		page.sendto.filter(str => str.includes(curr.file.name)) :
		dv.array(page.sendto).filter(str => str.includes(curr.file.name));

	let link_arr = st_arr.map(str => {
		return dv.sectionLink(
			page.file.name,
			("sendto:: " + str.replace(/\[\[/g, '').replace(/\]\]/g, '')),
			false,
			str.replace(/\[\[.*?\]\]/g, '')
		)
	});

	return link_arr
}

// set up table
dv.table(
	["File", "Note"], 
	pages
	.map(b => [
		b.file.link,
		formatLinks(b)
	])
)
```


***
## Documentation











# Data Science Skill Checklist

This is a checklist of topics and skills that are important for any data scientist to have in their toolkit. For each topic, complete the following:

1. Gather information through articles, courses, tutorials, books, etc.
2. Write a MVP notebook demonstrating the concept
3. Condense the information and code into a brief blog post.

**GETTING DATA**

- SQL
	- Setting up access to a SQL database in Python
	- Performing complex SQL queries (subqueries, windows, complex joins)
	- Putting the SQL pull into various data structures (dictionaries, pandas dataframes, numpy arrays, etc.)
- Scraping
	- Use your favorite package (e.g., Scrapy, BeautifulSoup) to scrape data from a variety of websites.
	- Use Selenium to scrape data from websites that require interaction with forms, logins, etc.
	- Store the scraped data into a variety of storage options (e.g., local and cloud-based SQL, pickled dataframe, JSON, csv, etc.)

**CLEANING AND PREPROCESSING DATA**

- Handling missing data
	- Imputation
	- Interpolation
- Handling outliers
	- Removal
	- Treat outliers as NaN
	- Capping & Windsorisation
- Scaling
	- Normalization
	- Standardization
- Test-Val-Train split
- Smoothing

**FEATURE ENGINEERING**

- Data Augmentation
- Transformations
	- Logarithm
	- Reciprocal
	- Square root
	- Exponential
	- Yeo-Johnson
	- Box-Cox
- Dealing with categorical variables
	- One-hot encoding
	- Count and frequency encoding
	- target/mean encoding
	- Ordinal encoding
	- Weight of evidence
	- rare label encoding
	- BaseN
	- Feature hashing
- Discretisation (binning)
	- Equal frequency discretisation
	- Equal width discretisation
	- Tree discretisation
	- ChiMerge discretisation
- Feature joining
	- sum, subtract, mean, min, max, product, quotient of group of features
- Feature splitting
- Working with dates
- Text features
	- Bag of words
	- TFIDF
	- n-grams
	- word2vec
	- topic extraction

**ANALYZING DATA**

- Dimensionality Reduction
	- PCA
	- Regularization
	- T-SNE
	- Autoencoder
- Pivot table
- Distributed computing
	- Spark
		- Use pySpark to set up Spark instance in jupyter.
		- Use pySpark to analyze a dataset

**VISUALIZING DATA**

- Distribution plots
- Correlation matrices
- Depicting parameter variability
	- Error bar
	- Box plot
	- Violin plot

**STATISTICS**

- Hypothesis Testing
- Causal Inference
- Bayesian Inference
	- MLE
	- MAP
	- Bayesian updating
- A/B Test
- Power Analysis

**BUILDING MODELS**

- Hyperparameter tuning
	- Grid Search
	- Random Search
- Supervised
	- Tree-based models
		- Decision trees
		- Random forest
		- Boosting
		- Bagging
		- Stacking
	- Linear Regression
	- Logistic Regression
	- Naive Bayes
	- K-Nearest Neighbor
	- Support Vector Machines
- Unsupervised
	- K-Means Clustering
	- Hierarchical Clustering
	- Mixture Models
	- DBSCAN
	- Anomaly Detection
	- Latent Variable Models (Expectation-Maximization, blind signal separation)
- Neural Networks
	- Multilayer Perceptron
	- Convolutional Neural Networks
	- LSTM/GRU
	- Recurrent Neural Networks
	- Deep Belief Networks
	- Deep Stacking Networks

**EVALUATING MODELS**

- ROC
- Cross-validation
- Classification metrics
	- Confusion matrix
- Regression metrics

**INTERPRETING MODELS**

- LIME
- Shapley Values

**DEPLOYING MODELS**

- Cloud Platforms
	- AWS
	- Google Cloud Services
	- Heroku

**MLOPS (Maintaining models)**

**SPECIAL TOPICS**

- NLP
	- Attention
	- Sentiment Analysis
	- Language Models
	- Topic Modeling
		- Latent Semantic Analysis via SVD
		- Non-negative matrix factorization (NMF)
		- TF-IDF
		- Latent Dirichlet Allocation
	- Embeddings
		- Word2Vec
		- Sentence and document embeddings
		- Graph embeddings
	- Transfer Learning
	- Knowledge graphs
- Computer Vision
	- YOLO
	- Salience Map





- **Workera Skills to improve**
    
    [https://workera.ai/](https://workera.ai/)
    
    **For each skill, create a card in the knowledge review database, then check it off.**
    
    - Math
        - [ ]  Finding an incoherence in a mathematical proof
        - [ ]  Taking the integral of a function
        - [ ]  Calculating the gradient of a function
        - [ ]  Taking the derivative of the sigmoid function
        - [ ]  Taking the derivative of the tanh function
        - [ ]  Evaluating the argmax of a function
        - [ ]  Identifying a convex function
        - [x]  Taking the sigmoid of a vector
        - [x]  Taking the softmax of a vector
        - [x]  Understanding the difference between sigmoid and softmax functions
        - [ ]  Summing elements of vectors
        - [ ]  Taking the outer product of two vectors
        - [ ]  Performing a matrix/vector multiplication
        - [ ]  Performing a matrix/matrix multiplication
        - [ ]  Taking the dot product of a matrix and a vector
        - [ ]  Understanding the properties of the trace
        - [ ]  Finding the eigenvalues of a matrix
        - [ ]  Finding the eigenvectors of a matrix
        - [ ]  Understanding the relationship between the determinant of a matrix and its invertibility
        - [ ]  Understanding the properties of a matrix's inverse
    - Data Science
        - [ ]  Calculating a mean using a PDF
        - [ ]  Understand the direction of the vector of residuals
        - [ ]  Differentiating generative and discriminative models
        - [ ]  Understanding the properties of a latent variable
        - [ ]  Identifying independent events in probabilities
        - [ ]  Identifying when to use hypothesis testing
        - [ ]  Calculate the expectation of a random variable
        - [ ]  Calculate the variance of a random variable
        - [ ]  Defining good hypotheses in a hypothesis test
        - [ ]  Analyzing a residuals plot
        - [ ]  Calculating a probability using a density function
        - [ ]  Calculating the expected value of the sum of two random variables
        - [ ]  Calculating a probability when a random variable follows a binomial distribution
        - [ ]  Calculating conditional probabilities using the Bayes rule
        - [ ]  Calculating the probability of an intersection of events
        - [ ]  Calculating the probability of a sum of random variables
        - [ ]  Computing the probability of a series of n independent events
        - [ ]  Recognizing the mean and variance of a normal distribution on a frequency plot
        - [ ]  Taking the exponential of a logarithmic regression model
        - [ ]  Identifying when to use R-squared
        - [ ]  Enunciating the Central Limit Theorem (CLT)
        - [ ]  Compute the mean and variance of a Bernoulli distributed random variable
        - [ ]  Calculating the mean of the binomial distribution
        - [ ]  Analyzing the implications of a logarithmic regression model
        - [ ]  Calculating a probability when a random variable follows a uniform distribution
    - SWE
        - [ ]  Making good software design decisions
        - [ ]  Understanding the open/closed principle
        - [ ]  Understanding classes and inheritance
        - [ ]  Understanding the purpose of static code analysis
        - [ ]  Making an Entity Relationship Diagram
        - [ ]  Choosing test cases in whitebox testing
        - [ ]  Understanding the role of the Hostname in a request
        - [x]  Understanding the SQL WHERE clause
        - [ ]  Understanding the purpose of a load balancer
        - [ ]  Managing access permissions
        - [ ]  Understanding the factory method
        - [ ]  Understanding what is structured data
        - [ ]  Understanding HTTP response status codes
        - [ ]  Understanding the single responsibility principle
        - [ ]  Understanding decorators
        - [x]  Understanding the different SQL joins
        - [ ]  Understanding the syntax of the JSON format
        - [ ]  Understanding the difference between concurrency and parallelism
        - [ ]  Understanding cookies and domains
        - [x]  Applying the SQL COUNT function
        - [ ]  Understanding method overriding
        - [ ]  Understanding latency and throughput
        - [ ]  Understanding the purpose of different HTTP requests
        - [ ]  Using LIMIT and OFFSET clauses
        - [ ]  Understanding idempotency in HTTP verbs
        - [ ]  Understanding race conditions
        - [x]  Version control
        - [ ]  Understanding the singleton pattern
        - [x]  Cloning a Git repository
        - [ ]  Understanding the purpose of the test coverage metric
        - [ ]  Differentiating Monolithic vs. Microservices architectures
        - [ ]  Identifying problems in unnormalized tables
        - [x]  Understanding the purpose of branching in Git
        - [ ]  Understanding the concept of infrastructure as code
        - [ ]  Understanding the iterator pattern
        - [ ]  Differentiating unit and functional testing
        - [ ]  Choosing test cases in blackbox testing
        - [ ]  Choosing primary keys
        - [ ]  Understanding safe HTTP verbs
        - [ ]  Understanding derived tables
    - Algorithms
        - [ ]  Understanding Bubble sort
        - [ ]  Understanding the implementation of Depth First Search
        - [ ]  Understanding Merge sort
        - [ ]  Solving a problem with recursion
        - [ ]  Traversing a tree in a certain order
        - [ ]  Choosing a good data structure to solve a coding problem
        - [ ]  Understanding Quick sort
        - [ ]  Understanding the Euclidean algorithm
        - [ ]  Looping over list/array indices
        - [ ]  Understanding code written by others
        - [ ]  Analyzing a code function
        - [ ]  Implementing a code solution to solve a problem
        - [ ]  Understanding insertion sort
        - [ ]  Understanding the implementation of A-star
        - [ ]  Filling the blanks in a code function
        - [ ]  Accessing elements in nested lists
        - [ ]  Understanding the implementation of binary searchv
        - [ ]  Solving a problem with dynamic programming
    - ML
        - [ ]  Deriving the gradient descent update rule given a loss function
        - [ ]  Interpreting the linear regression coefficients
        - [ ]  Fixing a high variance model
        - [ ]  Differentiating stochastic from batch gradient descent
        - [ ]  Understanding properties of the Bayes error
        - [ ]  Choosing the right dataset split between train, dev and test sets
        - [ ]  Deciding when to use a decision tree ensemble
        - [ ]  Avoid computational overflow/underflow of softmax
        - [ ]  Examining a dataset
        - [ ]  Understanding the curse of dimensionality in K-means
        - [ ]  Choosing the correct evaluation metrics for imbalanced datasets
        - [ ]  Choosing the right loss function to use
        - [ ]  Understanding the impact of a distribution mismatch between train, dev and test sets
        - [ ]  Choosing when to use end-to-end learning
        - [ ]  Understanding L2 loss
        - [ ]  Understanding the equation of a hyperplane in a n-dimensional space
        - [ ]  Understanding the details of Principal Component Analysis
        - [ ]  Quantifying the penalty due to L2 regularization
        - [ ]  Deciding when to use K-nearest neighbors
        - [ ]  Selecting the principal components of a data matrix
        - [ ]  Understanding the hyperparameters of K-means
        - [ ]  Estimating the bias on the generalization error due to using cross validation
        - [ ]  Reducing avoidable bias
        - [ ]  Evaluating the output of a trained logistic regression model
        - [ ]  Understanding the impact of K in K-fold cross validation
        - [ ]  Understanding epochs
        - [ ]  Understanding L1 loss
        - [ ]  Estimating the Bayes error
        - [ ]  Quantifying the penalty due to L1 regularization
        - [ ]  Cleaning up incorrectly labelled data
        - [ ]  Understanding logistic loss
        - [ ]  Drawing the decision boundary of a Support Vector Machine
        - [ ]  Analyzing the bias/variance to improve model performance
        - [ ]  Understanding the effect of linearly separable data on logistic regression
        - [ ]  Understand the decision boundary of classic ML models
        - [ ]  Comparing the performance of models given their ROC curves
        - [ ]  Measuring avoidable bias
        - [ ]  Choosing an appropriate kernel for a Support Vector Machine
        - [ ]  Understanding the curse of dimensionality in K-nearest neighbors
        - [ ]  Understanding the details of K-nearest neighbors
        - [ ]  Counting the parameters of a linear regression
    - Deep Learning
        - [ ]  Understanding the filters in a maxpooling layer
        - [ ]  Understanding the forward propagation in a maxpooling layer
        - [ ]  Calculating the number of parameters in a fully-connected neural network
        - [ ]  Understanding the Intersection over Union metric
        - [ ]  Understanding the filters in a convolution layer
        - [ ]  Understanding the impact of the batch size on the gradient descent optimization
        - [ ]  Implementing a random gaussian initialization
        - [ ]  Understanding the forward propagation in a convolution layer
        - [ ]  Understanding the signification of a gradient
        - [ ]  Understanding the role of padding in a convolution layer
        - [ ]  Evaluating the interpretability of an end-to-end learning system
        - [ ]  Understanding the keep probability in a Dropout layer
        - [ ]  Performing transfer learning
        - [ ]  Understanding vanishing gradients when using the sigmoid activation function
        - [ ]  Evaluating the advantages of fully-connected, CNN and RNN layers for a given application
        - [ ]  Understanding Neural Style Transfer
        - [ ]  Evaluating the computational cost of a RNN vs. CNN
        - [ ]  Backward propagating through a ReLU function
        - [ ]  Knowing when to use softmax vs. sigmoid
        - [ ]  Understanding the dimensions of the scale and shift parameters in Batch Normalization
        - [ ]  Choosing when to use a bi-directional vs. unidirectional RNN
        - [ ]  Applying gradient descent on pixels for image generation
        - [ ]  Calculating the number of parameters in a convolutional layer
    - AI Literacy
        - [ ]  Understanding what machine learning is
        - [ ]  Understanding the difference between General and Narrow AI
        - [ ]  Understanding the machine learning engineer role
        - [ ]  Understanding supervised learning
        - [x]  Differentiating between machine learning and rule-based systems
        - [ ]  Identifying what AI can and cannot do
        - [x]  Understanding precision
        - [ ]  Choosing summary statistics for a given type of data
        - [x]  Understanding false positives
        - [ ]  Understanding the steps in a machine learning project
        - [ ]  Understanding what a sensor is
        - [ ]  Understanding the role of humans in building machine learning systems
        - [ ]  Understanding the purpose of the test set
        - [ ]  Understanding how images are represented in computer vision
        - [ ]  Understanding word2vec
        - [ ]  Understanding reinforcement learning
        - [ ]  Identifying bias in AI systems
        - [ ]  Understanding the data engineering task
        - [ ]  Visually identifying a linear relationship between two variables
        - [ ]  Understanding the uses of the median
        - [ ]  Identifying the difference between a pipeline and an end-to-end system
        - [x]  Recognizing categorical data
        - [x]  Understanding the difference between ordinal and nominal categorical data
        - [ ]  Choosing the appropriate model for a given problem
        - [x]  Understanding what a neural network is
        - [x]  Understanding one-hot encoding
        - [x]  Understanding the data scientist role
        - [ ]  Identifying possible adverse uses of AI

---


# Misc

