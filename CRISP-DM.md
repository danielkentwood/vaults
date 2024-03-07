# CRISP-DM
CRISP-DM stands for Cross-Industry Standard Process for Data Mining

![[Pasted image 20220909124623.png|500]]

* Business understanding
	- Determining Business Objectives
		- Compiling the Business Background
		- Defining Business Objectives
		- Business Success Criteria
	- Assessing the Situation
		* Resource Inventory
		* Requirements, Assumptions, and Constraints
		* Risks and Contingencies
		* Terminology
		* Cost/Benefit Analysis
	- Determining Goals
		- Data goals
			- Describe the type of problem (e.g., clustering, prediction, or classification, etc)
			- Document technical goals using specific units of time, such as predictions with a three-month validity.
			- If possible, provide actual numbers for desired outcomes, such as producing churn scores for 80% of existing customers.
	* Producing a Project Plan
* Data understanding (EDA)
	* Potential predictors
	* The statistics of those predictors
	* Any relationships between those predictors
* Data preparation
	* Select data
	* Clean data
	* Construct data
		* One-hot encoding
		* Transformations
			* log
			* standardization 
				* min-max
				* z-score
	* Integrate data
	* Format data
* Modeling
	* [[model selection]]
	* Generate test design
	* Build model
	* [[model evaluation]]
* Evaluation
* Deployment
* Monitoring