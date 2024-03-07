# General structure
#### Initial Questions (5 Min)
- Tell me a bit about yourself.
- What interested you in this position? In healthcare? In CVS Health?
- What relevant experience do you have in healthcare? In analytics?
- What is your data science stack?
- _(If needed, find an easy question from resume to help ease nerves)_
- Feel free to ask specific questions about items on their resume in place of the below if you’d like/if it feels appropriate

#### Python/R Questions  (10 Min)

#### Problem Solving and Experiment Design (25 min)



# Philosophy

* When interviewing, you have two goals, in order of importance:
	* Find the strengths of the candidate; understand how they can strengthen the work being done. For entry-level, this requires having a healthy mapping between (a) demonstrated skills and adjacent experience, and (b) the experience required for the job.
	* Find the gaps in the candidate's skillset/experience. 

* Given the two primary goals, the ideal way to conduct the interview is to explore/exploit. Start with a wide and shallow search space. Dig in when you find either:
	* Something that stands out as a strength
	* Something that stands out as a red flag
* When you dig in, don't get stuck in a rabbit hole. Only dig just enough to confirm.
* If the candidate gets stuck, when should you rescue?
	* If related to problem solving, give them time.
	* If related to something they can *and would* google (e.g., implementation), step in if they spend more than a few moments on it. You can ask them what they would google if you need more insight.



# SQL

```sql
/*
Consider the tables below and answer the following questions

Note that mem1 and mem2 splits the entire membership data into 2 tables

mem1                                  mem2
+---------------+---------+           +---------------+---------+
| id            | int     |<----+---->| id            | int     |
| gender_cd     | varchar |     |     | gender_cd     | varchar |
| age_band      | varchar |     |     | age_band      | varchar |
| zip_cd        | varchar |     |     | zip_cd        | varchar |
+---------------+---------+     |     +---------------+---------+
                                |      
                                |  
                                |    clm
rsk                             |    +--------------------+---------+
+---------------+---------+     |    | claim_id           | int     |
| id            | int     |<----+--->| id                 | int     |
| srv_start_dt  | date    |          | srv_start_dt       | date    |
| retro_risk    | double  |          | paid_prvdr_par_cd  | varchar |
| prosp_risk    | double  |          | srv_spclty_ctg_cd  | varchar |
 +--------------+---------+          | cost_ctg_short_nm  | varchar |
                                     | paid_amt           | double  |
                                     | billed_amt         | double  |
                                     +--------------------+---------+


1. Get the top 3 cost categories by average amount billed in 2018.

2. Same as above, but remove any members within a given cost category who have had less than 2 claims (in that cost category) in 2018.
*/
with members as (
	select 
		id, 
		cost_ctg_short_nm, 
		count(distinct claim_id) as claims
	from clm
	where year(srv_start_dt) = '2018'
	group by id, cost_ctg_short_nm
)
select 
	clm.cost_ctg_short_nm, 
	avg(billed_amt) as avg_billed_amt
from clm
inner join members
	on members.id = clm.id
	and members.cost_ctg_short_nm = clm.cost_ctg_short_nm
where year(srv_start_dt) = '2018'
	and members.claims >= 2
group by cost_ctg_short_nm
order by 2 DESC
limit 3;
```


Q1: What is the % of members by gender? 
```sql
WITH t1 AS ( 
	SELECT gender_cd, COUNT(DISTINCT id) AS n 
	FROM ( 
		SELECT * FROM mem1    
		UNION   
		SELECT * FROM mem2 
	) a 
	GROUP BY gender_cd 
) 
SELECT gender_cd, n/total AS p 
FROM t1 
JOIN (
	SELECT SUM(n) AS total FROM t1
) t2 
	ON 1=1 
```


Q2: What is the % of members by age band? 
```sql
WITH t1 AS ( SELECT age_band, COUNT(DISTINCT id) AS n FROM  ( SELECT * FROM mem1    UNION   SELECT * FROM mem2 ) a GROUP BY age_band ) SELECT age_band, n/total AS p FROM  t1 JOIN (SELECT SUM(n) AS total FROM t1) t2 ON 1=1 
```


