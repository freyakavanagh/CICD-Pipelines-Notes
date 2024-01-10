# Jenkins CICD

## Continous Intigration

The aim is to test the code before changes made on the dev branch are pushed to main.<br>

![](../ReadMeImages/CI.jpeg)

## Continous Delivery

Slower, as the deployment is manual. <br>
Delivers code that is ready to be deployed: in the form of artifacts e.g. jar file 

## Continous Deployment

Faster to get to users, as the deployment is automated.<br>
But may be more issues for the end user.<br>
Users have to understand that they need to report ongoing feedback to the developers. (a culture)

## CICD Pipeline

![](../ReadMeImages/CICDpipeline.jpeg)

1. git push on the dev branch (trigger for the pipeline), github recieves the info
2. GitHub notifies Jenkins (webhook = when one service notifies anther service of a change) that there has been a change on the dev branch (Jenkins is listening for any changes)
3. Test the dev branch code
4. If tests pass, merge to main branch
5. Deploy the changes to AWS (update the code on the EC2 instance)

- For complex pipelines you might have many stages with multiple jobs within them.
- Jobs run conncurently

- Steps 3 and 4 are the continous intigration part
- Step 5 is the Continous Deployment.

### Why Pipeline?

- automation
- code quality
- saves time
- get the useable software into the hands of the end users (most important reason) - then can create value for a bussiness

## Jenkins

### Why Jenkins?

- Open-source and free
- Powerful plugins
- large community so many plugins
- industry standard, robust, been around a long time

## Jenkins CICD Overview

1. Push dev branch to main branch on GitHub using SSH
2. GitHub will then notify Jenkins that a change has been made with a Webhook notification (Jenkins is listening)
   - Jenkins is made up of...
   -  the master mode/ built-in node: runs on its own virtual machine, can run jobs but not reccomended as it is not as expendable as the agent nodes
      -  Spins up/uses agent nodes
   -  agent nodes: as many as neccessary to run the jobs
3. Jobs
   1. test the code in the dev branch (test if it compiles), if succesful... 
   2. merge dev to main
   3. deploy the updated code to the EC2 instance on AWS
      Jenins will have to merge code on main branch, will need to SSH into both GitHub and the EC2 instance (.pem file)

## Jenkins CICD Pipeline Detailed Steps

1. Create key pair
   - freya-jenkins-2-github-jsonvh
2. Public key to github
   - allow write access so we can merge the branches
3. Log in to jenkins (server 2)... credentials

### Job 1

1. New Item
   
![](../ReadMeImages/creatingajob.png)

   - name = freya-jsonvh-job1-ci-test
   - freestyle project
   - desc: To test the jsonvh app
   - discard all builds, max 3
   - Check GitHub project, add HTTP url from GitHub repo: https://github.com/freyakavanagh/tech242-jsonvoorhees-app.git
   - Source code management: Git
      - URL: git@github.com:freyakavanagh/tech242-jsonvoorhees-app.git
         - Go to git hub rep and click 'code' and copy the SSH
   - Add credentials...

![](../ReadMeImages/jenkins-credentials.png)

   - Kind: SSH username with private key
   - ID: freya-jenkins-2-github-jsonvh
   - Desc: read/write to repo
   - Username: freya-jenkins-2-github-jsonvh
   - enter directly
   - Then select from the credentials list
   - Branch specifier: */main
   - Build Steps
      - Invoke top level maven targets
         - version e.g. 3.6.3
         - Goals: package test (to rerun and test the code)
          - Advanced
            - POM:pom.xml
1. Run the job on the dashboard to test

![](../ReadMeImages/jenkins.png)

### Set up Webhook to trigger job 1

1. In job1 configure
2. Build Triggers
3. Check GitHub hook trigger for GITScm polling
4. Change Branch specifier: */dev

On GitHub...

1. Go to the chosen repo
2. Settings
3. Webhooks
4. Add Webhook
   - Payload URL: http://52.31.15.176:8080/github-webhook/ (IP + port of jenkins server dashboard + github-webhook) 

![](../ReadMeImages/github-webhook.png)

In terminal...

1. Clone git repo to machine (using ssh)
2. git branch dev
3. git checkout dev
4. Go to readme file (nano README.md)
   - add something inside e.g. ##checking 
   - Control o and enter (to save)
   - Control x (to exit)
5.  git add .
6.  git commit -m "changed readme"
7.  git push origin main

On GitHub...

1. Check to see if it has pushed

On Jenkins...

1. Check to see if the job has been triggered

### Job 2

1. Add item 
2. name = freya-jsonvh-job1-ci-test
   - freestyle project
3. desc: To test the jsonvh app
   - discard all builds, max 3
  
![](../ReadMeImages/job2part1.png)



4. Check GitHub project, add HTTP url from GitHub repo: https://github.com/freyakavanagh/tech242-jsonvoorhees-app.git
5. Source code management and select: Git
   -  Repository URL: git@github.com:freyakavanagh/tech242-jsonvoorhees-app.git (SSH)
6. Jenkins source code management
7. Select the matching credentials 
8. In the "Branches to build" section, Branch Specifier = "*/dev"
   
![](../ReadMeImages/job2part2.png)   
![](../ReadMeImages/job2part3.png)
9.  Click "Add additional behaviours" and select "Merge before build"
10. Enter Name of repository = origin
11. Branch to merge to = main
12. Jenkins additional behaviours
13. Add post-build action, select Git publisher
14. Tick Push Only If Build Succeeds and Merge Results

![](../ReadMeImages/job2part4.png)

15. Click save

### Allowing Job 1 to Trigger Job 2

17. Navigate to the configure section for job 1
18. Scroll to the bottom, click "Add post-build action" and select "Build other projects"
19. Choose job 2 and set to "Trigger only if build is stable"

![](../ReadMeImages/triggerajob.png)







