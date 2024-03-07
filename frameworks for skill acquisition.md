created:: 2022-10-30 23:17
modified:: <%+ tp.file.last_modified_date() %>
mode:: #mode/gnosis 
kind:: #zettel 
status:: #status/raw
parent:: [[π SkillGraph]]

What does the acquisition of skill look like, and how can we validate it accurately and efficiently? 

# 1. Stages of skill

#### 1.1 The [Dreyfus model of skill acquisition](https://en.wikipedia.org/wiki/Dreyfus_model_of_skill_acquisition) 
| Cognitive Function | Novice | Advanced Beginner | Competence | Proficient | Expert |
| --: | --- | --- | --- | --- | --- |
| Recollection | Non-Situational | Situational | -----> | -----> | -----> |
| Recognition | Decomposed | -----> | Holistic | -----> | -----> |
| Decision | Analytical | -----> | -----> | Intuitive | -----> |
| Awareness | Monitoring | -----> | -----> | -----> | Absorbed |

* **Recollection**: A novice will be able to recite memorized definitions of concepts, but will not appropriately recall them situationally. It is very early on in skill acquisition that the individual begins to learn the situations in which a concept should be recalled. 
* **Recognition**: Beginners must engage in some level of decomposition in order to recognize a concept or technique. After progressing to competence, individuals can holistically recognize concepts, situations, etc.
* **Decision**: Intuitive decision-making within a particular skill domain only comes after developing proficiency. Prior to that, decision-making relies on explicit analysis. 
* **Awareness**: Prior to gaining expertise in a particular skill, one's awareness of the task is explicit and thematic due to the need to monitor for errors. These errors provide important feedback, so extra attention is devoted to catching them. A hallmark of expertise is an absorption into the task; this happens as errors become less frequent and less catastrophic, to the point where the benefits of absorption outweigh the benefits of error-monitoring.


# 2. Skill decay
Whether an individual has a skill at time $t$ will be a function of: 
* **Integration**: How integrated this skill is with other similar skills (i.e., contextualized learning decays more slowly)
* **Recency**: How much time has passed since the last validation of this skill? 
* **Execution cadence**: How often within a day/week/month was/is this skill used? 
* **Execution duration**: How long to execute the skill? Over what time frame does the skill play out? Some skills represent behaviors that play out over the course of days, while others play out over the course of minutes. 
* **Validation duration**: How much time between the first and last validation of this skill? 
* **Validation density**: What is the summed validation score (i.e., since validations differ in the quality of evidence, each has a different score) over the validation duration? 


# 3. Skill classification
Find a low-dimensional projection of all the skills, and cluster them into classes. What are some possible dimensions?
* **Time to acquisition**
* **Decay rate**
* How often do people have to look up the implementation (e.g., Stack Overflow) to remind themselves how to do it? To learn how to do it in the first place? 
* How long, on average, to reach different stages of skill?
* What is the average acquisition time frame (within a career) for a given skill? 
	* Another way of framing this question: on average, how early in their careers are candidates gaining this skill? How rapidly do they consider themselves experts? 
* How rapidly does the skill decay? 
* Which other skills most commonly co-occur in people with this skill? 
* How often does a particular role require the skill to be used? Some skills are used frequently, and others are used on rare occasions, depending on the role. Across the roles that use this skill, how often, on average, is this skill used? 


# 4. Value
How can we standardize a way of measuring the value (to a business) that the skill holder is able to create by using the skill? We need to be able to link the skill to artifacts (or at least claims about artifacts). For example, if I am skilled at predictive modeling, I can measure how much value I create with this skill by linking it with the business endpoints that were downstream causal effects of my models. *BONUS:* the more people link value to their skills, the more validation they get at the meta-skill of "Value-based thinking/decision-making"


# 5. Neuroscientific Foundation
A large part of my graduate and postdoctoral research focused on sensorimotor skill. The development of cognitive skill heavily overlaps. Distill the relevant work here. 
* Fast (cerebellar) and slow (motor cortex) learning. 
* Forward vs inverse models.
* Adaptation and consolidation.
* Chunking. 
* Symbolic/strategic/explicit vs. implicit.
* Reinforcement/reward vs. error gradients.
* Motor and cognitive maps.
* Explore/exploit