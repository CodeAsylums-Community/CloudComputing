# This is the completed task detail.

## I have created an automated CI CD pipeline using jenkins(not jenkins pipeline) and DigitalOcean Iaas
    Here I have used three VM to create the pipeline 
        * Jenkins server
        * Staging Server
        * Production server

## HOW to test the CI CD pipeline
1. make changes and push the desired code in the repository [codeasylum_fellowship_website] (https://github.com/GlitchBrain/codeasylum_fellowship_website) (**note I could make codeasylum_fellowship_website to directly work for this repository but I am not sure how to the webhooks will work then**) also to push the code you require my account credentials[].

2. Enter the jenkins server at http://157.230.191.146:8080/ `username: karan` and `password: codeasylum123@` to observe the workflow/jobs success and see the nodes and jobs i have created. 

3. when "built website" job is finished observe the changes in the Staging Server at http://67.207.90.154:82/.

4. when "push_production" job is finished observe the changes in the Production Server at http://192.241.131.214/

## The CI CD pipeline structure 
    **Github code push** -->
                **Jenkins/Master Server**(1st DigitalOcean droplet) -->
                                         **code build**/tested but not in this task(2nd DigitalOcean droplet) -->
                                                             **code push to production server**(3rd DigitalOcean droplet) 

# HOw the CI CD pipeline works 
    The pipeline has 3 jobs and 2 nodes
    > the "git-job" which upon getting a webhook starts downloading the latest code in the site folder `/root/jenkins/workspace/git-job` then the next job "build website" is started, the "git-job" is performed under the "Staging" node in the 2nd droplet.

    > the "build website" jobs starts and performing the DOCKERFILE from the repo which create a container of apache server and add the others files from `/root/jenkins/workspace/github/` to the `/var/www/html/` this is done by the built in commands in the job config, the "build website" is performed under "Staging" node in the 2nd droplet.                                                     

    > upon completion of "build website" job the "push_production" jobs starts performing where the code from github repo is again copied in the same file structure as "git-job" and similar docker commands are run as "build website"
    this job is performed under "production" node in the 3rd droplet 

# Steps taken to create the whole project
    1. Create 3 DigitalOcean droplets/VM of ubuntu image with 1GB ram/cpu, 20 GB storage, a SSH key using puttygen commands.

    2. Installing docker,java -version 8 in all the VM.

    3. Installing Jenkins in the 1st VM and setting required ports.

    4. Setting Jenkins initial setup then making two nodes "Staging" and "production". Then downloading the agents for the nodes
        and uploading the agents in the VM of 2nd and 3rd droplet using filezilla.
        * activate agents in the 2nd and 3rd VM respectively.

    5. creating the first job "git-job" adding webhooks token in the job and making the post built job to "build website"
        * Setting up a new github repository adding index.html and DOCKERFILE
        * create an webhook from github repo settings.
        * adding tokens in the job config.

    6. Creating 2nd job "build website" which executes some docker command ***which deletes old containers and built newly
        committed code in a new container*** after which "push_production" job is put in the scheduler. This change can be seen in [staging server] (http://67.207.90.154:82/)
        * added docker commands which deletes old container and build the DOCKERFILE
        * perform 3rd job "push_production" only when the build is stable

    7. Next creating 3rd job "push_production" which takes place in the production node of 3rd VM. Where we perform:
        * adding newly committed code from github
        * performing docker commands similar to 2nd job. Upon which we can observe the changes in the [production server]
        (http://192.241.131.214/) 

    **note while performing these many times error occurred specially with ports and github branches which is solved upon googling**

## requirements
    **Html** **Docker** **apache**
