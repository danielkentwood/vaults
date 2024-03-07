# ç Hadoop functions

##### Metadata
created:: 2023-03-04 00:02
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/praxis 
kind:: #code
status:: #status/seed
language:: 
platform:: [[Hadoop]]
***

## hadoop filesystem (HDFS)

From the [A&BC Tech Repo](https://github.aetna.com/pages/analytics-org/abc-tech-repo/analytics_computing_environment/cluster/hdfs/): 

> HDFS is the storage layer of Hadoop. 
> 
> * Each file stored in the Hadoop cluster is divided into blocks once it's over a default size configured by Hadoop admins. 
> * Each block is stored on three different data nodes.
> * Each Hive table is stored insider a folder on HDFS. The folder can have many files, each of which will be stored as described above.
> * When scheduling a Hive or MapReduce job, YARN (the resource manager of hadoop) will try to execute tasks on the nodes that store blocks of the table's files. This bring data close to compute and increase the efficiency of computation.
> 
> An HDFS path look like `hdfs://server:8020/path/to/hdfs/file`
> 
> Where __hdfs__ is the protocol, __server__ is HDFS server name (prodmid for HDP 2.6 Production cluster). 8020 is the port number for hdfs. /path/to/hdfs/file is the path for the file. For example, the Hive table __default.nyse_stocks__ is located at `hdfs://prodmid:8020/training/nyse`
> 
> When using Hadoop tools like Hive or spark, `hdfs://promid:8020` can be omitted.

see https://cvshealth.stackenterprise.co/questions/507/856#856 for more info



## Basic HDFS commands
All hdfs commands start with "hadoop fs". Run the commands on a terminal of jupyterhub or SSH session.

#### Listing files
```bash
hadoop fs -ls <path>
```

If path is ignored, the user's home directory will be listed.

#### Creating new directory
```bash
hadoop fs -mkdir <dir name>
```

#### Copying file from edge node to HDFS
```bash
hadoop fs -put <local file path> <HDFS file path>
```

#### Copying files from HDFS to edge node
```bash
hadoop fs -get <HDFS file path>
```

#### Delete files
```bash
hadoop fs -rm <HDFS file path>
```

When a file is deleted, it'll be moved to the .trash folder. You can use the -skipTrash option to remove the file permanently
```bash
hadoop fs -rm -skipTrash <HDFS file path>
```

#### Delete an HDFS folder
```bash
hadoop fs -rm -r <HDFS folder name>
```

## Working Examples

#### Upload data to your HDFS home

To upload data file or folder on edge node to HDFS under a new folder named data, use below commands on the edge node

```bash
hadoop fs -mkdir data # this will create a new folder data under your HDFS home folder
hadoop fs -put <file name> data/
```
#### Download data from HDFS to edge node

There will be times that you want to take data to edge node,
```bash
hadoop fs -get <hdfs path> <edge node path>
```

## Work with data in HDFS

You don't need to download the data if you just want to check the data. For text file,

```bash
hadoop fs -cat <hdfs file path>
hadoop fs -head <hdfs file path>
hadoop fs -tail <hdfs file path>
```

Refer to hadoop document for more commands.

#### Create a Hive external table from data in your home folder

First, you need to put the data in a folder, so create a folder in hdfs first, then upload data to the newly created folder:
```bash
hadoop fs -mkdir data/table_name
hadoop fs -put data.csv data/table_name
```

Remember to remove header before upload to HDFS
Now you are ready to create the external table at HDFS location: `/user/a123456/data/table_name`.

Second, run hive2 command from command line and create the table:
```sql
use db_name;
CREATE EXTERNAL TABLE IF NOT EXISTS lending_club (
col1 string,
col2 string )
ROW FORMAT DELIMITED
FIELDS TERMINATED BY ','
STORED AS TEXTFILE
LOCATION '/user/a123456/data/table_name';
```

Pay attention that `/user/a123456/data/table_name` is the absolute path of the HDFS folder you just created. 
Read the HDFS file from spark

Suppose you have a file under `/user/a123456/data/table_name` with first line header.

Assume a spark session is already created as variable named "spark", below is the python code to read in the csv file with header:

```python
df = spark \
.read \
.format("csv") \
.option("header", "true") \
.load("/user/a123456/data/table_name")
```

Use additional `option("delimiter ", "|")` if delimiter is not ",".

#### Write to HDFS and Hive from spark

To write a Spark dataframe to an HDFS location,

```python
df.write.parquet("/user/a123456/folder_name")
```

Note that the folder_name shouldn't exist.

To write a spark dataframe to a Hive table:

```python
target_table = "db.table"
# df is a spark dataframe
df = df.repartition(20).cache()
df.createOrReplaceTempView("mytempTable")
spark.sql("DROP TABLE IF EXISTS " + target_table)
spark.sql("CREATE TABLE " + target_table + " AS SELECT * FROM mytempTable")
```
