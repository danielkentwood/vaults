# π SkillGraph
created:: 2022-08-30 10:58
modified:: <%+ tp.file.last_modified_date() %>
mode:: #mode/management
kind:: #project/startup 
status:: #status/raw
parent:: [[∂ Startup Dashboard]]

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
### Meetings/Notes
```dataview
table created
from (#meeting and #mode/management) or (#zettel and #mode/gnosis)
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

### General
The more this develops, the more I think SkillGraph and arc.ai are the same idea. Or at least part of the same family.

### Alternative names
* umvelt.ai
* skillgraft.ai
* skillgraph.ai
* thearc.ai
* praxia.ai

### On resumes 
* Self-marketing: Some people don't sell themselves. Some people are experts at selling themselves. 
* Visual design: Some people are fantastic at designing. Some people are horrible at designing. 
* Communication: Some people are expert communicators. Some people struggle with communication. 
* Business sense: Some people are hopeless at connecting their work to the business side. Some people excel at this.

You'll often hear people argue that if someone puts together a poor resume, it is a signal that they might not be a good fit for the job. Of course, some jobs require applicants to have a subset of the skills above, but I would argue that most don't. Moreover, I would argue that resumes are not the optimal artifact for assessing those skills. But it is the artifact that we, as a culture, have agreed to use. 


### Minimal Team
After the core hypotheses have been confirmed and the MVP is validated, the launch team should be the smallest possible team that possesses the following skills (either as full-time or contract roles):

**Skill Ontology**
* NLP
	* [[Knowledge graphs]]
		* [[Named entity recognition (NER)]], entity disambiguation
		* [[Relation extraction]]
	* [[topic modeling]]
* Graph DB
	* Familiar with existing solutions or capable of building/maintaining custom solution
* Web scraping
* Computer Vision for extracting skill nodes from resumes

**Data Engineering**
* big data
* graphs
* large scale I/O
* API dev

**Data Visualization**
* custom large-scale interactive visualizations
* networks in javascript
* semantic zoom
* game design
	* we need to have a truly beautiful/engaging experience in the UI

**Sales/Marketing**
* branding
* market understanding
* website design
* customer acquisition/retention
	* SEO
	* site analytics/optimization/experimentation

**Legal**
* Privacy
* IP


### MVP
The MVP will consist of the following:
* No visualization necessary. Just code at this point.
* A subset of the ontology exists. The breadth doesn't need to be vast (maybe just a few very popular topics/fields), but the depth should be complete, from field/industry to implementation.
* There is a minimal API for querying the ontology, allowing you to add a node (or set of nodes) from the ontology to your skill tree.
* There is a minimal set of tools for validating the nodes on your skill tree.
* There is a minimal set of analytical tools for comparing and analyzing skill trees.


***
### Social Networking component
One of the most powerful retention techniques is to create social pressure to return. If we have a way of letting people create communities, it might help keep customers coming back. What is the simplest way to start this? Two ideas:
* **The Marketplace** 
	* This is where users can go to search for jobs (full time, contract, etc), employees, mentors, mentees, etc.
* **Neighborhoods**
	* Users can arbitrarily define a neighborhood by tagging all of the relevant skill nodes. 
	* The tagged skill nodes act as finding funnels. People looking for neighborhoods will get recommendations based on matches between the neighborhood skill nodes and their own skill tree (or desired skill tree). This will automatically pressure the neighborhoods to be stratified by skill level. You'll be grouped with people who are relatively close to you on their journey. 
	* Owners can define the requirements for joining a neighborhood
	* Neighborhoods will have social tools (chat/messaging/etc) and tools for gamifying/boosting progress on a particular topic. These are almost like a mix between study groups and MMORPG raid parties. 

***
### Information aggregation component
A lot of the ideas in this platform are based on aggregating lots of information from the internet and curating or standardizing it. 

Resist the urge to create a new search engine. The scope must be limited. This platform is focused on providing resources for building skill. For that to happen, we want to feed people the best resources. Find out how to automate the discovery of the best resources for every node. 

***
### Personalization
Each node in a user's tree is also a markdown document! 
* There is a standardized section of the document that contains metadata, learning resources, etc. There is also a personal section that allows the user to take their own notes.
* Users can make their own arbitrary nodes and links between nodes in the tree, but they will exist on a side tree, to distinguish them from the standardized tree. 
* Users can populate their tree with any node, even ones that they don't have any skill in, allowing them to start taking notes and learning about a new skill. The validation layer is what determines the actual skill tree that a user possesses. 

***


# Old Notes

The hiring process is rife with inefficiency and bias. While some marketplace solutions (e.g., LinkedIn) provide recommendations to job seekers and employers, these recommendations are built on impoverished underlying data. We need to have tools for augmenting and refining the data that would provide a better signal about the match between a company and a candidate.

Ok Cupid style questions to learn about culture, preferences, etc. this would allow us to get a culture profile for companies, teams, etc

What does SkillFlow do?

- It helps employers. How?
    - Companies waste resources on job descriptions that are inaccurate and unrealistic. We can automate and empirically validate many parts of the job description.
    - Fewer resources spent on recruiters: In the same way that real-estate agents are increasingly become obsolete due to real-estate startups that automate many of the tasks that agents perform, we would automate many of the functions that recruiters currently perform.
    - Once we have enough of the market, we also provide probabilistic estimates regarding things like:
        - the match between the job description and the candidate
        - how much (and exactly what kind) of experience the role requires
        - the cultural match between the team and the candidate (tricky but also a fun problem to try and solve)
    - We provide tools/platform for evaluating the candidate during and after interviews (and incentives for using those tools). **Examples of tools:** sandbox for coding challenges, de-biasing tools, recommended questions/prompts/answers, evaluation forms, etc. **Examples of incentives**: if they use our tools they improve our understanding of what they’re looking for and therefore they get better matches in the future, actual financial incentives to the company (so HR pressures teams to use the tools).
- It helps job seekers. How?
    - 
- The platform would automate “tests” corresponding to the SkillFlows that a company uses (when such tests are amenable to automation, at least). Job seekers can get a sense for how good they are at these tasks, and can choose to attach their work to their profile. This would provide companies with a high-quality signal regarding potential applicants. *In other words, both the job seeker and the company get higher-quality information about each other, thus reducing false positives (people applying who aren’t ready) and false negatives (people who don’t apply because they falsely believe they aren’t ready).*

Another thought: We could provide analytics to companies regarding the market for the roles they are advertising. What is the supply of candidates that are truly matched to the role? What is the supply of roles like this one? Where does my company rank in terms of compensation offered for this role? What is the likelihood that I will be able to retain people in this role? Are people leaving their roles to find better opportunities? Should companies be working harder to retain? 

For another potential function of this app/platform, see also [[π Data Science Ecosystem]]


# Why is this necessary?

**Resumés are a mess**

Resumes are the fundamental unit of currency in hiring and self-marketing. Given this fact, it should be clear and simple to understand what companies want and therefore how to write a good resume that effectively markets your skills and experience. But when it comes time to write a resume, you run into some problems:

- You get conflicting advice.
- You get bad advice (and you probably don't realize it).
- Nobody is clearly telling you what resume parsers can and cannot handle.
- For many reasons, it's hard to talk about your skills. Should you try to rate skill level? How does your skill level compare to other applicants' skill levels? How much detail should you include? How should you group them? How are companies even supposed to verify that you actually have these skills (can they adequately cover all of them and more in a day of interviews)?
- Are you experienced enough to have a multi-paged resume? Or should you fit everything into one page and leave out critical information?
- Should I build my resume from scratch or should I use a template? Which one will take longer?
- Which version of my resume is this? Is this the most recent one? There are a few services out there that solve the version control problem for resumes (for example, Overleaf, if you happen to know LaTeX and have the upgraded account), but I doubt most people use them.

To my knowledge, no service currently exists to address this friction. Nobody has successfully captured the market on resume writing. I see little to no innovation here.

LinkedIn arguably has the largest share of this market today, but the LinkedIn profile pages are pseudo-resumes. They try to be resumes but they do a poor job of it. Perhaps this is because LinkedIn is a social network first and foremost. Their profile pages are sufficient for self-marketing, but they standardize in ways that feel clunky and haphazard, almost as if they haven't tried to optimize anything yet. They funnel everyone into a self-marketing schema that has a stretched out UI with unnecessary integration of the social media feed, a very limiting interface for listing skills and accomplishments, an odd section for endorsements, and very little ability to adapt to field-specific needs and practices (e.g., ordering of sections, emphasis or de-emphasis of publications, etc.). Nobody has stepped in to fill this niche. Proof? If someone had, people wouldn't still be submitting pdfs for resumes, and companies probably wouldn't need to create their own webforms for applications (which just creates an extra, annoying barrier for applications). 

**This Hurts Companies**

The lack of standardization makes life difficult for companies who need to parse hundreds to thousands of applications for their job searches. And the lack of innovation around resumes has led all of us to accept the limited number of trustworthy signals that a resume can carry; the rest we have to leave up to the noisy process of interviews. As a result, they often attach their own information gathering tools to their application framework.

**This Hurts Applicants**

This market gap also leads to a very difficult time for job applicants; how many articles and talks have been created about "how to create a good resume"? Far too many. Even worse, so much advice on how to write a good resume is not informed by data; it comes from the anecdotes of people who have been hired or who have hired other people, and they are just telling you what they've seen working. To my knowledge, there isn't a service that exists that can gather causal data on what works in a resume and what doesn't (and then teach applicants about what works as they create their resume). Furthermore, as companies try to gather information that should be available within a resume (but usually isn't), applicants are forced to waste their time entering the same information into dozens of different webforms during the application process. 

**How could this be different?** 

What if there was a website that solved these problems in such a way that made pdf-based resumes obsolete? 

# What is a SkillFlow?

The central unit that ties everything together is the ***SkillBlock*** — an object that contains a hierarchy of information about a skill. For example, starting the top level and moving down, one possible SkillBlock could be model development —> hyperparameter optimization —> grid search —> GridSearchCV() from scikit-learn. The SkillBlock hierarchy can be an arbitrary depth, depending on the complexity of the skill tree in question.

Users will be able to chain together multiple SkillBlocks into a ***SkillFlow*** — a directed graph of SkillBlocks, describing a unique workflow.

Individuals and companies may want to utilize the SkillFlow tech without having to tether themselves to the SkillFlow platform. So there will be an API as well as shareable/embeddable SkillFlow graphics and links.

### Competitors?

Ultimately, SkillFlow will be a competitor with LinkedIn (e.g., see here for LinkedIn's efforts to move in this direction: [https://engineering.linkedin.com/blog/2016/10/building-the-linkedin-knowledge-graph](https://engineering.linkedin.com/blog/2016/10/building-the-linkedin-knowledge-graph)), but it will be limited to tech jobs. At least at first. 

Another competitor is stackshare.io. But stackshare appears to have limited buy-in because the only value proposition is to share the tech stack. SkillFlow would share the tech stack by default, but it wouldn't be the primary value proposition.

Include list of things that I need to verify if its going to go forward. 

What is the added benefit/cost of each of the components?

What are the hypotheses I need to test? How much do I need to pay to test each hypothesis? 

## What is the business model?

Freemium subscription model with tiered access to different functions and products. 

## What problems does this solve?

- **JOB TITLES**:
    
    The SkillFlow concept can help make progress on the problem of job titles in data science (and other fields that suffer from similar ambiguities). People want to be a data scientist because it is sexy, and companies think they need a data scientist, so the company puts out an ad for a data scientist and hires the applicant. And then the applicant finds out that the company wants them to focus primarily on SQL wrangling or something else that they didn't expect. Nobody is happy. With SkillFlow, companies will be able to effectively manage expectations about the jobs they are advertising. As the SkillFlow concept gains traction, we will learn about the distributions of SkillFlows that exist in individuals and in companies, providing us with a data-driven, unsupervised approach to classifying unique roles. This will help the field mature. 
    
- **SKILL VERIFICATION**:
    
    For individuals, every skill in the skillblock or skillflow *should* be linked to a concrete item:
    
    - Code written in a project.
    - A written description of a project.
    - Online assessments.
    - A past role
    - etc.
    
    There will be different levels of verification attached (as tags) to each skill. There will be verification by code, by endorsement of someone who observed the skill, verification by their company validating the SkillFlow as one that the company uses, etc. When you go to someone's page and click on a specific skill in a SkillBlock, a new window appears (maybe a new page, a pop-up, or a side-window) and displays all of the validators for that particular skill. People can create SkillBlocks without linking the skills to any validators, but they will be tagged as such. The website will nudge the user and teach them how to link to validators (and why it is important to do so). 
    
- **TIME COMMITMENT**:
    
    Especially as people become more senior in their career, they may have too much experience to list, and they probably don't want to spend hours creating SkillBlocks that describe each project they've been involved in. There are two innovations that will address this:
    
    1. *Code —> SkillFlow Model*: If people link to a public github project, we can train a classifier to go through their code and recognize the skills that were used, and suggest a SkillFlow. As people (1) build their SkillFlows from scratch and link them to their project, and/or (2) edit their SkillFlows that are suggested from the algorithm, the model will continue to train itself on this new information, and will continually get better. 
    2. *SkillFlow Recommender System*: If someone on their team builds a SkillFlow (and tags them on the project, for example), they will get an alert or a nudge asking if they want to add this SkillFlow. Also, as they write descriptions of projects, they will get recommendations from a model that has been trained to extract SkillFlows from natural language. Finally, there will be a recommender system that simply looks at which skills they have and tries to infer any gaps (i.e., any skills they neglected to mention) based on other user profiles (collaborative filtering) and based on proximity to other skills in the knowledge graph (content based-filtering). 
    3. ***Gamification?*** A third possible innovation would be gamification. Badges, skill trees, ranks, etc. These would probably be private (since introducing these platform-wide might introduce a level of competition that would repel a lot of people). But the goal would be to create an interface that is fun to use and that leverages the same human psychological impulses and biases that make RPG games so immersive and enjoyable (e.g., stochastic rewards, visible evidence of growth and progress, the development of an avatar that partially satisfies fundamental self-actualization needs). Not sure how this would be implemented, but I'm thinking it could dovetail with the "job titles" issue — i.e., as we gain more insight into the naturally clustering skill profiles that emerge in the distribution, we can create "pathways". 

---

### Sub-Project 1: Data Science Topic Modeling and Knowledge Graph

To build the SkillBlock, I need to develop a hierarchical knowledge graph of data science skills (start with DS and then branch out to other tech industries). 

### Sub-Project 2: Write code for SkillBlocks and SkillFlows

Write code that indexes the DS knowledge graph in order to build SkillBlocks.

### Sub-Project 3: SkillFlow model trained on GitHub code

The model will go into a GitHub repository and extract all of the SkillBlocks, and then assemble them into a SkillFlow. The user will have the option to modify/correct the SkillFlow (which will provide feedback to the model). 

---

---

**Roadmap**

1. **STAGE 1: SkillFlow UI for individual users**
    1. MVP is two main pages
        1. SkillFlow construction page: 
            1. You build SkillBlocks by navigating the Skill Tree of your chosen field, zooming into the skill area, and then clicking the nodes of the tree until you've reached your desired depth for that SkillBlock. When you complete the SkillBlock, it appears in the SkillFlow canvas near the bottom of the screen.
            2. You build the SkillFlows by linking SkillBlocks together in a drag-and-drop chain-building interface. You can start with templates of common skillflows. 
        2. Profile page for user
    2. Branding, outreach, ads
    3. Value proposition: 
        1. Users get a SkillFlow graphic they can embed in their resume (that shows their skills and how they connect to each other)
        2. They can link to their profile page, which will provide more detailed information about their skills and how they use them.
        3. They can link to projects on their profile, showcasing their skills. The website will drive traffic to their projects. 
        4. They get access to other user's projects in order to upskill and see how others have used a particular skill in actual code. 
    4. Skill verification: at first, this will be tied primarily to projects. The user will be nudged to connect a skillflow to a project so that anyone who wants to verify can go to the project and see the skills in action.
2. **STAGE 2: SkillFlow UI for companies**
    1. Companies get their own profile pages
    2. Specific roles are listed, each with associated SkillFlow(s). 
    3. This is initially bootstrapped from users listing their companies, roles, and the associated SkillFlow(s)
    4. Companies can curate (reject, promote, suggest edits to) the SkillFlows that their employees have linked to the company. They are free to control how much information they reveal about their SkillFlows, so they can balance intellectual property considerations with marketing effectiveness. 
    5. **Skill verification:** Users can see company workflows and companies can see their employee's workflows. Dishonesty about skills will look bad. Anonymous reviews will allow previous and current employees to confirm or provide critique of company workflows. 
    6. Value proposition:
        1. Companies can learn about the SkillFlows of similar companies in order to improve their own practices. 
        2. Companies can more effectively market and brand themselves and their open roles, and they can onboard new employees with the SkillFlows associated with the new role.

---

**Functions and services**:

- **Flow Search:**
    - Topical:
        - Example: If you're interested in NLP, you search for it, and it will provide three categories of results:
            1. USER FLOWS: Most common NLP SkillFlows from users.
            2. COMPANY FLOWS: Specific NLP SkillFlows from companies.
            3. PROJECT FLOWS: User projects that have NLP-related SkillFlows. (education function)
    - Skill-based:
        - You search a specific SkillBlock or SkillFlow, and it returns:
            - Companies with job ads that require that Skill*
            - Companies with job roles (but not necessarily hiring) that use that Skill*
            - User projects that involve that Skill*
- **Hiring tools:**
    - SkillFlow Company API:
        - This divorces the front end from the back end, allowing users to format and decorate their profile pages however they desire, without affecting the underlying information accessible to companies.
        - A company using the direct apply function can request whatever information they want, in various levels of specificity.
    - Direct apply:
        - candidates can apply to your job ad directly on the SkillFlow website with a single click. Only the relevant info (selected with the API) is harvested from the applicant's profile.
        - dashboard for companies to view metrics for each job posting, including arbitrary scores that the company can assign to every applicant based on various features.
        - Ethics Tools: a company can choose to scrub the applicant's info of any demographic information that might bias the initial selection stages.
    - Redirect apply (legacy system):
        - candidates are redirected to your own website's application webform.
        - candidates can export a PDF of their SkillFlow profile to submit to your website.
        - you don't get the benefits of the API unless your developers build them into your website's forms.

---

# WEBSITE FRAMEWORK

## Front End

- Profile pages
    - User profile page
        - Role
            - SkillFlow
        - Project
            - SkillFlow
    - Company profile page
        - Role
            - SkillFlow
        - Employees
        - Jobs available

## Back End


# More thoughts on platform layers

* Ontology: This defines the types of entities and the types of relationships that can exist between them. It also defines what consitutes a skill in the context of the graph.
* Base graph: this is the implementation of the knowledge graph, containing all of the entities and the hierarchical relationships between them.
* Skill layer: Skills are atomic subgraphs composed of specific types of nodes in a specific order. They are compositional; this compositionality cannot be derived in most cases -- it must be empirically measured. 
* Skill level layer: 
	* assignment of level-type features to a skill type
		* operationalization of the skill in terms of dreyfus model (i.e., what does each stage/level look like for each cognitive function?)
		* statistics on skill acquisition and decay
		* etc.
	* classification of skill level for a user
		* uses validation layer to classify a user's current skill level
* Validation layer
	* validation should be a weighted graph metric, like degree. It is a function of:
		* the size of the graph (relative to a distribution of similar graphs)
		* the weight (a priori or empirical) of the "evidence" nodes attached to the graph.
	* evidence nodes: 
		* input types: 
			* courses
			* certifications
			* memberships
			* degrees
		* output types:
			* non-public acheivements (description attached to a company or a lab)
			* influence on others (testimonial from a co-worker)
			* public acheivements (publications, grants, artwork, etc.)

# Use cases!
#### Career progression/planning
As you build out your graph, you'll be prompted to get more specific. This will help you quantify your accomplishments in concrete ways. And this, in turn, will help you (1) clarify how your accomplishments measure up to your goals, and (2) argue more persuasively for promotion/raise. 
- You can directly compare yourself to a subset of the users and get relativistic performance metrics. 
- You can output a boilerplate year-end or mid-year review package. 

Ensure that people who use your platform have a massive edge! 

#### Career switching
Your skill graph will provide a mathematical answer to the question: "What other fields am I qualified to enter?" Indeed, based on your skill graph, you may find a field that you are more qualified for than your current field. 

#### Learning guide
What should I learn next? If I want to learn X, what should I learn before it? What are others in my field learning right now (i.e., what is the new, hottest thing)?

#### Job search
Mathematically optimized matching between open roles and candidates. 

#### Knowledge management
SkillGraft provides the base layer knowledge graph, but users have the freedom to connect nodes however they want with wiki-style links. For the user, each node is a markdown document.

#### Community
There will be a social graph. 

# Ontology

1. Entities:
	- Discipline: Broad subject areas within data science (e.g., Machine Learning, Data Analytics, Statistics, Bayesian Inference).
		- Properties: name, description
	- Method: Specific techniques or approaches used in data science, including algorithms and frameworks (e.g., Linear Regression, Cluster Analysis, Data Structure, Theorem).
		- Properties: name, description, category (algorithm or framework)
	- Activity: Tasks or processes performed in data science (e.g., Data Wrangling, Exploratory Data Analysis, prediction, optimization, recommendation, etc.).
		- Properties: name, description
	- Tool: Instruments or technologies used in data science, including coding languages, platforms, and libraries.
		- Properties: name, description, category (coding_language, platform, library), release_date
	- Resource: Educational or reference materials related to data science (e.g., online courses, books, tutorials, blog posts).
		- Properties: name, description, format (e.g., video, text), author, URL
	- Validation: Evidence of proficiency.
		- Properties: name, description, category (certification, competency, degree, artifact, acheivement, testimonial)
	- Role: Represents a specific job title or function in the data science field (e.g., Data Scientist, Data Analyst, Machine Learning Engineer).
		- Properties: name, description
	- Industry: Represents an industry or sector where data science skills are applicable (e.g., Finance, Healthcare, Retail, Technology).
		- Properties: name, description
	- Data: Represents a type of data (e.g., stock prices, temperatures, A1C scores, timestamps, etc.)
		- Properties: name, description, type (nominal, ordinal, binary, continuous)
2. Relationships:
	- "superclass_of": Denotes a hierarchical relationship between methods, pointing from the parent to the child.
	- "has_instance": Indicates that a discipline, method, or activity is an example or instance of a more general concept.
	- "uses": Describes the utilization of a tool, method, or algorithm in the context of an activity or discipline.
	- "is covered in": Connects a skill, method, or discipline to a resource that provides relevant information or instruction.
	- "for": Denotes the motivation/goal of an activity.
	- "of": Connects an activity and a data type or another activity (e.g., "optimization", "of", "medical coding")

Skill is a concept that refers to a human ability. There is no activity that is inherently a skill, but a human can develop skill in any activity. Also, skills should always be contextualized. Thus, rather than represent skill as a type of entity in the ontology, skill will be represented in two ways: (1) as a user-specific subgraph, and (2) as a graph-based metric. 
1. A user can pick out a skill by connecting nodes to construct an imperative mood, bare infinitive clause. For example: "multi-armed bandit"---for--->"optimization"---of--->"email subject lines". 
2. As users build more skill subgraphs, certain nodes will be represented more than others. The frequency that a node is included in the user's skill subgraphs will determine a score representing the user's skill.


## Next up on graph editor
- For link creation mode, have the edge line follow the cursor around (anchored at the original node) until it is connected to the target node.
- Create a pruning mode: anything you click on is deleted.
- Implement the editing logic for node and link properties to allow users to modify properties like labels, colors, or weights.
- Add functionality to remove links from the graph.
- Display edge type (at specific zoom and/or when hovered)
- Color node by entity type
- Add controls for modifying graph (force magnitude, edge length, component colors, etc.)


