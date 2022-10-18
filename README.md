
# Publish your Java artifacts (.ear, .jar, .war) to Nexus 3 using Jenkins and Maven

I have created a _docker compose_ file which comes with Nexus and Jenkins. Let's take into considerations these assumptions and details about how the example works:

+ You have docker and docker-compose installed properly.
+ Jenkins will create the maven 2 (hosted) repository in Nexus on the startup script.
+ Any _.groovy_ file you placed under __/var/jenkins_home/init.groovy.d/*.groovy__ will be automatically executed. So you will find a job that is executed which is in charge to 
create the Nexus repository. This is a chance to review how to use Jenkins Rest API operations and Script operations in Nexus.


## How does it works?

Jenkins already have defined these items defined in the configuration as code file:

+ _nexus-push_: Jenkins pipeline example which will __build__ the Java artifact and push it to Jenkins.
+ _nexus-create-repo_: Jenkins pipeline which will run every time Jenkins is started and will try to create the Nexus repository.
+ Credential __nexus-credentials__ to login to use the rest API and the Nexus Jenkins plugin to push artifacts.
+ Maven tool to use it in the Pipeline, I called it __Maven 3.6.0__
+ Two jobs defined using DSL.

### Let's start

Clone the project. Start docker-compose application:
```
docker-compose up
```
And that's it! You are ready to explore Jenkins in port 8080 and run the job.
Jenkins has a capability which allow you to run Groovy code whenever Jenkins is started.

The script basically build an existing job which is defined in the Jenkins configuration as code file with name: _nexus-create-repo_.

### Let's try it out!
So easy as going here:

http://localhost:8080/job/nexus-push 

and build it! Enjoy the logs!


