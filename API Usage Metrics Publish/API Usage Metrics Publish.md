> API usage statistics are published to a GrokOla instance.

#### Uses the Open Source Spring 
Starter Project: [https://github.com/in-the-keyhole/khs-spring-boot-publish-swagger-starter](https://github.com/in-the-keyhole/khs-spring-boot-api-statistics-starter) 

Apply the `@EnableApiStatistics` to the Spring Boot `main` method.

    @PublishSwagger
    @SpringBootApplication
    @EnableApiStatistics
    public class EmployeesApp {
    
    	public static void main(String[] args) {
    		SpringApplication.run(EmployeesApp.class, args);
    	}
    }
    
Configuration is defined in `application.yml`. 

    api:
      statistics:
        name: employeeapi
        pattern-match: /api/.*
        publish-url: https://dst.grokola.com/sherpa/api/stats/7
        token: c67d90d0-1284-48e3-8b4d-718b48e20695 

API will be published to the GrokOla API wiki.
    
#### Here is a [LINK TO The Project Service API STATS](https://dst.grokola.com/#api/stats/6)
