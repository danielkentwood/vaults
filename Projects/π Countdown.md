# π Countdown
created:: 2022-08-31 05:16
modified:: <%+ tp.file.last_modified_date() %>
mode:: #mode/management
kind:: #project 
status:: #status/dormant
parent:: [[∂ Personal Project Dashboard]]

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




# Project Workspace:

- Do a survival analysis
    - [https://towardsdatascience.com/deep-learning-for-survival-analysis-fdd1505293c9](https://towardsdatascience.com/deep-learning-for-survival-analysis-fdd1505293c9)
- Develop a bayesian approach for integrating scientific findings into the distributions.
- Learn d3.js and create a cool interface

We have a distribution P(x) - probability of death as a function of age. Let s be smokers and ns be nonsmokers.

P(x)=P(x|s)P(s)+P(x|ns)P(ns)

E[x|s]-E[x|ns]=10, where E is the expectation (mean).

You could come up with an infinite number of slightly different distributions that could follow the above equations. Therefore you will need additional assumptions about how the distributions of P(x|s) and P(x|ns) differ (the shifts you were referring to).

One potential way to go about solving this would be to think about it from an optimization standpoint, where you're trying to find the values in many bins of the histogram you're trying to solve for. And you would tie in assumptions about how the bins of P(x|s) and P(x|ns) differ, along with smoothness of the bins. Another potential way would be assuming some class of distribution for P(x|s) and P(x|ns), and try to fit for parameters that give them the correct properties.

we use the difference between E for the P(x|s) and P(x|ns) distributions--i.e., a difference value that we pulled from the literature, say--and now we have the inverse problem of figuring out what the individual E values were, as well as which distributions of P(x|s) and P(x|ns) gave rise to their respective E values

NOTES:

- What are all the sources of data available?
- How do I combine HBER mortality data with medical studies about the impact of certain habits, genetics, etc.?
    - combine main distribution with "shift" distribution.
        - age-weight the shift distribution by combining distributions of all the different causes of death related to the reason for the shift.
- **Financial planning:**
    - How much do I have to save if I want to retire at a certain age?
    - How does geography and cost of living impact that?
- **Therapist:**
    - You can choose your own style of therapy.
    - A bot talks to you and helps you through your issues
    - It uses common batteries and questionnaires to diagnose according to the DSM.
    - It teaches meditation/mindfulness techniques.
- Being reminded of your impending death can be difficult for some people. Have tools to help them frame this in a positive/constructive way.
- A great deal of this app will be about presenting data in beautiful/interesting/helpful ways.
- **Experiences:**
    - Instead of measuring the time they have left in terms of years/months/days/minutes, measure it in terms of experiences. See [https://waitbutwhy.com/2015/12/the-tail-end.html](https://waitbutwhy.com/2015/12/the-tail-end.html)
    - Examples:
        - How many times will I likely see my parents before they die or before I die?
        - How many times will I get to engage in a particular activity with my children before they are grown up?
        - How long will it take me to switch careers and is it worth it given the amount of time I have left?
        - If I visit one country per year until I die, how much of the world will I get to see?
        - How many more books will you read?
        - When I start a new career, what will it do to the rest of my life in terms of experiences? Does it reduce the number of experiences in other areas because I'm too busy?
        - 

**Countdown**

An app that takes personal information about demographics and health habits, and produces a distribution of likely death days and causes. It takes the median of this distribution and counts down in hours, days, weeks, months, and/or years.

**Why is it important?**

If someone handed you an envelope containing a letter informing of the day you would die, would you open it? Why would someone want to know how long they have left to live? Death is a nearly universal source of fear and anxiety. Confronting the reality of your mortality can lead to greater clarity about your hopes, your goals, and the meaning of your life. We'll sometimes go for years without thinking about this, only to be caught by surprise at how quickly time is passing, and how little of it we have left. Compounding this problem is the lack of information about when our death is likely to happen. What if we could narrow the window and get a more accurate guess about when we are likely to die? What could we do with that information? Could we work on changing our life to push that number farther back (e.g., stopping smoking, drinking less, exercising more frequently)? Could we find the motivation to rid our lives of things that don't contribute to our most important goals and hopes?

**How does it work?**

To inform the predictions that Countdown makes about a single individual's possible death date, I will train a model that takes into account a broad array of predictors that potentially influence life expectancy. Some early predictors of the model might be things like daily health habits (e.g., cardiovascular exercise, sleep, caloric consumption, etc) and demographics (e.g., race, education, economic bracket, geographical location, etc). Later, it might be possible to add information about genetic risk factors through peer-reviewed studies, genealogical data, etc.

Early on, the choice of model will be less important. We can work on honing the model as time goes by.

- It could be a logistic regression for each day (i.e., given the following predictor values, what are the odds of dying at this exact age? etc.)
- It could spit out a probability function given a set of predictor values.
- Bayesian modeling: combining multiple distributions from disparate sources. From a demographics-based model, from published results of health studies, etc.

**Design Ideas**

Don't over-engineer the prediction side of things. It can't be perfect, and it won't be accurate at the individual level. It just needs to be believable. The more believable sources you can use to inform the prediction, the more believable the prediction will be.

* At first, it gives you a countdown in the form of a number (which can be expressed in seconds, minutes, hours, days, weeks, months, years). If you click on it, it takes you to a new page with a bunch of graphics that creatively compare the time left with the amount of time you've already lived. The amount of experiences you've had with the amount you have left to experience. Things that tie back to the person's motivations. If you click in deeper, it takes you to a timeline that shows you the distribution of likely death days. If you click on that distribution further, that distribution gets decomposed into all of the component distributions, which will display the research or data used to create it if you hover over it. Also, the distribution page will have a series of sliders so that you can see what happens to the distribution if you change certain behaviors like smoking, drinking, sleeping, sitting, etc.

**Roadmap**

Start off as a standalone website.

Develop it into an iOS app that can be integrated with other health and time management apps. Users of these apps can get summary data on the app, and can be redirected to the website for more detailed information.

Market it to the school of life or some other philosophically oriented movement?

**HOW TO**

Use Selenium to automate the process of scraping: [http://www.eyalfrank.com/scraping-web-forms-with-selenium/](http://www.eyalfrank.com/scraping-web-forms-with-selenium/)

Combine probability distributions to get a single distribution?

If the probability distribution represents years increased or decreased (e.g., smoking gives you 2 years less to live), how do I combine that with a distribution in terms of life expectancy (e.g., you will die at age 72)?

**Starting out, just focus on a few datasets.**

Public health data

Cardio exercise

Sleep

Smoking

Time sitting

Occupation [https://www.cdc.gov/niosh/topics/noms/query.html](https://www.cdc.gov/niosh/topics/noms/query.html)

for uploading the youtube video:

[https://www.makeuseof.com/tag/reduce-video-file-size-without-sacrificing-quality/](https://www.makeuseof.com/tag/reduce-video-file-size-without-sacrificing-quality/)

Article about a few existing death clocks:

[http://www.cbc.ca/firsthand/m_features/death-clocks-science](http://www.cbc.ca/firsthand/m_features/death-clocks-science)

[https://flowingdata.com/2015/09/23/years-you-have-left-to-live-probably/](https://flowingdata.com/2015/09/23/years-you-have-left-to-live-probably/)

see also: [https://flowingdata.com/tag/life-expectancy/](https://flowingdata.com/tag/life-expectancy/) for ideas on visualizations

**Data Sources:**

- CDC NVSS. Public health data.
    - [https://wonder.cdc.gov/](https://wonder.cdc.gov/)
- Archived CDC mortality datasets:
    - [http://www.nber.org/data/vital-statistics-mortality-data-multiple-cause-of-death.html](http://www.nber.org/data/vital-statistics-mortality-data-multiple-cause-of-death.html)
- Smoking:
    - [https://www.cdc.gov/tobacco/data_statistics/index.htm](https://www.cdc.gov/tobacco/data_statistics/index.htm)
- Calorie consumption
- Geographical location
- Exercise
- Amount of time sitting:
    - [https://www.webmd.com/fitness-exercise/news/20160406/too-much-sitting-may-shorten-your-life-study-suggests](https://www.webmd.com/fitness-exercise/news/20160406/too-much-sitting-may-shorten-your-life-study-suggests)
    - [https://www.usnews.com/news/articles/2012/07/09/study-excessive-sitting-cuts-life-expectancy-by-two-years](https://www.usnews.com/news/articles/2012/07/09/study-excessive-sitting-cuts-life-expectancy-by-two-years)
- Sleep:
    - [https://www.google.com/search?q=effect+of+sleep+on+life+expectancy&rlz=1C5CHFA_enUS764US764&oq=effect+of+sleeping+on+life+&aqs=chrome.1.69i57j0l2.5838j0j7&sourceid=chrome&ie=UTF-8](https://www.google.com/search?q=effect+of+sleep+on+life+expectancy&rlz=1C5CHFA_enUS764US764&oq=effect+of+sleeping+on+life+&aqs=chrome.1.69i57j0l2.5838j0j7&sourceid=chrome&ie=UTF-8)
- Obesity:
    - [https://jamanetwork.com/journals/jama/fullarticle/195748](https://jamanetwork.com/journals/jama/fullarticle/195748)
- Family health history:
    - [https://www.cdc.gov/genomics/famhistory/famhist_researchers.htm](https://www.cdc.gov/genomics/famhistory/famhist_researchers.htm)
    - Scrape geneological sites for information about cause of death, and search for correlations in cause of death
    - FAMILY HISTORY OF LIFE EXPECTANCY APPARENTLY HAS A VERY SMALL EFFECT.