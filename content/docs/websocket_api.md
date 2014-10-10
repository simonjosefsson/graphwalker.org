/*
Title: GraphWalker WebSopcket API
Description: This description will go in the meta description tag
*/

# GraphWalker WebSopcket API (from version 3.2.0)

## Establishing a connection to the GraphWalker WebSocket Server
Start GraphWalker from the command line using the standalone jar, using the **online** command.
~~~
java -jar graphwalker-3.2.0-SNAPSHOT.jar -d ALL online -p 8887
~~~
Starts the WebSocker server on localhost, listing on port 8887

A client may connect to ws://hostname:port. See [Java WebSocket Client example](https://github.com/GraphWalker/graphwalker-example/tree/3.2.0/java-websocket)

When connected, a GraphWalker machine will be created on the server, which will serve this client only.
When disconnected, the server will destroy the machine.

## loadModel
Loads a model into the GraphWalker machine.

The first model loaded, will be the one where the execution starts.
Several models can be loaded. Every model which is loaded, will have it's own context in the machine.
     
See also [The graph in JSON](docs/json_graph)

## start
Starts the machine. No more loadModel calls are allowed. 

## getNext
Gets the next element from the the GraphWalker machine

## hasNext
Checks if the machine has more steps to generate.

## restart
Will restart the machine. Any previously loaded models will be destroyed.

## getData
Asks the machine to return all data from the current model context.

## visitedElement
When the graph is executed by the server, it will send updates regarding the model state.
