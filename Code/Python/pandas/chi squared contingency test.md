mode: #mode/praxis 
kind:: #code
status:: #status/seed
language:: [[ç Python]]
platform:: [[Pandas]]

### In Pandas, get count tables with $\chi^2$ p-values
Here's a helpful article on chi-squared: [https://towardsdatascience.com/gentle-introduction-to-chi-square-test-for-independence-7182a7414a95](https://towardsdatascience.com/gentle-introduction-to-chi-square-test-for-independence-7182a7414a95)

```python
from scipy.stats import chi2_contingency
import pandas as pd

def get_std(p, N):
    p = np.array(p)
    N = np.array(N)
    return np.sqrt(p*(1-p)/N)

def get_ci(p, std):
    cis = []
    for i,k in enumerate(p):
        cis.append((p[i]-std[i]*2, p[i]+std[i]*2))
    return cis

def general_chi_square(df, index_var, col_var, print_flag=1):
	"""
	Perform crosstab and chi-squared test on the contingency table.
	
	Inputs:
		* df: A pandas dataframe
		* index_var: categorical column from `df` that will become the index
					 values in the output dataframe(s).
		* col_var: categorical column from `df` that will become the columns in
				   the output dataframe(s).
		* print_flag: (optional) flag for printing.

	Outputs: 
		* df_crosstab: a pandas dataframe containing the counts from the crosstab.
		* df_percent: a pandas dataframe containing percentages from the crosstab.
		* pval: a p-value from the chi-squared test.
	"""
    # run the crosstab
    df_crosstab = pd.crosstab(
	    index=df[index_var], 
	    columns=df[col_var], 
	    margins=True
	)
    # get the chi_square for this table
    pval = chi2_contingency(df_crosstab.iloc[0:-1,0:-1])[1]
    # get percentages
    df_percent = (100 * (df_crosstab / df_crosstab.iloc[-1,-1])).round(2)
    # print
    if print_flag:
        print('Counts: \n')
        display(df_crosstab)
        print('percentages: \n')
        display(df_percent)
        print('p-value: {}'.format(pval))
    return df_crosstab, df_percent, pval



def boolean_chi_square(df, index_var, col_var, print_flag=1):
    """
    Perform crosstab and chi-squared test where the crosstab index variable is
    boolean. Only keep the true values.
    
    Inputs:
        * df: A pandas dataframe
        * index_var: boolean column from `df` that will become the index
                     values in the output dataframe(s).
        * col_var: categorical column from `df` that will become the columns in
                   the output dataframe(s).
        * print_flag: (optional) flag for printing.

    Outputs: 
	    A dict containing the following:
        * count_table: a pandas dataframe containing the counts from the crosstab.
        * percent_table: a pandas dataframe containing percentages from the crosstab.
        * p: a p-value from the chi-squared test.
        * chi2: the chi2 score,
        * percentages: list of the relative percentages for each category
        * variances: list of variances for each category
        * fig: a figure plotting the percentages ± 95% confidence intervals
    """
    # run the crosstab
    df_crosstab = pd.crosstab(
        index=df[index_var], 
        columns=df[col_var], 
        margins=True
    )
    # get the chi_square for this table
    chi2, pval, dof, exp_freq = chi2_contingency(df_crosstab.iloc[0:-1,0:-1])
    # get percentages
    true_count = df_crosstab.iloc[df_crosstab.index==True, :].values[0]
    all_count = df_crosstab.iloc[df_crosstab.index=='All', :].values[0]
    percents = true_count / all_count
    # get 95% CI
    stds = get_std(
        percents[:-1],
        true_count[:-1]
    )
    cis = get_ci(
        percents[:-1], 
        stds
    )

    # Only keep TRUE rows and add percentages
    df_count_percent = pd.DataFrame([
        true_count, 
        percents
    ])
    df_count_percent.index = ['count','pctg']
    df_count_percent.columns = df_crosstab.columns
    
    # build the plot
    fig = go.Figure(data=go.Scatter(
        x=df_count_percent.columns[:-1],
        y=100*np.array(percents[:-1]),
        error_y=dict(
            type='data',
            symmetric=True,
            array=100*2*np.array(stds))
    ))
    
    # print
    if print_flag:
        print('\nCounts:')
        display(df_crosstab)
        print('\n\nPercentages:')
        print(f'Index variable: {index_var}=TRUE')
        display(df_count_percent)
        print('\np-value: {}\n\n'.format(pval))

    return {
        'count_table': df_crosstab, 
        'percent_table': df_count_percent, 
        'p': pval,
        'chi2': chi2,
        'percentages': percents[:-1],
        'variances': stds,
        'fig': fig
    }
```





