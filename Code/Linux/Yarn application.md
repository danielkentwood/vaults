mode: #mode/praxis 
kind:: #code
status:: #status/seed
language:: [[Linux]]
platform:: [[Hadoop]]

To interact with different yarn applications (Hive and Spark jobs), you can use the `yarn application` command

For a breakdown of the different commands

	yarn application --help

To list current jobs:

	yarn application -list

All current jobs owned by me:

	yarn application -list | grep a522860

Kill a specific job:

	yarn application -kill <application_id>
