> The Swagger specification (i.e. OpenAPI) provides API documentation.

### Swagger Generation 

The [Spring Fox](http://springfox.github.io/springfox) framework is used to glean API patterns from Spring `@RestControllers`.

Here is a partial implementation of the `EmployeeService` API implementation. 

    @RestController
    @RequestMapping("/api")
    public class Api {

         ...
  
    @RequestMapping(method = RequestMethod.GET, value = "/employees", produces = MediaType.APPLICATION_JSON_VALUE)
        ResponseEntity<Iterable<Employee>> employees() {
        	Iterable<Employee> employees = dao.readAll();
        return new ResponseEntity<Iterable<Employee>>(employees, HttpStatus.OK);
        }
    
           ...

### Swagger Java Configuration for the `EmployeeService` is shown below. 

    @Configuration
    @EnableSwagger2
    public class SwaggerConfig {
    
    	@Bean
        public Docket apiDocket() {
            return new Docket(DocumentationType.SWAGGER_2)
                    .apiInfo(apiInfo())
                    .select()
                    .paths(regex("/api.*"))
                    .build();
        }
         
        private ApiInfo apiInfo() {
            return new ApiInfoBuilder()
                    .title("Employee Service")
                    .description("An employee bounded context example for DST Microservice Reference.")
                    .contact(new Contact("DST", "dst.com", "dpitt@keyholesoftware.com"))
                    .version("2.0")
                    .build();
        }
    }