Q3: What is the % of paid amount by provider specialty for 2018? 
```sql
SELECT 
	srv_spclty_ctg_cd, 
	paid_amt/total AS p 
FROM (
	SELECT 
		srv_spclty_ctg_cd, 
		SUM(paid_amt) AS paid_amt         
	FROM clm         
	WHERE YEAR(srv_start_dt) = 2018         
	GROUP BY srv_spclty_ctg_cd ) t1 
	JOIN (  
		SELECT SUM(paid_amt) AS total 
		FROM clm            
		WHERE YEAR(srv_start_dt) = 2018 
	) t2 ON 1=1
```




# Python
#### 1. Palindromes
*writing functions and classes, dealing with strings*
1. Write a function that returns a boolean value indicating whether an input string is a palindrome
	1. if they haven't already, ask them to force the input to be a string and the output to be a boolean
2. Write another function that takes a palindrome and extends it by appending a second input string
	1. Use the first function to ensure that the first input string is actually a palindrome.
3. **If they say they are comfortable with OOP**: Write a class for handling palindromes, with the two above functions as methods
	1. Make it so that when the class is instantiated with a string, it automatically checks whether that string is a palindrome and prints a warning if not.

```python
class Palindrome:
    
    def __init__(self, string=''):
        self.string = string
        if string!='':
            if not is_palindrome(self.string):
                print('Input string is not a palindrome')
 
    def is_palindrome(self, string: str) -> bool:
        assert type(string)==str
        self.string = string
        str_rev = string==string[::-1]
        assert type(str_rev)==bool
        return str_rev

    def expand_palindrome(self, string: str, tag: str) -> bool:
        assert self.is_palindrome(string)
        str_exp = tag + string + tag[::-1]
        self.string = str_exp
        assert self.is_palindrome(str_exp)
        return str_exp
```

#### 2. Pandas
*Pandas I/O, groupby, crosstab, merge, loc vs iloc, adding columns*

```python
import pandas as pd
import numpy as np

test_dict = {'employee_id': pd.Series(range(1,7)), 'department': ['Parts', 'Parts', 'Parts', 'Autobody refinishing', 'Autobody refinishing', 'Autobody refinishing'], 
             'sales': [900, 450, 2100, 1875, 4025, 2017], 
             'hire_date': ['2021-01-01', '2012-02-01', '2019-03-01', '2019-04-01', '2020-01-15', '2020-06-08']}

## Generate pandas dataframe that shows all the employee records ordered by
## department and hire date
df = pd.DataFrame.from_dict(test_dict) 
df['hire_date'] = pd.to_datetime(df['hire_date']) 
df = df.sort_values(['department', 'hire_date'], ascending=[True, True]) 

## and includes 2 additional columns 
## (1) dep_sales - total sales in each department
df['dep_sales'] = df.groupby(‘department’)['sales'].transform(sum)
# or, alternatively:
df = df.merge(
		df.groupby('department')['sales']
			.sum()
			.reset_index(drop=False)
			.rename(columns={'sales': 'dep_sales'}),
		on = 'department'
)

## (2) cum_sales - a running total of the sales in each department ordered by employee hire date, with most tenured employee first
df['cum_sales'] = df.groupby('department')['sales'].cumsum() 

print(df)

```



#### 3. For the given points, how would you calculate the Euclidean distance in Python?
```python
plot1 = [1,3]
plot2 = [2,5]

euclidean_distance = sqrt( (plot1[0]-plot2[0])**2 + (plot1[1]-plot2[1])**2 )
```


#### MISC
- What are the advantages of Python for data science over other languages? What are the disadvantages?
- What is a generator? How is this different from a list?
- What is a comprehension?
- How do you add a simple and a complex field to a pandas dataframe?
- What is a transformer/transormermixin in python/SciKit and how is it used?

##### For R
- What are the advantages of R for data science over other languages? What are the disadvantages?
- How are lists indexed in R, and how is this different from other programming languages?
- How can you add a complex field to an R dataframe
- How do you transform the data type of a variable in a dataframe? (as.factor, as.numeric, etc) Why do you use as.[datatype]() instead of [datatype]() ?


