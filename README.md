# mySpringCloud
# bug
* when use spring cloud config to get properties remotely, 
the validations on GatewayProperties.class and my own class won`t work 
even there is nothing in my remote config file.
But HeartbeatProperties.class does validation. As you can see the config about gateway.routes in 
bootstrap-dev.yml is illegal obviously, but the application start successful.
* the myGateway-dev.yml in /resources is the remote config file in my remote config server.
* When debug the application, I found the  HeartbeatProperties has been 
initialized twice, the fist one with ValidationBindHandler.class as bind handler,
which will do the validations in onFinish(), the second one with ConfigurationPropertiesBinder.class
as handler which do nothing in onFinish();
* In this test application, when I don`t use the spring-cloud-config(not use 
the dependencies), the 
validations on GatewayProperties.class work properly.
* conclusion: 
    * Are there any faults in my test application config ?
    * or is there any Incompatible between Spring-cloud-gateway and config ?
    * Why the HeartbeatProperties.class will be initialized twice in ConsulDiscoveryClientConfiguration.class
    and how to realize this ?
* version:
    * springBootVersion : 2.1.2.RELEASE
    * springCloudVersion : Greenwich.RC2
* Thanks for your concerns!
# Minimize
* When minimizing the application, I found the validation bug was cause by dependency on  
'org.springframework.cloud:spring-cloud-starter-bus-kafka'.When add this dependency and config
'Spring.kafka' properly, validations on GatewayProperties not work.
* 'bootstrap-dev.yml' is the minimum config to reproduce this error. The kafka is a default 
instance run in local.