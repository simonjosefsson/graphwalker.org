/*
Title: Best practices
Description: This description will go in the meta description tag
*/

# Best practices

During the years some best practices has evolved. This is a collection of them.


## Prefixes of labels

### Readability

Adding prefixes on labels for edges and vertices is a practice that helps the implementation part. When looking at the code that implements a model, the labels, which in the code are represented by methods, they may not easily be distinguished as edges or vertices. When adding the prefix **v_** for vertices and **e_** for edges they will. This increases readability of the code.

### Aspect Oriented Programming using [AspectJ](https://eclipse.org/aspectj/)

Using AspectJ when programming in Java can be very helpful. An example could be logging results or taking screen shots. These actions could be performed in various ways:
 * Take a screen shot just before a call to a vertex.
 * Take a screen shot just after a call to a vertex.
 * Log every time an edge or a vertex is to be called.

Using prefixes as described above, will facilitate creating [pointcuts](http://blog.espenberntsen.net/2010/03/20/aspectj-cheat-sheet/).




