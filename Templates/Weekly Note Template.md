# <% tp.file.title %>
<%* 
m0 = moment([String(20)+tp.file.title.substr(1,2), tp.file.title.substr(8,2) -1, tp.file.title.substr(10,2)]).subtract(7, 'd');

m1 = moment([String(20)+tp.file.title.substr(1,2), tp.file.title.substr(8,2) -1, tp.file.title.substr(10,2)]); 

m2 = moment([String(20)+tp.file.title.substr(1,2), tp.file.title.substr(8,2) -1, tp.file.title.substr(10,2)]).add(7, 'd'); 
-%>
<< [[<%- m0.format("[Y]YY[W]ww (MMDD-") -%><% m0.add(6, 'd').format("MMDD)") -%>]] || [[<%- m2.format("[Y]YY[W]ww (MMDD-") -%><% m2.add(6, 'd').format("MMDD)") -%>]] >>
<% await tp.file.move("/Periodic/Weekly Notes/" + tp.file.title) -%>

##### Metadata
created:: <% tp.file.creation_date() %>
modified:: <%+ tp.file.last_modified_date() %>
mode:: #mode/management
kind:: #periodic/weekly
status:: #status/raw
description:: Weekly review for <% m1.format("YYYY-MM-DD") %> to <% m1.add(6, "d").format("YYYY-MM-DD") %>
***

## Notes
```dataviewjs
let curr = dv.current()
let month = String(Number(curr.file.name.substr(8,2)))
let day = String(Number(curr.file.name.substr(10,2))) 
let week = String(Number(curr.file.name.substr(4,2)))
let year = '20'+String(Number(curr.file.name.substr(1,2)))
const dt = DateTime.fromObject({
	year: year,
	month: month,
	day: day
});

// get the days of the week in an array
let first_day = dv
	.date(dt.toFormat('yyyy-LL-dd'))
var week_arr = new Array();
let i = 0;
while (i<7) {
	week_arr.push(first_day.plus({days: i}).toFormat('yyyy-LL-dd'))
	i++
}

// daily notes
let daily_pages = dv.pages("#periodic/daily")
	.where(p => {
		if (p.file.day && week_arr.includes(p.file.name)) {
			return true
		}
	})
	.sort(p => p.file.day)
	
dv.header(3, "This week's daily notes:")
if (daily_pages.length > 0) {
	dv.list(daily_pages.file.link)
} else {
	dv.paragraph('No daily notes for this week yet')
}

// CREATED THIS WEEK
let created_pages = dv.pages().where(p => {
	return p.file.name != curr.file.name && !daily_pages.includes(p) &&
		week_arr.includes(p.file.ctime.toFormat('yyyy-LL-dd'))
})
	.sort(p => p.file.ctime, 'desc')
	
dv.paragraph('***')
dv.header(3, "Created this week:")
if (created_pages.length > 0) {
	let periodic_c = created_pages.filter(p => 
					String(p.kind).includes("periodic"))
	if (periodic_c.length > 0) {
		dv.header(4, '~Other periodic~')
		dv.table(['Page', 'Kind'],
			periodic_c
				.sort(k => k.kind, 'desc')
				.map(k => [k.file.link, k.kind]))
	}

	let nonperiodic_c = created_pages.filter(p => 
						!String(p.kind).includes("periodic"))
	if (nonperiodic_c.length > 0) {
		dv.header(4, '~Non-periodic~')
		dv.table(['Page', 'Kind'],
			nonperiodic_c
				.sort(k => k.kind, 'desc' || k.file.link)
				.map(k => [k.file.link, k.kind]))
	}
} else {
	dv.paragraph('No notes created this week')
}

// UPDATED THIS WEEK
let updated_pages = dv.pages().where(p => {
	return p.file.name != curr.file.name && !daily_pages.includes(p) &&
		week_arr.includes(p.file.mtime.toFormat('yyyy-LL-dd'))
})
	.sort(p => p.file.mtime, 'desc')

dv.paragraph('***')
dv.header(3, "Modified this week:")
if (updated_pages.length > 0) {
	let periodic_m = updated_pages.filter(p => 
					String(p.kind).includes("periodic"))
	if (periodic_m.length > 0) {
		dv.header(4, '~Other periodic~')
		dv.table(['Page', 'Kind'],
			periodic_m
				.sort((k,j) => k.kind, 'desc')
				.map(k => [k.file.link, k.kind]))
	}

	let nonperiodic_m = updated_pages.filter(p => 
						!String(p.kind).includes("periodic"))
	if (nonperiodic_m.length > 0) {
		dv.header(4, '~Non-periodic~')
		dv.table(['Page', 'Kind'],
			nonperiodic_m
				.sort((k,j) => k.kind, 'desc')
				.map(k => [k.file.link, k.kind]))
	}
} else {
	dv.paragraph('No notes modified this week')
}

```

