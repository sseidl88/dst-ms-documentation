> Single requests from the service `Edge` can span multiple process hops. There must be a way to track activity by user request. 

##### Spring Sleuth 

Distributed Session Tracking, from `RestControllers` and `RestTemplate` invocations.

Tracks spans (i.e. RPC calls) with a 64-bit unique id. 

[Link to Documentation](https://cloud.spring.io/spring-cloud-sleuth)

Engaged by adding to the classpath.

The logs shown below are from the API Gateway. Notice the correlation IDs and service names.

![](https://user-images.githubusercontent.com/21327244/27604930-87653f40-5b40-11e7-8002-c953ef8a745d.png)
