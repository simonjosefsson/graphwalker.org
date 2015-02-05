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
The tests is designed using [yEd](http://www.yworks.com/en/products/yfiles/yed/). The test design is divided between 5 models. The models can be fiund in folder:
```
src/main/resources/com/company/
```
When opened in yEd, the models will look like this:

### The main model: PetClinic

<img src="https://raw.githubusercontent.com/GraphWalker/graphwalker-example/master/java-petclinic/src/main/resources/com/company/PetClinicSharedState.png" alt="PetClinic" align="left">

### The Find Owners model

<img src="https://raw.githubusercontent.com/GraphWalker/graphwalker-example/master/java-petclinic/src/main/resources/com/company/FindOwnersSharedState.png" alt="FindOwners" align="left">

### The Veterinariens model

<img src="https://raw.githubusercontent.com/GraphWalker/graphwalker-example/master/java-petclinic/src/main/resources/com/company/VeterinariensSharedState.png" alt="Veterinariens" align="left">

### The Owner Information model

<img src="https://raw.githubusercontent.com/GraphWalker/graphwalker-example/master/java-petclinic/src/main/resources/com/company/OwnerInformationSharedState.png" alt="OwnerInformation" align="left">

### The New Owner model

<img src="https://raw.githubusercontent.com/GraphWalker/graphwalker-example/master/java-petclinic/src/main/resources/com/company/NewOwnerSharedState.png" alt="NewOwner" align="left">


