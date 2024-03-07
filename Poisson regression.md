# Poisson regression
created:: 2022-09-15 16:45
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/gnosis
kind:: #zettel 
status:: #status/seed
parent:: [[regression]], [[statistical models]]
***

### When is poisson regression the ideal approach? 
* If we are comparing counts 
* If we assume the distributions we are modeling are poisson (i.e., timing of any sample is independent of the previous sample)
	* If we don't assume this, then we know the dynamics of other systematic time-varying influences on the event rate

>[!important] Example: Neuron firing rate
>We typically assume a Poisson distribution to spontaneous firing rates of a given neuron. If we provide a stimulus that excites the neuron, we can expect a transient increase in the firing rate. We can model the expected firing rate relative to the timing of the stimulus as a Poisson distribution + an arbitrary set of temporal basis functions.



## External Resources