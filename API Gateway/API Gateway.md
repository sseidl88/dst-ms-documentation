> The role of the API gateway is to `synthesize` service calls into a specific purpose API (i.e. SPA user interface).

Github Repository: [https://github.com/in-the-keyhole/dst-api-gateway](https://github.com/in-the-keyhole/dst-api-gateway)

![](https://user-images.githubusercontent.com/21327244/27604075-e227c3ce-5b3d-11e7-892f-6315a840e3d4.png)

The reference application API Gateway is implemented as a Spring Boot Application MVC application with REST controllers.

The API snippet below shows how the `/projects/{id}/resources` accesses the `EmployeeService` to full fill a `ProjectResource` request for the API.


    @RequestMapping(method = RequestMethod.GET, value = "/projects/{id}/resources", produces = MediaType.APPLICATION_JSON_VALUE)
    ResponseEntity<Resources<ProjectResource>> projectResources(@PathVariable("id") Long id) {
  
    ResponseEntity<Resources<ProjectResource>> responseEntity = projectService.projectResources(id);
    Resources<ProjectResource> projectResources = responseEntity.getBody();
    Iterable<ProjectResource> resources = projectResources.getContent();
    
    for (ProjectResource projectResource : resources) {
  
    Employee employee =      employeeService.employee(projectResource.getEmployeeId());
    	projectResource.setEmployee(employee);
    		}
    Resources<ProjectResource> returnEntity = new Resources<ProjectResource>(resources);
    return new ResponseEntity<Resources<ProjectResource>>(returnEntity, HttpStatus.OK);
    	}
  
    }
