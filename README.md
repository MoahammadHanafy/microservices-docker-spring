# microservices-docker-spring
This Project was motivated by the following work
https://dzone.com/articles/buiding-microservice-using-springboot-and-docker

The Project Implements a simple microservice app that is deployed on docker, the application consists of 1) Gateway service, 2) service discovery service, 3) a config service and 4)a servie that calls another service to show inter-service communincation.   

Below are some Notes that could help in understanding some concepts of microservices:

##Notes
===========================================================================
Microservices main pillars are:
1- Config service:  
	 - It is used to store all configurations of all services to prevent serives down when config changes.
	 - It should be highly available (not SPF-Single point of failure-).
	 - One examlpe is "Spring cloud config" arcgitecture that :
		- It provides the configuration through REST end point.
		- It registers each service with a unique Id.
		- It uses version control repository(serve dev,test,prod,..).
		- It usesactuator(to not need restart when config changes).
		- It refreshes the configuration either indiviually (call /refresh) or for all through (Cloud Bus).

2- Discovery service:
	- Miscroservicces components are many and spwaned dynamically on the fly with different IPs and endpoints so we need a service that keep to track of the changed to our components.
	- Microservice components register themselvies or manager removes them when they are not available.
	- It should be highly available (not SPF).
	- One example is "Eureka" Discovery server:
		- It is a microservice that every other service registers itself during the bootstrap.
		- It bings the registered services to assure that they are available.
		- It can be used in service-to-service communication.

3- Components:
	- They are the services that are running and communicate with eachother to provide the functionality of our app.
	- They have a defined API to be dealed with.

4- Gateway Service:
	- A service that is a facade to all our application
	- We may configure our security on this layer
	- It makes client avoid CORS
	- It provides server side load balancing and routing
	- One Example of such is Zuul
	
==================================================================================================================
Fiegn Client:
	Fiegn client (Rest client) is another tool from netflix to enable service-to-service communication
hystrix:
	Is a circuitbreaker (framwork setteled between caller and calle services if reposne time exceded certain time it stop all further calls for certain time to allow the calle to recover)
