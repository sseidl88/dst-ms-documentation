> Development of a user interface will typically just require local installation of the API Gateway and the ability to serve up static content. Services utilized will be deployed to a platform.

#### Port Forwarding Allows a Local API Gateway to Access Platform Services

From an OC command shell, run the following commands to forward API Gateway calls to the OpenShift platform:

    > ./oc port-forward employee-service-27-ku2dw 8082:8080
    > 
