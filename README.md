# Spring Cloud Config Service 




## Runnign the Spring Cloud Config Service

Hi, this is a simple Spring Boot app configured to act as a Spring Cloud Config Service. It serves up configuration files from a Git repository
for microservices that identify themselves with a logical name, e.g.: `foo`, from a property file `foo.properties`. All microservices, no matter what their names, 
return information from `application.properties`. So, every microservice should get two sets of configuration: `application.properties` and the configuration from the specific file for that microservice, too.

Given a microservice named `my-service`, you could get the configuration for that microservice [from this URL](http://localhost:8080/my-service/default).

You can build a Docker container out of the Spring Boot Config Server with `./gradlew bootBuildImage`. It'll take about a minute and then dump out a Docker image name at the end of the output. 

Here's how you'd run that Docker image given the docker name. You can use environment variables to override the URL for the Git config server:

`docker run <IMAGE_NAME>   -e SPRING_CLOUD_CONFIG_SERVER_GIT_URI=https://github.cm/blah/blah `
 
 That URL is the Git repository from which the Config Server draws its configuration. It needs to be a Git repository. The default I've written in the code points to a Git repository on the local Desktop.  But, it could be anything. A Github URL. Gitlab. etc. etc. 
 
 
## Sourcing the Configuration 

The Git repository needs to have either `.properties` or `.yaml` files, named for the service, or just `application.properties` or `application.yaml`. 

So, given a repository:

```shell
application.properties
a.properties
b.properties
```

Then, if a microservice identifying itself as `a` connects, it would get the properties from both `a.properties` and `application.properties`.
