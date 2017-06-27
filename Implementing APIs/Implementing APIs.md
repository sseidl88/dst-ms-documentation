> The Spring MVC framework is use to implement Restful API controllers 

Here's an example of the EmployeeService API that returns all employees as a JSON object. 

    @RestController
    @RequestMapping("/api")
    public class Api {
    
    	@Autowired
    	private EmployeeService employeeService;
    
    	@RequestMapping(method = RequestMethod.GET, value = "/employees", produces = MediaType.APPLICATION_JSON_VALUE)
    	ResponseEntity<Iterable<Employee>> employees() {
    		Iterable<Employee> employees = employeeService.readAll();
    		return new ResponseEntity<Iterable<Employee>>(employees, HttpStatus.OK);
    	}
    	
    ...


`RestController's` interact with `service` implementations. 

You can invoke this api from the platform with the following `URL` in a browser, 






![](https://user-images.githubusercontent.com/21327244/27604280-7a769740-5b3e-11e7-80f8-85e59caa23ea.png)
