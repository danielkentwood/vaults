# Min of 2 uniform random variables
created:: 2022-08-31 05:17
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/praxis 
kind:: #zettel 
status:: #status/seed
language:: 
platform:: 
***

We want to find the [[expected value]] of the min of 2 random variables taken from the same [[uniform distribution]].

## Question:

Say we have X ~ Uniform(0, 1) and Y ~ Uniform(0, 1). What is the expected value of the minimum of X and Y?

## Answer/Discussion:

![Min%20of%202%20uniform%20random%20variables%20636b2c3db083493b8927ff879ce733b0/Untitled.png](Untitled%2023.png)

[http://premmi.github.io/expected-value-of-minimum-two-random-variables](http://premmi.github.io/expected-value-of-minimum-two-random-variables)

[https://tsourakakis.com/2015/12/14/expectation-of-minimum-of-n-i-i-d-uniform-random-variables/](https://tsourakakis.com/2015/12/14/expectation-of-minimum-of-n-i-i-d-uniform-random-variables/)

[https://www.youtube.com/watch?v=DsshiqmOdtw&ab_channel=StatQuestwithJoshStarmer](https://www.youtube.com/watch?v=DsshiqmOdtw&ab_channel=StatQuestwithJoshStarmer)

[https://www.youtube.com/watch?v=-qt8CPIadWQ&ab_channel=jbstatistics](https://www.youtube.com/watch?v=-qt8CPIadWQ&ab_channel=jbstatistics)

We want to solve for the expected value by [[taking the integral]] of a PDF of min(X, Y).

To get to this point, we need to first get the CDF of min(X, Y) and differentiate it.