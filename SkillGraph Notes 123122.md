### SkillGraph
# SkillGraph Notes 123122
created:: 2023-01-01 16:22
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/gnosis
kind:: #zettel 
status:: #status/seed
parent:: [[π SkillGraph]]
***

## External Resources
#### Philosophy
* The ontology should only encode actions, not theoretical knowledge. The point is to use our knowledge. Even if it is just communication about a topic. 
	* This brings up a difficult point -- if we allow people to claim expertise on any theoretical topic by showing that they have written about it, we will need to have the ability to represent every possible topic. In a sense, this makes us into another massive wiki. 
	* If we are a massive wiki, there needs to be an element of openness/crowd-sourcing. 
	* Entity resolution will be difficult. 
#### BackEnd
* The graph for an individual should be directed, but not necessarily a 1:many dendrogram, and perhaps not acyclical. 
	* We should allow a single node to have several parents.
	* We should allow skill branches to arbitrarily be attached to each other (i.e., I use PCA in the service of spike sorting for multicellular electrophysiology)
#### Ontology
* Skills should always be contextualized. What was the need? What was the outcome? 
	* There should be a graph of needs
		* For example, signal separation <-- multicellular electrophysiology <-- cortical electrophysiology <-- neurobiology
	* There should be a graph of outcomes. 
#### Software
* We need to develop a NLP library for identifying entities and contextualizing them in their fields. Core entities:
	* skills/techniques/actions
	* business needs
	* outcomes/artifacts/metrics
	* roles
	



