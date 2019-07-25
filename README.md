# mySpringCloud
# bug
* when use spring cloud config to get properties remotely, 
the validations on GatewayProperties.class and my own class won`t work 
even there is nothing in my remote config file.
But HeartbeatProperties.class does validation.
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