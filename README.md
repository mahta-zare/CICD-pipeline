Create a droplet on digital ocean and set firewall rules. Open port 22 to connect to the server with ssh and port 8080 to connect to jenkins container.

Install Docker on the server to run Jenkins container.

Run Jenkins container:
```
docker run -p 8080:8080 -p 50000:50000 -d -v jenkins_home:/var/jenkins_home jenkins/jenkins:2.551
```

Open port 8080 and 50000 to access jenkins container, and allow communication between jenkins manager and worker nodes respectively. /var/jenkins_home is the location inside the jenkins container that we connect to volume for backup. 

Jenkins container should be up and running as a docker container and should be accessible on the browser by entering the IP_address:8080.


After accessing Jenkins UI, in settings -> Tools, we add a Maven installation to make Maven commands available in the Jenkinsfile.

We also add our docker hub credentials in settings -> Credentials as "Username with password" type to provide access to docker hub from Jenkins. We do the same with GitHub credentials to access github repositories form Jenkins.

We can also install the Stage View plugin to see the progress of each step stage of the pipeline.


We create a Jenkinsfile that includes build jar, build image, and deploy stages. We also add a script.groovy file and include the functions for these stages inside.

To access GitHub through Jenkins, add GitHub Integration and Authentication plugins.

Create a simple pipeline that uses this GitHub repository as the source code and set the used branch to main.