### Resources: NLP skill entity extraction
##### Blogs, etc.
* [Extracting skills from job postings](https://support.prodi.gy/t/extracting-skills-from-job-postings/2017](https://support.prodi.gy/t/extracting-skills-from-job-postings/2017/10)
* [A Review of Named Entity Recognition (NER) Using Automatic Summarization of Resumes](https://towardsdatascience.com/a-review-of-named-entity-recognition-ner-using-automatic-summarization-of-resumes-5248a75de175)
* [A Beginner’s Introduction to NER (Named Entity Recognition)](https://www.analyticsvidhya.com/blog/2021/11/a-beginners-introduction-to-ner-named-entity-recognition/)
##### Articles
* [Occupational skills extraction with FinBERT](https://www.theseus.fi/bitstream/handle/10024/348657/Mariia_Chernova_Master_Thesis_full.pdf?sequence=2)
* [SkillNER: Mining and mapping soft skills from any text](https://arxiv.org/pdf/2101.11431.pdf)
* [A context-aware approach for extracting hard and soft skills](https://pdf.sciencedirectassets.com/280203/1-s2.0-S1877050921X00166/1-s2.0-S1877050921020573/main.pdf?X-Amz-Security-Token=IQoJb3JpZ2luX2VjEE0aCXVzLWVhc3QtMSJIMEYCIQDnkxk7Aojieczp%2FjvNTEa61ygj003qyT7LEEWRVTqpLQIhAJEQXGbBVzrF9bXSXGFDNiXiiQ%2BPOgpl047F9KguTl1wKtUECJb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQBRoMMDU5MDAzNTQ2ODY1Igx6pwLfchwpgJ%2B2h0gqqQT75P8YlRRtQi6JLKU6f9Wk0i%2F8BUzCNA0%2FeOQARoJg2lSVTgE70Yedr0FPp7XSGgIjgvQx8Tuc6TZgvF2HD4IKglaFJFxlHWS8jD6DSUiqXc%2BS3Zwfmc6AR9hl8DkkuIENbWGuar1SIOwU7bnSKIiwRfu9go1DiSIyQ35JY%2FdueMsFT0duEsH%2Bu2P7nokb1dkJbnevSJqgjvBQRehHaHptinYgsiZkpKMvPxV8G%2BFKTtxuH73eGPEbZFRvrqcuPIjATKxiD1x0WB%2F2hau%2Btnfi4qBHUuB8edDC6%2Fz3Tcp44wei1S0zys2rwyN274SMIO1C6s5CrDUvpO5A6yTp8i87O3wXgSrKwSM6Q%2BrF%2BFrCHLPwfOgxAnzLfXkRNB26I%2BUdb5UdLPoyhG33uYsIa3KI%2F5hsDa%2B%2FHwH4i%2B1dA2qgv%2FL1e7ryJEtbiHfgQ9ClkY%2BeQ40JrLhH6guEPcYCXMNApIQIX1SvD3H7990DbyPkyThcUvAg%2BGtkDSD%2BBVMNl%2Bn5kIpRfhDqhUlGndkY%2BU9WK71aV%2FBpiQQQm2S9Irkce69m43ClhBCCILKJZNUtVr1ASGp2aCoNBOp4zB5WZdH%2BdTeZk0SNnWqjE%2FhSAKy7y685%2FUeZ7kly%2Be5tRQdtKoXfW9%2Fm4slbW%2BVTXPDYq0It5Y2PPSvFuwcqY5uAIi1xDUqAeqf7j75INyFfsiq2jS7dsq9ZDWkbIc5uII2H%2BmbmdZ32cEST6FfCMK7Dwp0GOqgBzpzQBt600vbfIQN1CVC1Z80xWw6BI3Q3FNSGxv%2BCMHRpTEc9Asep8SY4UwGWrKpyEqxjvezWc1rmvW3vJioIdUF9pKBE8NwFUNNf5S0CytU%2Fxn02v5pRv%2BzZXmF5r%2BIgu9x6a%2FeizLdekwDd2gkLr5pTRfZrQSE%2BA1Ez5sjrUU0xLyYpng%2BJCw7uyjzmxfQu1SvLU34LLT82poxDg5rFHnyTZZZ0bh7W&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20221231T221738Z&X-Amz-SignedHeaders=host&X-Amz-Expires=300&X-Amz-Credential=ASIAQ3PHCVTY7L3H5OVC%2F20221231%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Signature=9cc78a21e2ec9e47c1807217e01a91305c099666153ab59ee3fce60beda91fdb&hash=b10bf67ee42ce8f8915083c8b111cf2389328de220dcd4dc05a40d11f5c45380&host=68042c943591013ac2b2430a89b270f6af2c76d8dfd086a07176afe7c76c2c61&pii=S1877050921020573&tid=spdf-f0b87a9b-7289-4c43-b5e0-52e8b375b63b&sid=7f2825171ed6a048b30adac6b1d7b564463agxrqa&type=client&ua=525f545554530a060e06&rr=782662efaad3e226)
* [SKILLSPAN: Hard and Soft Skill Extraction from English Job Postings](https://aclanthology.org/2022.naacl-main.366.pdf)
* [Semi-supervised deep learning based named entity recognition model to parse education section of resumes](https://link.springer.com/article/10.1007/s00521-020-05351-2)
* [Differential Hiring using a Combination of NER and Word Embedding](https://www.ijrte.org/wp-content/uploads/papers/v9i1/A2400059120.pdf)
* [SKILLBERT: "SKILLING" THE BERT TO CLASSIFY SKILLS!](https://openreview.net/pdf?id=TaUJl6Kt3rW)
* [Retrieving Skills from Job Descriptions: A Language Model Based Extreme Multi-label Classification Framework](https://animeshprasad.github.io/resources/c5.pdf)
* [Design of Negative Sampling Strategies for Distantly Supervised Skill Extraction](https://www.semanticscholar.org/reader/85b9aa7515ad6ef5314f349a75029bc0acd5dc43)
* [JoBERT: Understanding Job Titles through Skills](https://www.semanticscholar.org/reader/ec38ec96402dfe98a8e8c850eff476b5a3382637)
* [An Open and Data-driven Taxonomy of Skills Extracted from Online Job Adverts](https://www.semanticscholar.org/paper/An-Open-and-Data-driven-Taxonomy-of-Skills-from-Job-Djumalieva-Sleeman/54dcef5e2e7837424997aaf29d807121d88ab49f)
* [GraphLMI: A data driven system for exploring labor market information through graph databases](https://www.semanticscholar.org/paper/GraphLMI%3A-A-data-driven-system-for-exploring-labor-Giabelli-Malandri/ad4e3a5a86e8446dfba5aff4a59205c03770d5e4)
* [Skills2Graph: Processing million Job Ads to face the Job Skill Mismatch Problem](https://www.semanticscholar.org/paper/Skills2Graph%3A-Processing-million-Job-Ads-to-face-Giabelli-Malandri/5950391aa289c9c1638d352a8b8a6425e6ae3eca)
	* https://www.youtube.com/watch?v=Fiz9z_4FSbA
* [SKILL: A System for Skill Identification and Normalization](https://www.semanticscholar.org/paper/SKILL%3A-A-System-for-Skill-Identification-and-Zhao-Javed/bfd50521466808d022940fbcfe09e1835ae97822)
* [Is it Required? Ranking the Skills Required for a Job-Title](https://www.semanticscholar.org/paper/Is-it-Required-Ranking-the-Skills-Required-for-a-Anand-Decorte/71a230318a2241e1809c6d30963cc357081557c3)
* [Automatic job skill taxonomy generation for recruitment systems](https://pure.tue.nl/ws/portalfiles/portal/139505683/Final_PDFA_Dipika_Baad_Thesis.pdf)
* [HR-Specific NLP for the Homogeneous Classification of Declared and Inferred Skills](https://www.semanticscholar.org/paper/HR-Specific-NLP-for-the-Homogeneous-Classification-Celsi-Moreno/9a90620565009fda979240d97b6377e21599a88a)
* 


### ChatGPT session

> Create a hierarchical ontology of skills, limited to the field of statistics.

Here is a possible hierarchical ontology of skills in the field of statistics:

1.  Basic statistical concepts and techniques

-   Descriptive statistics
-   Probability
-   Normal distribution
-   Confidence intervals
-   Hypothesis testing

2.  Data preparation and management

-   Data cleaning
-   Data exploration
-   Data visualization
-   Data transformation

3.  Regression analysis

-   Simple linear regression
-   Multiple linear regression
-   Nonlinear regression
-   Multivariate regression

4.  Experimental design

-   Randomized controlled trials
-   Quasi-experiments
-   Factorial designs

5.  Multivariate statistics

-   Principal component analysis
-   Factor analysis
-   Cluster analysis
-   Multidimensional scaling

6.  Time series analysis

-   Autocorrelation
-   Stationarity
-   ARIMA modeling

7.  Machine learning

-   Supervised learning
-   Unsupervised learning
-   Reinforcement learning

8.  Advanced statistical methods

-   Survival analysis
-   Longitudinal data analysis
-   Meta-analysis
-   Bayesian statistics


> Alright, let's dig in to multivariate statistics. Can you expand the tree 2 levels down, starting with multivariate statistics as the root node?

Certainly! Here is a possible hierarchical ontology of skills in the field of multivariate statistics:

1.  Multivariate statistics

-   Principal component analysis
	-   Calculating principal components
	-   Interpreting principal components
	-   Choosing the number of components
	-   Using principal components for data reduction
-   Factor analysis
	-   Exploratory factor analysis
	-   Confirmatory factor analysis
	-   Choosing the number of factors
	-   Rotating factors
-   Cluster analysis
	-   Hierarchical clustering
	-   K-means clustering
	-   Density-based clustering
	-   Choosing the number of clusters
-   Multidimensional scaling
	-   Classical MDS
	-   Nonmetric MDS
	-   Choosing the number of dimensions
	-   Interpreting MDS results