## Tasks
```dataviewjs
let curr = dv.current()
let month = String(Number(curr.file.name.substr(8,2)))
let day = String(Number(curr.file.name.substr(10,2))) 
let week = String(Number(curr.file.name.substr(4,2)))
let year = '20'+String(Number(curr.file.name.substr(1,2)))
const dt = DateTime.fromObject({
	year: year,
	month: month,
	day: day
});

// get the days of the week in an array
let first_day = dv
	.date(dt.toFormat('yyyy-LL-dd'))
var week_arr = new Array();
let i = 0;
while (i<7) {
	week_arr.push(first_day.plus({days: i}).toFormat('yyyy-LL-dd'))
	i++
}

// get pages
let task_pages = dv.pages().where(p => {
	return !p.ignoreTasks &&
		p.file != curr.file
});

// get done tasks
var done_count = new Array();
for (let i = 0; i < week_arr.length; i++) {
	done_count.push(
		task_pages.file.tasks.where(t => {
			if (t.done && week_arr[i] == dv.date(t.done).toFormat('yyyy-MM-dd')) {
				return true
			}}).length)
}

// get due tasks
var due_count = new Array();
for (let i = 0; i < week_arr.length; i++) {
	due_count.push(
		task_pages.file.tasks.where(t => {
			if (t.due && week_arr[i] == dv.date(t.due).toFormat('yyyy-MM-dd')) {
				return true
			}}).length)
}

// plot the data
const chartData = {  
	type: 'line',  
	data: {  
		labels: week_arr,  
		datasets: [  
		{  
			label: 'Tasks completed',  
			data: done_count,  
			backgroundColor: [  
				'rgba(255, 99, 132, 0.2)'  
			],  
			borderColor: [  
				'rgba(255, 99, 132, 1)'  
			],  
			borderWidth: 1,
			fill: true
		}, 
		{  
			label: 'Tasks due',  
			data: due_count,  
			backgroundColor: [  
				'rgba(90, 255, 132, 0.2)'  
			],  
			borderColor: [  
				'rgba(90, 255, 132, 1)'  
			],  
			borderWidth: 1,
			fill: true
		}, 
		]  
	}  
}
window.renderChart(chartData, this.container);

// list the tasks
let t_due = task_pages.file.tasks.where(t => {
		if (
			t.due && 
			!t.done && 
			week_arr.includes(dv.date(t.due).toFormat('yyyy-MM-dd')) 
		) {
			return true
		}
	})
	.sort(t => t.due, 'asc');

let t_done = task_pages.file.tasks.where(t => {
		if (
			t.done && 
			week_arr.includes(dv.date(t.done).toFormat('yyyy-MM-dd'))
		) {
			return true
		}
	})
	.sort(t => t.done, 'asc');

dv.header(3, "Tasks Due:")
if (t_due.length) {
	dv.taskList(t_due, false)
} else {
	dv.el("em", "No tasks due this week")
}

dv.paragraph('<br><hr>')
dv.header(3, "Tasks Done:")
if (t_done.length) {
	dv.taskList(t_done, false)
} else {
	dv.el("em", "No tasks done this week")
}

// CREATED THIS WEEK
let weekTasks = dv.pages().where(p => {
	return p.file.name != curr.file.name &&
		(
			week_arr.includes(dv.date(p.file.ctime).toFormat('yyyy-MM-dd')) || 
			(p.file.day && week_arr.includes(dv.date(p.file.day).toFormat('yyyy-MM-dd')))
		)
})
	.file.tasks

dv.paragraph('<br><hr>')
dv.header(3, "New tasks added:")
if (weekTasks.length > 0) {
	dv.taskList(weekTasks.filter(t => !t.completed))
} else {
	dv.el("em", "<br>No tasks added this week<br>")
}
```

***
## Backlogs
### TODO
```dataviewjs
dv.taskList(dv.pages('-"Templates"').where(p => {
	return !p.ignoreTasks
}).file.tasks
	.where(t => !t.completed)
	.where(t => t.todo))
```



### Capture
```dataview
TABLE
	capture AS "item to capture",
	dateformat(file.ctime, "yyyy-MM-dd") AS "date"
WHERE capture 
SORT file.ctime
```

***
## Reference