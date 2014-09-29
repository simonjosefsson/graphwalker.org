/*
Title: The workflow using GraphWalker
Description: This description will go in the meta description tag
*/

# Workflow - This is how you would work using GraphWalker
This article will describe a normal workflow when designing for test automation using GraphWalker. There are 3 main steps involved:

* Test idea
* The design
* Writing the test code
* Running the test. 

## Test idea and design
The purpose of the test design is to describe the **expected behavior of the system under test**. The way it works, is that you in a finite state diagram [model], express an action as a directed edge. An edge is alson known as an arrow, arc or transition. The edge points to a vertex. Also known as a node or state, where the results or the consequence of the previous action is verified/asserted.

### Test idea
Our test idea, is to write a regression test for the Spotify Desktop Client, more sepcifically, the feature **login**. (<a href="http://en.wikipedia.org/wiki/Spotify">Spotify is a music streaming business</a>)

The feature is suppose to work  like this:
* In a freshly installed client, and the client is started, the Login dialog is expected to be displayed.
* The user enters valid credentials and the client is expected to start.
* If the user quits, or logs out, the Login dialog is displayed once again.
* If the user checks the **Remember Me** chackbox, and logs in (using valid creds), the client starts, and, nect time the user starts the client, it will start without displaying the Login dialog.

A model, would look something like this:

<a href="http://www.flickr.com/photos/36681632@N00/8380189446/" title="simpleLogin by kristian_karl, on Flickr"><img alt="simpleLogin" height="240" src="http://farm9.staticflickr.com/8213/8380189446_8dc6a91076_m.jpg" width="172" align="left"></a>

**1.** The Start vertex is where the tests starts. (Duh!)

**2.** In e_init, we remove all cache.

**3.** v_ClientNotRunning will assert that there is no client process running.

**4.** e_Start start the client

**5.** v_LoginPrompted asserts that the login dialog is displayed and correctly rendered.

**6.** e_ValidCredentials enters valid user name and password in appropriate input fields, and clicks the Sign In button.

**7.** v_WhatsNew asserts that the What's New page is correctly displayed.

### Test automation code
This is the programming part. Using Java  and libraries like Selenium or Sikuli (or other), you implement the code that will be clicking the buttons, selecting menus, or making REST-calls. But also, verifying and asserting that your system under test is behaving correctly.

<img alt="A model of the login feature on the Spotify desktop client" src="http://farm9.staticflickr.com/8507/8367918574_75c29a2a78.jpg" style="width: 500px; height: 227px;" align="left">

* Click on the model above, and save the Login.graphml file locally on your computer.
* Download the latest GraphWalker standalone jar. Pick graphwalker-N.N.NN-SNAPSHOT-standalone.jar, and copy it to the same folder as the Login.graphml file.
* Download the source code template file ModelAPI.template, and copy it to the same folder as the Login.graphml file
* Now, open a console/terminal, change current directory into the folder where your files from above are, and enter following command:

~~~
java -jar graphwalker-2.5.18-SNAPSHOT-standalone.jar source -f Login.graphml -t ModelAPI.template
~~~

This will print stub source code to the terminal. If you want to save it directly to a file, add: " > Login.java" to the end of the command (skip the quotation marks).

Of course, you need to fill in the missing code into the methods. First you have to find the right tool for the job. If it's the web, maybe the Webdriver from Selenium is your choice.  See the demo, where the webdriver is put into good use.

### Running the test
GraphWalker, has the capability to to traverse through a model using differently strategies and stop criteria. Using different combination, we can create different test types, like Smoke Test, Functional Test or a Stability Test to determine reliability and resource usage, but still using exactly the same model and code!

### Smoke test example
A model of the login feature on the Spotify desktop client

Consider the model above.It's a model of the login feature of the Spotify desktop client. 

We will use the same model [/model/Login.graphml], and code [class Login]  in all three examples. In this case we use:

* a generator A_StarPathGenerator, which will generate the shortest path through the model (given the stop criteria).
* a stop criteria ReachedVertex, which will stop the walk when we reach the specified vertex.
Using this combination of generator and stop criteria, GraphWalker will generate a short walk through the model, calling following methods in the class Login in this order:

~~~
e_Init
v_ClientNotRunning
e_StartClient
v_LoginPrompted
e_ValidPremiumCredentials
v_WhatsNew
~~~

A Smoke test would look something like this:

~~~
// Instancing GraphWalkers model handler
ModelHandler modelhandler = new ModelHandler();
    
// Get the model from resources
URL url = LoginTest.class.getResource("/model/Login.graphml");
File file = new File(url.toURI());
 
// Connect the model to a java class, and add it to graphwalker's modelhandler.
// The model is to be executed using the following criteria:
// EFSM: Extended finite state machine is set to true, which means we are using the data domain
// in the model
// Generator: a_star, we want to walk through the model using shortest possible path.
// Stop condition: Stop when we reach vertex v_WhatsNew.
modelhandler.add("Login", new Login(file, true, new A_StarPathGenerator(new ReachedVertex("v_WhatsNew")), false));
 
// Start executing the test
modelhandler.execute("Login");
 
// Verify that the execution is complete, fulfilling the criteria from above.
Assert.assertTrue(modelhandler.isAllModelsDone(), "Not all models are done");
 
// Print the statistics from graphwalker
String statistics = modelhandler.getStatistics();
System.out.println(statistics);
~~~
 
### Functional test example
We are still using the same model [/model/Login.graphml], and code [class Login] as above. But, in this case:

* The generator is changed from A_StarPathGenerator to RandomPathGenerator, which will walk to model in an upredicted way.
* Stop criteria is changed from ReachedVertex to EdgeCoverage, which guarantees the we will coverer the complete model.

Using the RandomPathGenerator, will give us the benefit of generating a path through the model, which is not exactly the same path we used before. A different permutation will increase the test coverage, given if we run the test frequently.

~~~
// Connect the model to a java class, and add it to graphwalker's modelhandler.
// The model is to be executed using the following criteria:
// EFSM: Extended finite state machine is set to true, which means we are using the data domain
// in the model
// Generator: random, walk through the model in a random manor.
// Stop condition: Stop when we have covered all edges at least once
modelhandler.add("Login", new Login(file, true, new RandomPathGenerator(new EdgeCoverage(1.0)), false));
~~~

### Stability test example
We are still using the same model [/model/Login.graphml], and code [class Login] as above. But, in this case:

* The stop criteria is changed from EdgeCoverage to TimeDuration, and a time set to 10 hours.

This combination will walk around the model and execute the test for 10 excruciating hours.

~~~
// Connect the model to a java class, and add it to graphwalker's modelhandler.
// The model is to be executed using the following criteria:
// EFSM: Extended finite state machine is set to true, which means we are using the data domain
// in the model
// Generator: random, walk through the model in a random manor.
// Stop condition: Stop when we reach vertex v_WhatsNew.
modelhandler.add("Login", new login(file, true, new RandomPathGenerator(new ~~~
TimeDuration(10*3600)), false));
~~~
