# Jenkins



Jenkins:
--------

Note: Though the script works fine, there is a permission issue when it tries to connect with local Docker image for Jenkins lts.H.Use jenkins blue ocean image instead
Script sample: https://dzone.com/articles/building-docker-images-to-docker-hub-using-jenkins
 
(1) Popular CI tool 
(2) Allows us to build pipelines for runnign unit tests, code qulaity checks, packae your app, integration tests and deploy 
Sample scripts: D:\OneDrive\Study\DevOps\devops-master-class-master\jenkins\JenkinsFileBackups

(3) Microservice being used: Currency Exchange
	

(4)Jenkins will be run as a docker container:



(5)Docker compose :
	- Is by default installed with Docker desktop. If not avalable, install manually 
	- docker-compose version:
		cmd: docker-compose version 


(6) Start Docker :
	


(7)Yaml fil for Docker compose: 
	- cd
	- cmd: docker-compose up


(8) Setting up Jenkins:
	- copy pwd from logs of docker-compose:
		- jenkins    | Please use the following password to proceed to installation:
jenkins    |
jenkins    | 68235f206f6141f3b0ea03d6d6c3eb01


	- url: localhost:8081	
	- enter admin pwd as copied from logs
	- Install suggested plugins:
		- Thsi will take some time to complete
	- User name: buddy
	- password: buddy
	- Full name : thera para
	- Email adress: aaduthoma@gmail.com
	- use default url: http://localhost:8081/





(9) Setup MAVEN and Docker:

	- Docker:
		- Plugin mAnager-> Available-> Search fro Dockers -> Select  Docker,Docker Commons,Docker Pipeline, Docker API, Docker Build step, CloudBees Docker Build and Publish plugin , Docker Slaves
		- Restart Jenkins
		- Manage Jenkins->Manage Credentials -> Click on Global-> Add credentials :
			- Scope = Global
			- Username= docker id
			- pwd
			- ID: dockerHub  ( Note: Thsi should be teh same as mentioned in the 'Push Docker Image' step in jenkins file 
	- Maven:
		- Manage Jenkins-> Global Tool Configuration-> Maven Intallations-> Add Maven:
			- name=myMaven
			- Install Automatically
	- Docker;
		- Manage Jenkins-> Global Tool Configuration->Docker-> Add Docker-> name=myDocker-> Install Automatically	

	-GIT HUB:
	- Add GIT  credentials:
		- Geenrate personal access token in GITHUB:
			- Settings-> Developer settings-> Personal Access tokens
			- This will eb genrated the first time when we try toconnect to our repo through Jenkins
			- xx
			- Valid till Sep 28, 2021
    -GIT LAB
		- Geenrate personal acces token in GITLAB:
			- https://docs.gitlab.com/ee/user/profile/personal_access_tokens.html
			- Avatar-> Edit profile -> Personal Access Tokens:
					- Token name = Personal Access Tokens
					- Expiration date = 22-08-28
					- Seelct scope = api

		- Maange Jenkins-> Manage Credentials-> Jenkins-> Global Creentials-> Add Credential-> 
			- Username:SonyMC
			- Password: *** Use the personal access token value
			- iD: GitHub




(10) Create Jenkins job/pipeline:
	- Jenkins-> Create a job or New Item;
		- item name=jenkins-devops-microservice-pipeline
		- Select pipeline
		- Description = jenkins-devops-microservice-pipeline
		- Build triggers:
			- Options: 
				 - Build periodically:
					- Run very 1 hour: Schedule= H/60 * * * *  
					- E.g.s can be found by cliking teh ? icon
				- Poll SCM:
					- Scehdule: # Every minute
						   - * * * * *
				- Polling does nt work for Scripted pipelines. It would work only for declarative pipelines.
				- Pipeline:
					- Definition = Pipeline Script from SCM
					- SCM = GIT
						- Repositories :
							- Repository url= https://gitlab.com/demo_new/jenkins.git
							- Credentials= is a public repo so no need fro credentials 
							Access token: xx
							- branch specifier = */main
								- Note: Normally we configure */master but we have created main branch instead of master
							- Script path= Jenkinsfile

					- Build now or wait for 1 minute


Refeer : https://dzone.com/articles/building-docker-images-to-docker-hub-using-jenkins

	

