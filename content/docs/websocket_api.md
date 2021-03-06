/*
Title: GraphWalker WebSopcket API
Description: This description will go in the meta description tag
*/

# GraphWalker WebSopcket API

The GraphWalker WebSocket Server enables a user to launch and interact with GraphWalker and inplement your tests in a very dynamic way. Any programming language that has an implementation of WebSocket will be able to use this feature.


## Establishing a connection to the GraphWalker WebSocket Server
Start GraphWalker from the command line using the standalone jar, using the **online** command.
~~~
java -jar graphwalker-3.2.1.jar -d ALL online -p 8887
~~~
Starts the WebSocker server, with full debug logging, on localhost, listing on port 8887<br>
Download it from [Latest dev standalone CLI - branch 3.2.1](/archive/graphwalker-cli-3.2.1.jar)

A client may connect to ws://localhost:8887. Try [Echo Test](http://www.websocket.org/echo.html).

 * Input `ws://localhost:8887` into **Location:**
 * Click the **Connect** button
 * Copy and paste the Example from http://graphwalker.org/docs/json_graph into **Message:**
 * Click the **Send** button
 * Copy and paste the `{"type": "start"}` and click the **Send** button
 * Copy and paste the `{"type": "hasNext"}` and click the **Send**  button
 * Copy and paste the `{"type": "getNext" }` and click the **Send**button

When connected, a GraphWalker machine will be created on the server, which will serve this client only.
When disconnected, the server will destroy the machine.

## loadModel : client -> server
Loads a model into the GraphWalker machine.

The first model loaded, will be the one where the execution starts.
Several models can be loaded. Every model which is loaded, will have it's own context in the machine.
 
### Request
For the request, see [The graph in JSON](json_graph)

### Response
~~~
{
    "type": "loadModel",
    "success": boolean,
    "msg": "If success is false, an message will returned"
}
~~~

## start : client -> server
Starts the machine. No more loadModel calls are allowed. 

### Request
~~~
{
    "type": "start"
}
~~~

### Response
~~~
{
    "type": "start",
    "success": boolean,
    "msg": "If success is false, a message will returned",
}
~~~

## getNext : client -> server
Gets the next element from the the GraphWalker machine

### Request
~~~
{
    "type": "getNext"
}
~~~

### Response
~~~
{
    "type": "getNext",
    "id": "Element id",
    "name": "Element name"
    "success": boolean,
    "msg": "If success is false, a message will returned",
}
~~~

## hasNext : client -> server
Checks if the machine has more steps to generate.

### Request
~~~
{
    "type": "hasNext"
}
~~~

### Response
~~~
{
    "type": "hasNext",
    "hasNext": boolean,
    "success": boolean,
    "msg": "If success is false, a message will returned"
}
~~~

## restart : client -> server
Will restart the machine. Any previously loaded models will be destroyed.

### Request
~~~
{
    "type": "restart"
}
~~~

### Response
~~~
{
    "type": "restart",
    "success": boolean,
    "msg": "If success is false, a message will returned"
}
~~~

## getData : client -> server
Asks the machine to return all data from the current model context.

### Request
~~~
{
    "type": "getData"
}
~~~

### Response
~~~
{
    "type": "getData",
    "success": boolean,
    "msg": "If success is false, a message will returned",
    "data": {
        :
        :
    }
}
~~~

## visitedElement : server -> client
When the graph is executed by the server, it will send updates regarding the model state.

### Message
~~~
{
    "type": "visitedElement",
    "id": "The id of the graph element.",
    "visitedCount": "<The number of times GraphWalker has visited (passed) this element>
}
~~~

## Spefification by Example and MBT test for the WebSocket Server

The graph below is an actual test where GraphWalker is testing itself. The graph also serves as a [Specifaction by Example](http://en.wikipedia.org/wiki/Specification_by_example). The specification dictates what API calls can be made given the current status. The test verifies that the implementation follows the design.

The test is run as one of the Unit tests in the CLI module. See [GraphWalkerWebSocketServerTest.java](https://github.com/GraphWalker/graphwalker-cli/blob/3.2.0/src/test/java/org/graphwalker/cli/GraphWalkerWebSocketServerTest.java)

<img src="/content/images/websocket_api.png" alt="WebSocket API">
