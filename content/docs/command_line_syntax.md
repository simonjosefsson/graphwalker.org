/*
Title: Command line syntax
Description: This description will go in the meta description tag
*/

# Command line syntax

Complete command line syntax manual. For the easy of the readers eyes, the command:
~~~
%> java -jar <path to graphwalker stanalone jar>/graphwalker-cli-3.0.0.jar
~~~
is changed to the alias:
~~~
%> gw3
~~~

## Global options

The global options affect all commands. Some options, like version, exits the program directly.

* --debug, -g<br>
Sets the log level: OFF, ERROR, WARN, INFO, DEBUG, TRACE, ALL.
Default: OFF<br>

* --help, -h<br>
Prints help text

* --version -v<br>
Prints the version of graphwalker

## offline

Offline means generating a test sequence once, that can be later run automatically. Or, just generating a sequence to prove that the model with the path generator(s) together with the stop condition(s) works.

The syntax is:
~~~
%> gw3 GLOBAL_OPTIONS offline OPTIONS -m <model-file> "GENERATOR(STOP_CONDITION)"
~~~
Please note that the ***"GENERATOR(STOP_CONDITION)"*** should be enclosed with double-quotes.

### Options

* --json, -j<br>
Returns data formatted as json.<br>
Default is true

* --model, -m <br>
The model, as a graphml file followed by generator with stop condition.<br>
This options can occur multiple times.<br>
[Read more about path generators and stop conditions](/docs/path_generators_and_stop_conditions)

* --unvisited, -u<br>
Will also print the remaining unvisited elements in the model.<br>
Default is false.

* --verbose, -o<br>
Will print more details<br>
Default is false.

### Examples

~~~
%> gw3 offline -m model.graphml "random(edge_coverage(100))"
~~~
Use the model ***model.graphml***, and generate a path using the random path generator, and stop when the edge coverage is 100%


## online

Online testing means that a model-based testing tool connects directly to an SUT and tests it dynamically. GraphWalker will start as a HTTP REST server. The path to the API is:
~~~
http://HOSTNAME:9999/graphwalker/METHOD_NAME
~~~

### Method names

* ***/hasNext***<br>
Will return true if as long as there are unfulfilled stop condition(s). If all stop conditions are met (fulfilled), *hasNext* will return false.

* ***/getNext***<br>
Will return the next edge or vertex to walk.

* ***/getData?key=VARIABLE_NAME***<br>
Will return the value of the variable *VARIABLE_NAME*.

* ***/setData?script=JAVA_SCRIPT_ACTION***<br>
Will run the *JAVA_SCRIPT_ACTION*. If successful, the call will return "Ok", else an error message. On 1 statement per call.


### Options

* --json, -j<br>
Returns data formatted as json.<br>
Default is true

* --model, -m <br>
The model, as a graphml file followed by generator with stop condition.<br>
This options can occur multiple times.<br>
[Read more about path generators and stop conditions](/docs/path_generators_and_stop_conditions)

* --restful, -r<br>
Starts as a Restful API service.<br>
Default is true.

* --unvisited, -u<br>
Will also print the remaining unvisited elements in the model.<br>
Default is false.

* --verbose, -o<br>
Will print more details<br>
Default is false.

## methods

Generates a list of unique names of vertices and edges in the model.

### Options

* --model, -m <br>
The model(s), as a graphml file.<br>
This options can occur multiple times.

## requirements

Generates a list of unique names of the requirements found in the model.

### Options

* --model, -m <br>
The model(s), as a graphml file.<br>
This options can occur multiple times.