# ML Questions

#### What is your favorite way to compare distributions?

#### bagging vs boosting
> [!question] What is the difference between bagging and boosting? 
> Good Answers: 
> * Both are considered ensembling techniques that involve combining multiple models in such a way that the final model is more performant and/or generalizable. 
> * Bagging, which is short for bootstrap aggregation, refers to a process where several "weak learners" are essentially weighted and averaged to give way to a more robust model. The learners are considered weak because they are only privy to a random sub-sample of observations and variables, hence the bootstrapped sample, to hedge against the likelihood of overfitting. 
> * Boosting, which is typically short for gradient boosting, refers to an iterative learning process where models are trained sequentially essentially correcting for what what wrong in the previous iteration by adjusting weights. 
> 
> Poor Answers:
> * One is a random forest and the other is a gradient boosted tree. 
> 
> Appropriate Interview Probes: 
> * Can you provide an example of a bagging/boosting algorithm (random forest & gradient boosted trees)? 
> * Which type of algorithm typically runs faster (bagging because it lends itself to parallelization)? - Which algorithm is more suited for combating bias (bagging)?
> * What is a downside to boosting (potential overfitting)?


### Feature engineering
You have 1000 features (numeric, categorical, text) in a model. How do you perform feature selection without spending a month doing it? 

Potential answers might include:
- Remove those with zero variation or excessive % missing values
- Alternating Conditional Expectations: non-linear correlation with the target, can eliminate those with lowest values
- Correlations among features: find redundancy & eliminate
- In later iterations: train model, run Permutation Importance, eliminate those with negative impact, and perhaps some lower impact. Can use this to find redundant features as well.
	- Warning: this depends on the info that the trained model was able to extract from each feature.
- Entropy analysis? – mutual information – measure independence


### Explain Cross-Validation
What is it? Why do we do it? Are there ever cases when we shouldn't use it? 

### How would you compare multiple classification models?
Looking for:
    
- Ensure they are evaluated on same out of sample data
- If trained together, ensure that they are trained on EXACTLY the same data partitions
- if accuracy is primary: logloss; if ranking: ROC AUC or Gini Norm
- Otherwise: optimize threshold of each using cost model (not optimized on same test dataset), then compare total profit


### How can you interpret ROC AUC?
- It’s a ranking metric, with no respect for calibration
- ROC AUC is the chance that the model will rank a positive example higher than a negative example (greater predicted value)
	- ROC AUC is the % of every pair of actual-negative and actual-positive examples in the dataset that are ranked in the correct order relative to each other
	- Usually calculated by iterating through many threshold values, and computing area under the generated stair-step plot
	- ROC AUC = (Gini Norm + 1)/2


### How do you optimize a threshold in a binary classification model?
-   What do you use F1-score for?
-   What is implicitly assumed in the F1-score?






# Conceptual
## Measurement strategy scenario
A stakeholder approaches you and tells you that their product has been running for 2 years, and they are getting good feedback from customers. They were recently asked to prove that the product is working, but they couldn't do it. They want to partner with you to prove that their product is working. 

The product is a plan benefit that emails eligible members to let them know that Aetna will cover the full cost of (1) a blood-glucose monitor, and (2) the drug Metformin. The purpose of the intervention is to reduce A1C values (i.e., a metric that reflects average blood sugar levels over the past 3 months).

For members to be eligible, they must meet the following conditions:
* type 2 diabetes 
* A1C value >= 7.5% within the last 6 months
* not currently taking Metformin
* their plan has the benefit

Please create an outline of how you would handle this request. 

-- end of prompt --

### Scenario details
#### Data available
* ~100K new members eligible for the product within a calendar year
* Available data
	* clinical: 
		* A1C values
		* medical claims data over the past 4 years
		* Intervention type and timing
	* engagement:
		* Email open rates
		* Email clickthrough rate (clicking brings them to a 3rd party website that we have no insight into)

