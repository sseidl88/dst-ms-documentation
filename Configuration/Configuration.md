> Spring Boot Platform Services will obtain `environment` configuration from the Spring Config Server. A Spring Config Server is a way to provide distributed system with external configuration properties.

Here is a [link](https://cloud.spring.io/spring-cloud-config/spring-cloud-config.html) to the Spring Config Server documentation.

`Local` properties are defined in the `application.yml` and `bootstrap.yml` files located under a project's `src/main/resources` folder. 

'Remote' properties are stored in git-based repositories.

Configuration [based upon the development pipeline (i.e. DEV, TEST, PROD, etc...)] is enabled with the following settings in the `bootstrap.yml`. 

The server configuration below shows properties' repositories for local and remote configurations. 

    spring:
      cloud:
        config:
          server:
            git:
              uri: https://github.com/spring-cloud-samples/config-repo
              repos:
                simple: https://github.com/simple/config-repo
                special:
                  pattern: special*/dev*,*special*/dev*
                  uri: https://github.com/special/config-repo
                local:
                  pattern: local*
                  uri: file:/home/configsvc/config-repo
    

