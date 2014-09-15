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
%> gw3 GLOBAL_OPTIONS offline OPTIONS -m <model-file> GENERATOR(STOP_CONDITION)
~~~

### Options

* --json, -j<br>
Returns data formatted as json.<br>
Default is true

* --model, -m <br>
The model, as a graphml file followed by generator with stop condition.<br>
This options can occur multiple times.<br>
[Read more about path generators and stop conditions](path_generators_and_stop_conditions)

* --restful, -r<br>
Starts as a Restful API service.<br>
Default is true.

* --unvisited, -u<br>
Will also print the remaining unvisited elements in the model.<br>
Default is false.

* --verbose, -o<br>
Will print more details<br>
Default is false.

### Examples

~~~
%> gw3 offline -m model.graphml random(edge_coverage(100))
~~~
Use the model ***model.graphml***, and generate a path using the random path generator, and stop when the edge coverage is 100%


## online

Online testing means that a model-based testing tool connects directly to an SUT and tests it dynamically.