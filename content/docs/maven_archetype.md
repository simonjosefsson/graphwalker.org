/*
Title: Creating a boilerplate project using maven archetype
Description: This description will go in the meta description tag
*/

# Creating a boilerplate project using maven archetype

This will show how to create a boilerplate GraphWalker project using the maven archetype.


## Download and install the dependencies

 * Install the Java JDK, 7 or 8 will do
 * Install the [Maven](http://maven.apache.org/download.cgi)
 * Install the [yEd editor](http://www.yworks.com/en/products_yed_about.html)

## Create a boilerplate project
From the command line, run:
~~~
%> mvn archetype:generate -B -DarchetypeGroupId=org.graphwalker -DarchetypeArtifactId=graphwalker-maven-archetype -DgroupId=com.company -DartifactId=myProject
~~~
Move into the myProject folder, and test the project:
~~~
%> cd myProject
%> mvn org.graphwalker:generate-sources
~~~
You now have a complete GraphWalker 3 project.

### About auto-generated sources

The maven command above generated an interface **SmallTest**, from the model **SmallTest.graphml**. This feature helps the developer to keep the code in sync with the model(s). The requirement is that the graphml file needs to be in folder path, which is the same (package) path as for the java project, but under resource path instead.

<figure>
  <img src="/content/images/folderPaths.png" alt="Folder paths">
  <figcaption>The source code layout after the auto source code generation is done.</figcaption>
</figure>

<figure>
  <img src="/content/images/SmallTestInterface.png" alt="SmallTest Interface">
  <figcaption>The auto-generated interface that is created from the model below. The complete path is <code>target/generated-sources/graphwalker/com/company/SmallTest.java</code></figcaption>
</figure>

### The model

The test is itself is quite simple. When opened in the yEd editor, it will look like below.

<figure>
  <img src="/content/images/SmallTest.png" alt="Small test model">
  <figcaption>The model <strong>SmallTest.graphml</strong> that is used for this test.</figcaption>
</figure>

### The test automation code

The class **SomeSmallTest** implements the interface **SmallTest**. The annotation <code>@GraphWalker(start="e_AnotherAction")</code> tells GraphWalker to start the test at the edge <code>e_AnotherAction</code>. The default path generator is the random generator with 100% vertex coverage.

<figure>
  <img src="/content/images/SomeSmallTestJava.png" alt="SomeSmallTest Class">
  <figcaption>The class <code>SomeSmallTest</code> that implements the test.</figcaption>
</figure>


## Running the test
When running the the test the output might look something like this:
~~~
%> mvn org.graphwalker:graphwalker-maven-plugin:3.0.0-SNAPSHOT:test
:
:
:
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
