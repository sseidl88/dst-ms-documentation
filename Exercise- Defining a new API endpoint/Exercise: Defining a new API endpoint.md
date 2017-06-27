> This will walk the developer through the creation and deployment of a new API in the platform `EmployeeService`

1) Invoke existing `EmployeeService` API from a browser.

    http://test.niswonger.us/api/employees
    
![](https://user-images.githubusercontent.com/21327244/27605428-49b6a43e-5b42-11e7-8f5f-b558f4c5a999.png)  

2) Clone the Employee Service Github project: [https://github.com/in-the-keyhole/dst-employee-service](https://github.com/in-the-keyhole/dst-employee-service)

3) Add a new API route by adding the `controller` method shown below to the `com.dst.employee.Api` class. Change the `/yournamehere` route to you name or whatever you would like.
      
    ...  
 
    @ApiOperation(value="This is a new API",notes="Says Hello",response=String.class)
    @RequestMapping(method = RequestMethod.GET, value = "/davidpitt", produces = MediaType.APPLICATION_JSON_VALUE)
    	ResponseEntity<String> hello() {
    	
    		String result = "Hello David";
    		return new ResponseEntity<String>(result, HttpStatus.OK);
    	}

	...

4) Commit and push to the git repository. Here are the commands:

    > git add .
    > git commit 
    > git push 
    
5) If you log into the OpenShift console and check the `build tab`, you can see the build progress after a commit.  [https://openshift.niswonger.us:8443/console/](https://openshift.niswonger.us:8443/console) 

![](https://user-images.githubusercontent.com/21327244/27605461-6b2af1ce-5b42-11e7-8622-d63c4653a6f1.png)

6) After building and deploying, you can invoke your API from a browser with the URL below:

    http://test.niswonger.us/api/davidpitt

7) Changes will be built and deployed. Also, the new API Swagger documentation publishes to the API wiki. You should see it here after it finishes building.

#### [Link to EmployeeService API Documentation](https://dst.grokola.com/#search/command/1)





