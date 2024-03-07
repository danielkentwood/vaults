# ç Tutorial on Synthetic Patient Data
created:: 2022-06-02 18:05
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/praxis 
kind:: #code
status:: #status/seed
language:: [[Linux]]
platform:: [[TigerGraph]], [[Docker]]
***



# Use TigerGraph to analyze synthetic patient data
### Note: These instructions are for mac users.

Let's load a toy dataset. If you are new to TigerGraph as a platform, this will help you set up your environment properly before you start working with any real data. 

These instructions expand on https://github.aetna.com/analytics-org/mentygra/tree/master/applications/synthetic_app.

Tigergraph's app (GraphStudio) will act as the graph DB, the analytics engine, and the UI. We will be running it locally within a Docker container. This means that whenever we want to use any of Aetna's data in GraphStudio, we'll need to get it onto our local machine first. A simple way to do this is to run SQL queries, save the outputs as CSV files, and download the CSV files from the edge node to your local computer. In this demo, we will do the following:
1. Set up the environment on your local computer.
2. Create a docker container with GraphStudio inside. 
3. Transfer data from local dir to the docker container. 
4. Upload schema, data, and some queries to the GraphStudio instance inside the container.
5. Run a few queries in GraphStudio.


## Set up your environment
1. **Download Docker**
	If you want to test if it is running, use the instructions in the synthetic app README, but make sure you are not connected to the VPN -- it tries to clone a repo from GitHub (commercial), which the VPN will block.
2. **Download command line developer tools**
	If you haven't already, go ahead and download command line developer tools (XCode). 
3. **Set up SSH Key on GitHub** 
	Make sure you have an ssh key set up between your local computer and your Aetna GitHub account. If you don't, do the following:
	* check if you have an existing ssh key on your local computer: 
		`ls -al ~/.ssh`
	* if you have one of the following, you're set:
		-   _id_rsa.pub_
		-   _id_ecdsa.pub_
		-   _id_ed25519.pub_
	- If not, you'll need to create one:
		`ssh-keygen -t rsa -C "your_email@aetna.com"`
		(you can use the default filename and you can leave the passphrase empty)
	* Copy the public key to the clipboard, e.g.:
		`pbcopy < ~/.ssh/id_rsa.pub`
	* Go to Github. Click **Settings** under your profile photo. In the "Access" section, click **SSH and GPG Keys**. Click **New SSH Key**. Provide a title (e.g., "Local laptop") and paste the contents of the clipboard into the "Key" field. 
	* You should be able to clone Aetna GitHub repos onto your local machine now.
4. **Clone the MentyGra repo**
	You should be logged into the VPN at this point.
	`git clone git@github.aetna.com:analytics-org/mentygra.git`

## Create the tigergraph container 
1. **Create tigergraph instance**
	1. Edit the `install_tg.sh` file so that the `SOURCE_PATH` variable reflects the location of your local clone of the repo. 
	2. Modify the permissions with `chmod 777 install_tg.sh`.
	3. Run: `./install_tg.sh` (This will download about 4G of files onto your machine)
2. **Log in to tigergraph**
	1. Ensure the _syntheatg3_ Docker container is currently running. The `install_tg.sh` shell script automatically launches it, but if you come back after disconnecting, you'll need to make sure the container is running again. If you're not sure about its status, use `docker ps` at the command line. This will list containers and their current status. If your container isn't running, you can launch it in two ways:
		1. `docker container start syntheatg3`
		2. On the Docker app, select the _syntheatg3_ container, then click the START button in the upper right corner. 
	2. Run: `./login_tg.sh`
	3. password is `tigergraph`
		Your terminal will now index the container, and you should see your prompt change to something like the following: `tigergraph@9c5362d9b4fa:~$`, where _9c5362d9b4fa_ is the container ID. 
3. **Copy data to the container**
	1. In a separate terminal, navigate back to `/mentygra/applications/synthetic_app` of in your local clone of the mentygra repo. 
	2. Run: `./load_data_to_container.sh`
	3. your Docker container should now contain the GSQL queries and the data in `~/demo`.
4. **Start the graph**
	1. At the tigergraph container prompt, run: `gadmin start all`. 
	2. You should now be able to open _GraphStudio_. You can do this in two ways:
		1. Go to `http://localhost:14240` , or...
		2. On the Docker app, select the _syntheatg3_ container, then click "OPEN IN BROWSER" in the upper right corner. 
5. **Load the data**
	This step actually consists of three separate steps. We need to:
	1. Initialize the Tigergraph database with a DDL. This provides the schema of the graph.
	2. Load the test data. 
	3. Upload 3 analysis queries (GSQL) to the query library.

	We created a shell script that does this for you. From the local terminal at `/mentygra/applications/synthetic_app`, run: 
	`./deploy_graph.sh`

## Graph Analytics
1. Explore the graph
2. Run a basic GSQL query
3. More advanced GSQL query



