/*
Title: A quick startup guide
Description: This description will go in the meta description tag
*/

# A quick startup guide

This will show how to create a small test. We will not implement the test, I leave that as an exercise to the reader.


## Download and install the dependencies

 * Install the Java, 7 or 8 will do
 * Install the [Maven](http://maven.apache.org/download.cgi)
 * Install the [yEd editor](http://www.yworks.com/en/products_yed_about.html)
 * Download the latest GraphWalker standalone jar file.

## Create a boilerplate project
From the command line, run:
~~~
%> mvn archetype:generate -B -DarchetypeGroupId=org.graphwalker \
       -DarchetypeArtifactId=graphwalker-maven-archetype \
       -DarchetypeVersion=3.0.0-SNAPSHOT -DgroupId=com.company -DartifactId=myProject
~~~
Move into the myProject folder, and test the project:
~~~
%> cd myProject
%> mvn org.graphwalker:graphwalker-maven-plugin:3.0.0-SNAPSHOT:test
~~~
You now have a complete GraphWalker 3 project.

That last command did a couple of special things.

* It generated an interface **SmallTest**, from the model **SmallTest.graphml**. Any time the model is changed, the interface will be automatically re-generated when the maven goal **org.graphwalker:graphwalker-maven-plugin:3.0.0-SNAPSHOT:test** is run. This helps the developer to keep the code in sync with the model(s). The requirement is that the graphml file needs to be in folder path, which is the same (package) path as for the java project, but under resource path instead.
<img src="/pico/content/images/folderPaths.png" alt="Folder paths">
* The test is itself is quite simple. When opened in the yEd editor, it will look like below.

<img src="/pico/content/images/SmallTest.png" alt="Small test model" height="30%" width="30%">

* The class **SomeSmallTest** implements the interface **SmallTest**. Remember that that interface is auto-generated, and it's in the maven created **target** folder. The complete path is **target/generated-sources/graphwalker/com/company/SmallTest.java**. Below are the two classes.

<img src="/pico/content/images/SmallTestInterface.png" alt="SmallTest Interface">
<img src="/pico/content/images/SomeSmallTestJava.png" alt="SomeSmallTest Class">


## Running the test
When running the the test the output might look something like this:
~~~
[INFO] ------------------------------------------------------------------------
[INFO]   _____             _   _ _ _     _ _                                   
[INFO]  |   __|___ ___ ___| |_| | | |___| | |_ ___ ___                         
[INFO]  |  |  |  _| .'| . |   | | | | .'| | '_| -_|  _|                        
[INFO]  |_____|_| |__,|  _|_|_|_____|__,|_|_,_|___|_|                          
[INFO]                |_|         (3.0.0-SNAPSHOT)                            
[INFO] ------------------------------------------------------------------------
[INFO] Reflections took 1178 ms to scan 52 urls, producing 2128 keys and 8117 values 
[INFO] Configuration:
[INFO]     Include = [*]
[INFO]     Exclude = []
[INFO]      Groups = [*]
[INFO] 
[INFO] Tests:
[INFO]     SomeSmallTest(RandomPath, VertexCoverage, "")
[INFO] 
[INFO] ------------------------------------------------------------------------
Running: e_AnotherAction
[INFO] State changed [e_AnotherAction]
Running: v_VerifySomeOtherAction
[INFO] State changed [e_AnotherAction -> v_VerifySomeOtherAction]
Running: e_SomeOtherAction
[INFO] State changed [v_VerifySomeOtherAction -> e_SomeOtherAction]
Running: v_VerifySomeOtherAction
[INFO] State changed [e_SomeOtherAction -> v_VerifySomeOtherAction]
Running: e_SomeOtherAction
[INFO] State changed [v_VerifySomeOtherAction -> e_SomeOtherAction]
Running: v_VerifySomeOtherAction
[INFO] State changed [e_SomeOtherAction -> v_VerifySomeOtherAction]
Running: e_SomeAction
[INFO] State changed [v_VerifySomeOtherAction -> e_SomeAction]
Running: v_VerifySomeAction
[INFO] State changed [e_SomeAction -> v_VerifySomeAction]
[INFO] ------------------------------------------------------------------------
[INFO] 
[INFO] Result :
[INFO] 
[INFO] Tests: 1, Completed: 1, Incomplete: 0, Failed: 0, Not Executed: 0
[INFO] 
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 4.398s
[INFO] Finished at: Sun Sep 14 13:17:27 CEST 2014
[INFO] Final Memory: 41M/341M
[INFO] ------------------------------------------------------------------------
~~~
