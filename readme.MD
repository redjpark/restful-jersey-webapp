# use the following archetype to create maven project for webapp

```
% mvn archetype:generate -DarchetypeArtifactId=jersey-quickstart-webapp -DarchetypeGroupId=org.glassfish.jersey.archetypes -DinteractiveMode=false -DgroupId=com.example -DartifactId=simple-service-webapp -Dpackage=com.example -DarchetypeVersion=2.22.1 -s ~/.m2/settings-local.xml

% cd simple-service-webapp
% mvn clean package -s ~/.m2/settings-local.xml
```
# Import into Eclipse
Eclipse > Project > Import ... > Maven > Existing Maven Projects

# Run on Server

Make sure the webapp from the archetype is working correctly.

* Project > Run As > Run on Server > Apache 8
* http://localhost:8080/simple-service-webapp/
* click no like: 'Jersey Resource' on the page
* Or visit http://localhost:8080/simple-service-webapp/webapi/myresource

You can view WADL by:
* http://localhost:8080/simple-service-webapp/webapi/application.wadl

If you want to getnerate java code from WADL
* https://wadl.java.net/wadl2java.html

# Modify the project to use Jersey 3

## Add the Application class

```
// src/main/java/com/example/RestApp.java
package com.example;

import java.util.Set;

import javax.ws.rs.core.Application;

@javax.ws.rs.ApplicationPath("webapi")
public class RestApp extends Application {
	
	@Override
	public Set<Class<?>> getClasses() {
		Set<Class<?>> resources = new java.util.HashSet<>();
		resources.add(com.example.MyResource.class);
		return resources;
	}

}
```


## Empty out web.xml
* Edit src/main/webapp/WEB-INF/web.xml and comment out the entire content

## Fix up pom.xml to use Jersey 3
```
        <dependency>
            <groupId>org.glassfish.jersey.containers</groupId>
            <!-- <artifactId>jersey-container-servlet-core</artifactId> -->
            <!-- use the following artifactId if you don't need servlet 2.x compatibility -->
            <artifactId>jersey-container-servlet</artifactId>
        </dependency>
```


## Run on Server
* Project > Run As > Run on Server > Apache 8
* http://localhost:8080/simple-service-webapp/
* Click on the link 'Jersey Resource' on the page
* http://localhost:8080/simple-service-webapp/webapi/myresource
