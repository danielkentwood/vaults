# ç Interactive impulse response function
title:: ç Interactive impulse response function
created:: 2022-09-23 12:22
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/praxis 
kind:: #code
status:: #status/seed
language:: [[ç Python]]
platform:: [[Pandas]], [[Plotly]] 
***


```


```






**Build a table with the following columns**
* member identifier
* experimental group
* outreach date
* KPI value
* KPI date
* optional: any other dates that potentially have a causal impact on KPI
* optional: any other secondary outcome metrics (value and date)

**Once that table is ready, write a python function that plots the impulse-response function of the intervention, with the following features:**
* widgets:
	* select the impulse date (default is the outreach date)
	* select the response data (default is KPI)
	* toggle collapse or split any experimental cells within treatment/control (default is collapsed)
	* select aggregation method (options are sum over total, average over total, average over member average, average over member sum; default is average over total)
		* toggle 95% CI bars when possible (default is off)
	* toggle cumulative or instantaneous aggregation of response data (default is instantaneous)
	* select time interval (default is weekly; options are daily, weekly, monthly, yearly)
* operations:
	* subtract the impulse date from the response data date
	* group by the time interval and the toggle-selected experimental groups, using the selected aggregation method
	* plot it

## Resources

