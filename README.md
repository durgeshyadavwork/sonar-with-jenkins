# For Sonarqube
Prerequisite

Plugin Required --->> SSH Agent 
“Manage Jenkins” > “Manage Credentials” 
Step a: ID: docker-hub-creds   ,  Username: dugreshyadav   ,  Password: Docker-Token
Step b: ID: ec2-ssh-key      , Username: ec2-user        , Password: Private-Key
Create Git-repo (sonar-with-jenkins ---> test/sonar branch ) and docker image Repo (sonar-with-jenkins)


----------------------------------------------------------------------------------------------------------------------------------------------------------

Step 1: Install SonarQube Plugin
To run your project analyses with Jenkins, the following plugins must be installed and configured:

Navigate to Jenkins Dashboard -> “Manage Jenkins” -> “Manage Plugins”.

Go to the “Available” tab, search for “SonarQube Scanner” plugin, and install it.

------------------------------------------------------------------------------------------------------------------------------------------------------------

Step 2: Generate SonarQube Token
2.1. Log in to SonarQube using the admin credentials.

2.2. Navigate to “My Account” -> “Security” -> “Generate Tokens”.

2.3. Provide a name for the token and click on “Generate”. Save the generated token securely.



Step 3: To set up SonarQube credentials in Jenkins:

Go to “Manage Jenkins” > “Manage Credentials”.
Click “Add Credentials”.
Select the credential type (e.g., “Secret text” for tokens, “Username with password” for username/password).
Enter the credential details.
Provide an ID and description. (ID: sonarqube-token)
Save the credentials.




Step 4: Installing SonarQube Scanner in Jenkins
Open Jenkins dashboard and navigate to Manage Jenkins > Global Tool Configuration.
Scroll down to the SonarQube Scanner section.
Click on Add "SonarQube Scanner" and provide a name for the installation. (name: SonarScanner)
Specify the path to the SonarQube scanner installation directory.
Save the configuration.

--------------------------------------------------------------------------------------------------------------------------------------------------------------


Step 5: Create a New Project:
Once logged in, you need to create a new project in SonarQube. Follow these steps:

Click on the “Projects” tab on the top menu.                                   //same as setup sonar-project.properties 
Click on the “Create Project” button.                                          //sonar-project.properties ---->>> sonar.projectName=Sonar with Jenkins
Provide a unique project key and a display name for your project.              //sonar-project.properties ---->>> sonar.projectKey=sonar-with-jenkins
Choose the appropriate language for your project. SonarQube supports various programming languages.
Click on “Set Up” to proceed.


----------------------------------------------------------------------------------------------------------------------------------------------------------------

Step 6: Configure SonarQube in Jenkins
Navigate to Jenkins Dashboard -> “Manage Jenkins” -> “Configure System”.
Scroll down to the “SonarQube servers” section and click on “Add SonarQube”.
Provide a name for the SonarQube server.                    (name: ExternalSonarQube) //ExternalSonarQube this name given pipeline script stage -->> withSonarQubeEnv('ExternalSonarQube')
Enter the SonarQube server URL (http://IP_SonarQube:9000).
Paste the SonarQube token generated in Step 2.              (select token)
Save the configuration.



Step 7: Configure Webhook on SonarQube UI side 

Click on Administration tab, select Webhook from the drop down and click on create button. Name it, provide jenkins http://13.232.223.27:8080/sonarqube-webhook/ Save.    //(name: Jenkins Quality Gate)
