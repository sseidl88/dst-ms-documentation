> Consists of the Spring Boot framework along with `Spring/Netflix` OSS frameworks.

#### Parent POM.xml

	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>1.5.2.RELEASE</version>
	</parent>

Services are built as Spring Boot applications. When started from a `Java Main` method they boot up an application server. Here is a Spring Boot Main method:

    @PublishSwagger
    @SpringBootApplication
    @EnableCircuitBreaker
    @EnableApiStatistics
    public class EmployeesApp {
    
    	public static void main(String[] args) {
    		SpringApplication.run(EmployeesApp.class, args);
    	}
	...
	
Notice the `annotations` as a lot of Spring Magic happens through them.	
