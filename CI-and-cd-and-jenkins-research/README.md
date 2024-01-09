# CI/CD and Jenkins

### What is CI?

- CI stands for Continuous Integration. 
- It is a software development practice where code changes are automatically built, tested, and integrated into a shared repository frequently. 
- Developers merge/commit code to the master branch multiple times a day, fully automated build and test process which gives feedback within few minutes, by doing so, you avoid the many integration issues that usually happen when people wait for release day to merge their changes into the release branch.
-  The main goal is to detect and address integration issues early in the development process.


### What is CD?

- CD stands for Continuous Delivery. 
- It is an extension of CI that ensures that code changes can be reliably and efficiently delivered to production at any time without manual intervention. 
- It involves automating the entire software release process up to the production environment but the deployment is completed manually.

### Difference between CD and CDE

Continuous Delivery (CD) focuses on automating the delivery process up to the production environment, the final deployment decision is manual. Continuous Deployment (CDE) is an extension of Continuous Delivery where changes are automatically deployed to production without manual intervention. Only a failed test will prevent a new change to be deployed to production.

### What is Jenkins?

- Jenkins is an open-source automation server that facilitates building, testing, and deploying code. 
- It is a Java-based program with packages for Windows, macOS, & Linux.
- It supports the automation of any project, including building, testing, and deploying code changes.
- Great range of plugins available.

### Why use Jenkins? 

Automation: Jenkins automates repetitive tasks, saving time and reducing errors.<br>
Integration: It integrates with various tools and technologies used in the software development process.<br>
Extensibility: Jenkins supports a wide range of plugins, allowing users to extend its functionality.<br>
Also has packages for Windows, macOS, & Linux.

### Benefits of using Jenkins? 

Time Savings: Automation reduces manual intervention and speeds up the development process.<br>
Consistency: Ensures consistent and repeatable builds and deployments.<br>
Integration: Integrates with various tools, making it a central hub for the development pipeline.

### Disadvantages of using Jenkins?

Steep Learning Curve: Configuring Jenkins may be complex for beginners.<br>
Resource Intensive: Jenkins can be resource-intensive, especially for large projects.

### Stages of Jenkins

1. Install Jenkins and Docker
2. Go to a jenkins.war file and run command: java -jar jenkins.war
3. Open your browser and type www.localhost:8080
4. Log in to jenkins account
5. new item x3
6. configure
7. add build step
8. execute shell
9. Enter this command: date (shows todays date)
10. Click on Post-build Actions and select build other projects
11. Enter name of Job2 then click apply and save.
12. Click on Job2 then click on configure
13. Click on add build step and select Execute shell
14. Enter this command: sudo docker pull ahskhan/jenkins:v1 (pulls the image from Docker hub repository)
15. Enter Job3 in Project to build field, apply and save.
16. Click on Job3 then click on Configure
17. Click on Add build step and select Execute shell
18. Enter this command: sudo docker run ahskhan/jenkins:v1 (runs the image pulled by Job2 and display the message from Docker image)
19. Click apply and save.
20. Back to dashboard and click on Job1
21. Build Now
22. To see the outcome of Job1 click on console output and then do the same with the other jobs

### What alternatives are there for Jenkins

- GitLab CI/CD
- Travis CI
- CircleCI
- TeamCity

### Why build a pipeline? Business value?

Faster Time to Market: Continuous pipelines accelerate the development and deployment process so they get to consumers faster.<br>
Reduced Errors: Automation reduces the likelihood of human errors in the deployment process, so user experience is smoother.<br>
Consistency: Ensures a consistent and repeatable process for development, testing, and deployment.

### Create a general diagram of CICD

### Git workflow (stages)

### SDLC workflow (stages)