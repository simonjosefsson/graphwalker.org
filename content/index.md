/*
Title: Home
Description: This description will go in the meta description tag
*/

## What is GraphWalker?

It's a Model-Based testing tool built in Java. It reads models in the shape of finite-state diagrams, or directed graphs, and generate tests from the models, either offline or online.

<img src="/pico/content/images/Login-small.png" alt="Model" align="left">

#### *For the tester:*
It's easy to design for test automation, even if you don't have any or little programming skills. The modeling syntax is very simple, and people can get started in less than an hour. The most common use cases for GraphWalker are automated end user acceptance tests, or any tests with workflows in them. Designing a decent set of regression tests using GraphWalker is a breeze.

#### *For the test automation developer:*
GraphWalker is very easy to setup and start using in your test automation code. It's is highly modularized, and it's easy to extend if you need to customize it.

#### *For the team:*
Modelling using a finite-state diagram is visual, it's easy to understand. Getting feed-back from team members and stakeholders is so much more easier with models.

#### *For whoever pays the bills:*
The models creates an abstraction layer between the test design and the implementing automation code. This is important when it comes to maintenance. Remember that the test automation (code and design) will have as long life time expectancy as the system under test. The return of investment is higher, if the test design and automation code is easy to work with and maintain. That's why it's so important with a good abstraction layer between design and implementation.

## Some docs that you might wanna read
* [A quick startup guide](/pico/docs/quick_startup_guide)
* [GraphWalker modelling syntax](/pico/docs/gw_model_syntax)
* Running the examples
* [Workflow using GraphWalker](/pico/docs/workflow)

## How to get it?
Either download the standalone jar file, or include it directly in you java project.

* Download the stand-alone graphwalker.jar

* In your maven project. Add this to your pom.file

<pre>
<span style='color:#a65700; '>&lt;</span><span style='color:#5f5035; '>dependency</span><span style='color:#a65700; '>></span>
   <span style='color:#a65700; '>&lt;</span><span style='color:#5f5035; '>groupId</span><span style='color:#a65700; '>></span>org.graphwalker<span style='color:#a65700; '>&lt;/</span><span style='color:#5f5035; '>groupId</span><span style='color:#a65700; '>></span>
   <span style='color:#a65700; '>&lt;</span><span style='color:#5f5035; '>artifactId</span><span style='color:#a65700; '>></span>graphwalker-core<span style='color:#a65700; '>&lt;/</span><span style='color:#5f5035; '>artifactId</span><span style='color:#a65700; '>></span>
   <span style='color:#a65700; '>&lt;</span><span style='color:#5f5035; '>version</span><span style='color:#a65700; '>></span>3.0.0-RC1<span style='color:#a65700; '>&lt;/</span><span style='color:#5f5035; '>version</span><span style='color:#a65700; '>></span>
<span style='color:#a65700; '>&lt;/</span><span style='color:#5f5035; '>dependency</span><span style='color:#a65700; '>></span>
</pre>

## License

GraphWalker is a <a href="http://opensource.org/licenses/MIT">MIT lincensed</a> <a href="http://opensource.org">Open Soure project</a>.

