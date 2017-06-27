> Swagger documentation is automatically published to `GrokOla`. 

#### Uses The Open Source Spring 
Starter Project: [https://github.com/in-the-keyhole/khs-spring-boot-publish-swagger-starter](https://github.com/in-the-keyhole/khs-spring-boot-publish-swagger-starter)

Apply the `@PublishSwagger` annotation in the Projects Spring Boot main method class.

    @PublishSwagger
    @SpringBootApplication
    @EnableApiStatistics
    public class EmployeesApp {
    
    	public static void main(String[] args) {
    		SpringApplication.run(EmployeesApp.class, args);
    	}
    }

Configuration is defined in `application.yml`. 

    swagger:
      publish:
        publish-url: https://dst.grokola.com/swagger/publish/1
        security-token: c67d90d0-1284-48e3-8b4d-718b48e20695
        swagger-url: http://127.0.0.1:${server.port}/v2/api-docs


API will be published to the GrokOla wiki platform.

#### Here is a [LINK TO The Published Service API](https://dst.grokola.com/#search/command/1)
