/*
Title: A quick startup guide
Description: This description will go in the meta description tag
*/

# A quick startup guide

This will show how to create a small test. We will not implement the test, I leave that as an exercise to the reader.


## Download and install the dependencies

 * Install the Java, 7 or 8 will do
 * Install the [yEd editor](http://www.yworks.com/en/products_yed_about.html)
 * Download the latest GraphWalker standalone jar file.

## The model
Let's start with creating a simple model that will depict the expected behaviour of our system under test. For this exercise, we are gonna use the Amazon website, and we will test the search feature. The test will be very simple. We are only going to test som very few things.

This is how a model might look like:

 * Search for a specific book - Should just return 1 book
 * Do a broad search - Should return a list a books
 * Use a search expression that will yield no hits.

<a href="/pico/content/images/AmazonSearch.graphml"><img src="/pico/content/images/AmazonSearch.png" alt="Amazon search"></a>

Right-click on the model above, and save it (Save link as...) as *AmazonSearch.graphml*. To have look at the model, open it using yEd.
Put the model in the same folder as the GraphWalker jar.

## Generating tests

There are a lot of different tests or test cases hidden in this model. Let's use GraphWalker to extract some of them. The first test will be asking GraphWalker to traverse the model in a random fashion, and stop when we have visited erey vertex.
From the command line, run the following:

~~~
%> java -jar graphwalker.jar offline -m AmazonSearch.graphml "random(vertex_coverage(100))"
~~~
You would get something like this:
~~~
e_StartBrowser
v_AmazonHomePage
e_SearchForSpecificBook
v_OneBookOnly
e_Home
v_AmazonHomePage
e_BroadSearch
v_ManyBooks
e_Home
v_AmazonHomePage
e_ImpossibleSearch
v_NoBooks
~~~
It will most likely have a different order, but that is expected.