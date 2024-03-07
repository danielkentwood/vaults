# Health Informatics Course Notes
created:: 2022-08-31 05:18
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/gnosis
kind:: #literature 
status:: #status/seed
annotation:: 
parent:: [[AI-DS-ML in Healthcare]]
***


# Notes on Outcomes and Interventions of Health Informatics course on Coursera

**Decision support:**

**The goal is to help people make better health decisions. Decision support is technology that helps an end user make a health decision. When creating the decision support, always keep in mind 3 things:**

- Who is making the decision?
- What is the decision?
- Match? (i.e., does the screen/prompt match the decision to be made?)

A Next Best Action (NBA) at Aetna is a form of decision support.

For example, an app that helps diabetics track blood glucose.

1. The patient is making the decisions (typically) based on the data/statistics reported by the app.
2. The decision is whether to change management behaviors (e.g., larger/smaller insulin boluses)
3. Match? Most apps don't give clear support for the decision to be made. Is "14% average below range" a prompt to do something in particular? Most patients need some other external form of decision support (e.g., input/interpretation from their doctor) before they can make a decision.

At Aetna, who are we typically providing decision support for when we create our models?

This is really about affordances and human factors. Warnings. Understanding how people make decisions.

Is there an ANSI analogue for health information? A set of standards for creating labels, hazard warnings, etc. Is it just the FDA?

My background/training is really quite optimal for "decision sciences". My work with affordances in my PhD. My human factors work with Exponent. I understand how people make decisions.

For example, warning fatigue and overwarning: in our disease models, we need to absolutely minimize the false negatives (i.e., the missed cases, the "never" events), but if we have too many false positives, clinicians will absolutely stop listening to the model.

**"The Five Rights" and "The Stack"**
![[Pasted image 20221030011953.png]]

When creating your models, you'll always be thinking about the following questions:

- Should you build the product or buy it?
- Does it work?
- Will it be used?
- Does it accomplish our goals?
- How do I build it?

**Should we make an intervention?**

ROI heuristic.

The clinical objective value score = (P+O+C+N+G) - (D+C)

P = patient impact

O = organizational impact

C = clinician impact

N = number of patients positively affected

G = gap between the ideal and actual behavior and outcomes pertinent to the objective

D = difficulty associated with addressing the objective

C = cost of addressing the objective

You can make a decision tree to formally compute the clinical objective value score.

**HIMMS Framework**

**Before you decide to do a decision support intervention**
![[Pasted image 20221030012016.png]]

HIMMS: Healthcare Information and Management Systems Society

![[Pasted image 20221030012040.png]]

If you can't articulate these pieces of your problem, you don't understand your problem.

**Does it work? Testing**

When you decide to use an intervention, you need to test whether it is effective. How is the decision support being used? Is it missing cases? Is it giving you false alarms?

Three ways of testing:

1. Doing it in the lab with some test cases.
2. Silently running it behind the scenes but in practice.
3. Putting it into practice.

If you have a case where you suspect that there are [[heterogeneous treatment effects]] (e.g., regional differences in the effect of a drug), and you need to gather data to test this hypothesis, you need to remember that you are always balancing (1) the need for the best data possible, and (2) the cost of collecting that data. You need to do a power analysis. You need to understand exactly how many data points you need in order to see the effect if it is there (or, rather, to show that it is not there if that is indeed the case).

[[Effect size]]: You need to have an estimate of effect size for each of the different treatment variables. How do you decide on an effect size when you have no reliable information yet? You can do an analysis that looks at how much of an effect size you would need the variable to have in order to meet some minimum ROI.

