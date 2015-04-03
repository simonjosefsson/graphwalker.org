/*
Title: Documentation
Description: This description will go in the meta description tag
*/

## Documentation

### Startup guides
* [How to use GraphWalker](/docs/workflow)
* [Pet Clinic example](/docs/pet_clinic)
* [How to create a small test](/docs/howto_create_a_small_test)
* [Creating a boilerplate project using maven archetype](/docs/maven_archetype)

### Syntax
* [GraphWalker modelling syntax](/docs/gw_model_syntax)
* [Command line syntax](/docs/command_line_syntax)
* [Path generators and stop conditions](/docs/path_generators_and_stop_conditions)
* [Graph in JSON](/docs/json_graph) (from version 3.2.0)
* [GraphWalker WebSocket Messages API](/docs/websocket_api) (from version 3.2.0)

### How to's
* [How to submit a patch to GraphWalker](/docs/how_to_submit_a_patch_to_graphwalker)
* [How to run GraphWalker tests withC#](/docs/how_to_run_tests_with_c_sharp) (from version 3.2.0)

### Articles
* [Combining different stop conditions](/docs/combining_different_stop_conditions)
* [Best practices](/docs/bestpractices)

### Java Doc API
* [All Java Doc API documentation](/archive/apidocs/index.html)

### Maven Site Documentation
* [GraphWalker Project Site Documentation](/archive/site/index.html)

<br>
---------------------------------------

#### Missing anything?
If there's documentation you miss, if existing docs are wrong, or the english is bad or has typos, please let us know! Tell us by submitting an issue to [https://github.com/GraphWalker/graphwalker.org/issues](https://github.com/GraphWalker/graphwalker.org/issues)

Or even better, [create a pull request](https://help.github.com/articles/creating-a-pull-request)! Making a pull request means that reviewing the changes and discussing them gets so much more simpler.

* The doc is [here](https://github.com/GraphWalker/graphwalker.org/tree/master/content)
* The doc is stored in .md files. 
* The format of the doc is [markdown](http://en.wikipedia.org/wiki/Markdown)

##### How does this site work?
The source code for this site is in [GitHub](https://github.com/GraphWalker/graphwalker.org/). When a commit is pushed to the master branch, our build pipeline at [Travis CI](https://travis-ci.org/GraphWalker/graphwalker.org) gets triggered. The pipeline does not build anything, it just deploys any changes to [graphwalker.org](graphwalker.org) using rsync.The configuration for Travis is in [.travis.yml](https://github.com/GraphWalker/graphwalker.org/blob/master/.travis.yml).

The site is using [Pico CMS](http://picocms.org/).
