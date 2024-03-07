# <% tp.file.title %>
<< [[<% tp.date.now("YYYY-MM-DD", -1, tp.file.title, "YYYY-MM-DD") %>]] || [[<%* mmt = moment(tp.file.title).startOf('week'); -%><% mmt.format("[Y]YY[W]ww (MMDD-") -%><% mmt.add(6, 'd').format("MMDD)") -%>]] || [[<% tp.date.now("YYYY-MM-DD", 1, tp.file.title, "YYYY-MM-DD") %>]] >>

#### Metadata
created:: <% tp.file.creation_date() %>
modified:: <%+ tp.file.last_modified_date() %>
mode:: #mode/management
kind:: #periodic/daily
status:: #status/raw

#### Self Tracking
###### Today
bp_sys::
bp_dia::
weight::
miles_run::
pushups::
pullups::
curls::
shoulder_press::
calf_raise::
squats::
360_lunges::
360_planks::
###### Yesterday
hrs_sleep::
time_fell_asleep::
time_last_phone::
min_phone::
***
## Tasks
```dataviewjs
let curr = dv.current()
let today = curr.file.day.toFormat('yyyy-MM-dd')

// TODAY'S TASKS ==============================
let tasks = dv.pages().where(p => {
	return !p.ignoreTasks
})
	.file.tasks
	.where(t => {
		if (t.due && today >= dv.date(t.due).toFormat('yyyy-MM-dd')) {
			return true
		}
		if (t.done && today == dv.date(t.done).toFormat('yyyy-MM-dd')) {
			return true
		}
	})
	.sort(t => t.completed, 'asc')

if (tasks.length) {
	let overdue = tasks.filter(t => t.due && !t.completed && today > 
			dv.date(t.due).toFormat('yyyy-MM-dd')
		);
	let due_today = tasks.filter(t => t.due && !t.completed && today == 
			dv.date(t.due).toFormat('yyyy-MM-dd')
		);
	let completed = tasks.filter(t => t.completed && today ==
			dv.date(t.done).toFormat('yyyy-MM-dd')
		);

	if (overdue.length) {
		dv.header(2, 'Overdue')
		dv.taskList(overdue, false)
	}
	if (due_today.length) {
		dv.header(2, 'Due Today')
		dv.taskList(due_today, false)
	}
	if (completed.length) {
		dv.header(2, 'Completed')
		dv.taskList(completed, false)
	}
} else {
	dv.el("em",'No tasks to list :(')
}
```

## Log
### Morning
[[Morning Routine]]