Effect size can be measured by correlation coefficient, but it is usually measured by [[Cohen's D]]:

![Health%20Informatics%20d04af901b7a8448f969926412de70c04/image.png](image.png)

In other words, the difference in means divided by the [[standard deviation]].

[[Statistical Power]]: While effect size is a measure of how much an independent variable makes a difference in some dependent variable, power is a measure of how effective a statistical test will be at discovering that difference.

[[Sample size]]: the number of samples you need in order to reach the required power for the statistical test, given a certain effect size.

In Python, you can use statsmodels to conduct a power analysis. For example, the function TTestIndPower is the power analysis for a t-test between two independent samples.

See the following for examples of power analysis in Python:

[https://towardsdatascience.com/introduction-to-power-analysis-in-python-e7b748dfa26](https://towardsdatascience.com/introduction-to-power-analysis-in-python-e7b748dfa26)

Trading off different types of errors.

Trading off false alarms (FP) versus missed cases (FN). This is where the real money is.

[[Sentinel event]] = an error in the output of the model that tells you that something is wrong with the model.

Often, when missed cases are the most catastrophic thing, the goal is to first minimize false negatives (i.e., maximize recall). After that, you try to reduce false positives (i.e., maximize precision) without increasing false negatives.

**Is it used? Does it accomplish goals?**

Workflow alignment = making sure the decision support arrives at the correct moment in the workflow when the decision is being made. Also making sure that no interruptions are occurring because of the decision support (e.g., info about a patient's drug allergies in a very different place in the drug order than the ordered drug itself)

Usability constraints: I-MeDeSA

(The Instrument for Evaluating Human Factors Principles in Medication-Related Decision Support Alerts)

[s12911-018-0666-y.pdf](s12911-018-0666-y.pdf)

Effectiveness?

So far, no evidence that clinical decision support improves patient outcomes. Where is the literature on this?

There is no data on whether clinical decision support is actually more cost-effective. Again, is this correct? Maybe the lack of data is just because businesses are hesitant to publish their business model?

There does appear to be an effect on improving practitioner performance.

Clinical decision support has an impact in only 2/3 of studies. And when they do have an effect, the effect is on the order of 10-20 percent.

Attributes that conferred successes:

- Automatic prompting to use the system
- Use of "home grown" systems
- Automatic provision of advice "pushed" into clinicians' routine workflow
- Automatic provision of clear recommendations

-=========

**DEFINING DECISION SUPPORT**

The Digital Doctor, a book that is worth checking out. Describes the difficulties associated with the transition to electronic medical records.

Another book: Clinical Decision Support: The Road to Broad Adoption, Dr. Greenness

Types of clinical decision support

- Calculators
- Logical conditions (if/then statements)
- Data aggregators (stats on some intervention over time?)
- Information retrieval tools (e.g., pubmed)
- Heuristic models (constructed as knowledge bases based on consensus within the field)
- Probabilistic models

When creating decision support, one should employ a "design thinking" process. It consists of 5 steps:

1. Empathize
2. Define
3. Ideate
4. Prototype
5. Test

This is not a linear workflow. It is iterative and circular.

**Design/Empathy phase**

Empathy is a big part of this. Put yourself into the place of the user. Visit them and see what the workflow is.

Take into account:

- Technology and Tools
    - Mobile, workstation, web-based, device oriented?
- The person who is using the CDS
    - Technologist, nurse, physician, resident, attending?
    - What is their technical proficiency? How frequently are they using it?
- The task that you are giving support for
    - Order tests, prescribe medications, perform procedure?
- Environment
    - Sterile operating room? Remote telemedicine setting?
- Organization
    - Academic medical center, rural private practice?

**Define Phase**

Book: Better EHR: Usability, workflow, and cognitive support in electronic health records by Jiajie Zhang.

[https://drive.google.com/open?id=1S0OZUNtXYlZLFmP43f40ygWEylwOXKdC](https://drive.google.com/open?id=1S0OZUNtXYlZLFmP43f40ygWEylwOXKdC)

TURF Framework:

- Tasks
- Users
- Representations
- Functions

The goal of the TURF framework is to translate something like electronic health records (which are complex and difficult) into something useful, satisfying, and usable.

When defining your decision support, always ask 3 questions: Is it in the system? Is it wanted by users? Is it actually used in activities?

**Ideate Phase**

After defining the decision support:

Cast a wide net for soliciting feedback

Literature review

Market analysis

Prioritization

It's useful to create a wireframe or paper-based mockup of the app/widget

**Prototype Phase**

Rapid Validation:

- Wireframe
    - skeletal framework of website
    - Limited use of color and design
    - Depicts page layout and arrangement
- Visual prototype
    - Simulates a few, key aspects of the website
    - Users can interact to simulate flow
    - generally includes near final rendering of look and feel

**Test Phase**

Example: does the tool change perceived control for a patient?

- Validated survey instruments
- Use a control group that didn't receive the decision support tool

**Deploy Phase**

After building a tool that has been validated and tested, you need to figure out how to get the tool into the workflow.

Typically, your tool is balanced somewhere between being built directly into the EMR, or being a 3rd party CDS application that usually draws (to some degree) information from the EMR.
![[Pasted image 20221030012151.png]]

The CDS tool and the EMR interact with each other at various points. A CDS tool can provide reports and other documents that are entered into the EMR. The EMR will have an information model for providing data to the CDS tool. Finally, the EMR needs a way of launching the CDS tool (i.e., facilitation of the CDS tool within the workflow of interacting with the EMR).
![[Pasted image 20221030012217.png]]