#### Business context
* Constraints
	* We have been given a year to prove that it is working
	* We can do a holdout
	* We have enough money to run the campaign
* Conditions for success
	* After a year from now, we can confidently say whether or not our product reduces A1C values. And if so, by how much? 

#### Experimental context
* There has never been any holdout in the past
* Results from the original campaign:
	* Before the intervention, mean A1C was 8.1%
	* After the intervention, mean A1C was 7.9%
* In the literature, Metformin alone reduces A1C values by 1 - 1.5%

#### Model
They think they can make the product better if they have a way of predicting who is prediabetic (often people don't know that they are getting close to type 2 diabetes, i.e., prediabetes). Make a list (without going into too much detail) of steps to take, ending with deploying the model.


* how will you ensure that you don't overfit?
* which metrics will you choose to evaluate the performance of your model? Why? 









  














***
* Shadow Interview with Graeme
	* [[2022-07-12]]
## Several questions with single narrative
_Embed this into a template_

* **General**
	* Do they assume they understand the task without clarifying? 
* **SQL**
	* Get % of members by some category within a specific year (requires GROUP BY, CTE, WHERE filtering)
* **Python**
	* Pull the SQL table into a dataframe (it's okay to assume that we've exported the table into a csv, but if they know enough hive to export to csv, that would be awesome)
	* Do some operations on the dataframe




# Standards
We should make a Hiring focus group to improve the standards.

There are no clear standards that were communicated to me for the coding interview. What should a P3 be able to do vs a P2? There needs to be a clear standard so that we can be fair. The job req is not good enough.

Each interviewer should follow an approved template. 
If you don't like the templates that are provided, you can submit your own template for review. 

Template should have the following features:
* Suited to the role/level
	* identify which skills are necessary and which are "bonus"
	* for the skills that are necessary, identify specific benchmarks appropriate for the role/level
		* e.g., a P3 should be able to handle question "X" without any assistance.
* layered approach to skill assessment
	* start easy and fast, and move up
	* imagine if you could quickly provide the interviewee with 3 questions to solve (easy, medium, hard)




Send this out in advance of the interview
# Coding interview FAQ

### What should I expect?
* 5 minutes of intro chatting
* About 30 minutes of coding on Coderpad: SQL, python, and command line (bash and git) are fair game
* About 20 minutes of conceptual questions (maybe some coding here, too): experimental design, statistics, and ML topics
* 5 minutes of Q&A

### What if I can't remember the exact function/method/parameter?
* Bonus points if you've memorized Stack Overflow, but in most cases I honestly don't care. If you're stuck, you can either ask me or you can describe the logic of how it works. 

### How much should I talk?
* For coding questions, be an absolute blabbermouth while you solve the problems. Hearing how you think lets me move faster through the interview. But don't be offended if I interrupt you and move to the next question. We've got a lot to cover! 
* For conceptual questions, resist the temptation to tell me everything you know about a topic. Try to answer the question as concisely and clearly as possible. It's okay to take a second to think.

### How does my background influence what you are looking for?
* **Education:** 
	* *Not enough?* A degree is absolutely not required to be a good data scientist. But it does provide signal that you probably know how to learn, how to deliver assignments on time, and how to think carefully and deeply about a topic. If you don't have a degree, I'll probably be looking for cues about how curious you are, how deep your knowledge goes in the topics you've specialized in, etc.
	* *Too much?* The further you get into academia, the stronger the pressure to narrow the scope of what you are researching. This is good and important within academia because progress at the bleeding edge requires depth. But unless you are applying for a research scientist position, spending too much time on a very narrow topic can create habits that, to be honest, become a liability in most data scientist roles. If you have a PhD (even more if you spent time as a postdoc), I'll be looking for the following: 
		* you know how to curb your curiosity when necessary
		* when you don't know something, you don't hide it
		* you know how to 80/20 a problem
		* you can deliver on a tight schedule
		* you can talk about your work at a level that _anyone_ can understand
		* you can provide succint, high level answers despite having a firm grasp of all the details
	* *Different field?*



 
