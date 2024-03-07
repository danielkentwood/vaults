mode: #mode/praxis 
kind:: #code
status:: #status/seed
language:: [[ç Python]]
platform:: [[Pandas]]

In Pandas, you can extract the YYYY-MM from a datetime object with the following:

	df['clm_srvc_dt'].dt.to_period('M')

You can do arbitrary formats as well:

	df['clm_srvc_dt'].dt.strftime('%m/%Y')

This will give you dates with the format of 08/2022, for example. 