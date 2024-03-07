# SugarTS
created:: 2022-08-31 05:16
modified:: <%+ tp.file.last_modified_date() %>
mode:: #mode/management
kind:: #project 
status:: #status/dormant
parent::

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





To-do

- [ ]  re-think optimization approach. What other error metrics could I consider?
    - [ ]  Can I get multiple boluses?
- [ ]  consider doing a probabilistic approach with ranked suggestions (instead of just choosing the best one). This will become useful later if/when I get streaming data to work.
- [x]  build validation code into the package — the forecasts are pointless unless they are accurate.
- [ ]  you don't need to have real streaming data. You can create a massive dataset and host it somewhere, then have an API that pings it every five minutes for the next time point. This will work for now.
- [ ]  start writing unit tests and get CI/CD working on github or gitlab.


## **Implementations of DA-RNN**

[https://github.com/Seanny123/da-rnn](https://github.com/Seanny123/da-rnn)

improved branch: [https://github.com/goshaQ/da-rnn](https://github.com/goshaQ/da-rnn)

[https://github.com/Zhenye-Na/DA-RNN](https://github.com/Zhenye-Na/DA-RNN)

[https://github.com/YitongCU/Duel-staged-Attention-for-NYC-Weather-prediction](https://github.com/YitongCU/Duel-staged-Attention-for-NYC-Weather-prediction)

[https://github.com/KurochkinAlexey/DA-RNN/blob/master/DARNN_SML2010.ipynb](https://github.com/KurochkinAlexey/DA-RNN/blob/master/DARNN_SML2010.ipynb)

**SKTIME**

[https://github.com/alan-turing-institute/sktime](https://github.com/alan-turing-institute/sktime)

[https://www.youtube.com/watch?v=wqQKFu41FIw&ab_channel=CodingTech](https://www.youtube.com/watch?v=wqQKFu41FIw&ab_channel=CodingTech)

Focus on writing Medium articles. 

Content is important but less important than the ability to clearly communicate. 

Demonstrate that you understand the methodology and tooling and principles. This doesn't need to be a successful research project. 

A great skill to have is knowing when to stop on a project. 

- Once the model is predicting, use a brute force grid search (with parameters timing and amount of insulin) to identify the inputs where the model performs the best (according to some metric like the number of time points within the desired range).
- Future considerations:
    - maybe we only need to look at a scalar value where the peak of the insulin and carb impulse responses are happening?
    - 

## Notes

[https://openaps.org/](https://openaps.org/)

[https://github.com/openaps](https://github.com/openaps)

Ultimate goal:

The app will ping the api for new data and will keep up to 6 months worth of data for a user.

[https://github.com/nightscout/cgm-remote-monitor/](https://github.com/nightscout/cgm-remote-monitor/)

The model will be updated once a week.

[SugarTS%206e9f2f53ef8b4bc4a2f0da68960735be/2008.02852.pdf](2008.02852.pdf)

Use something like DeepAR, which provides probabilistic forecasts.

[1704.04110.pdf](1704.04110.pdf)

Ultimately, the ideal would be to have a ranked list of "next best actions" to bring or keep glucose levels close to the target level. These would get updated every five minutes.

Potential approaches:

**Convolutional Recurrent Neural Networks for Glucose Prediction**

[1807.03043.pdf](1807.03043.pdf)

**Automatic blood glucose prediction with confidence using recurrent neural networks**

[1696290_ssdl2018_paper_10.pdf](1696290_ssdl2018_paper_10.pdf)

**Blood Glucose Prediction with Variance Estimation Using Recurrent Neural Networks**

[Martinsson2020_Article_BloodGlucosePredictionWithVari.pdf](Martinsson2020_Article_BloodGlucosePredictionWithVari.pdf)

GOAL:

to understand the dose-response time series for

- protein
- simple and complex carbs
- 

IDEA:

Model all of the important covariates as gaussians with the following parameters:

- skew (long tail at start or finish of time-course?)
- bias (where does it peak in time)
- variance (how wide is the curve -- i.e., how long does the covariate have an effect on BG?)
- coefficient (determined by the amount of food, the dose of the

Time-Series Analysis of Continuously Monitored Blood Glucose:The Impacts of Geographic and Daily Lifestyle Factors

[804341.pdf](804341.pdf)

export data from:

- myfitnesspal (currently not exporting, follow up on this)
- Dexcom clarity (get login info for this)
- tandem: t-connect website (get login info for this)

Do standard time-series analysis

Run several different ML models on the time-series, trying to pull out the effects of the various features

[https://stackoverflow.com/questions/42031684/read-a-csv-file-with-multiple-data-sections-into-an-addressable-structure](https://stackoverflow.com/questions/42031684/read-a-csv-file-with-multiple-data-sections-into-an-addressable-structure)

[https://github.com/YitongCU/Duel-staged-Attention-for-NYC-Weather-prediction](https://github.com/YitongCU/Duel-staged-Attention-for-NYC-Weather-prediction)