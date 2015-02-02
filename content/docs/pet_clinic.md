/*
Title: Pet Clinic Example
Description: This description will go in the meta description tag
*/

# Pet Clinic Example

This is an example on how to implement a test using the [PetClinic Sample Application](https://github.com/spring-projects/spring-petclinic/). 

## Pre-requisites
* Java JDK installed (preferably 8)
* Maven installed (version equal or greater than 3.2.3)
* git installed
* Firefox installed

## Get and start the PetClinic Sample Application
```
git clone https://github.com/SpringSource/spring-petclinic.git
mvn tomcat7:run
```
**If you are usning Java8** please see this issue: [fix for JasperException when java8 is used #51](https://github.com/spring-projects/spring-petclinic/pull/51/files), apply the fix.

## Get and run the GraphWalker test example
```
git clone https://github.com/GraphWalker/graphwalker-example.git
cd graphwalker-example/java-petclinic
mvn graphwalker:test
```

## The test
The tests is designed using [yEd](http://www.yworks.com/en/products/yfiles/yed/). The test design is divided between 5 models.
