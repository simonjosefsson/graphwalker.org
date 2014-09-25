/*
Title: How to create a small test
Description: This description will go in the meta description tag
*/

# How to create a small test

This will show how to create a small GraphWalker test.


## Download and install the dependencies

 * Install the Java JDK, 7 or 8 will do
 * Install the [Maven](http://maven.apache.org/download.cgi)

## Create folder structure
From the command line, run:
~~~
%> mkdir -p gw_test/src/test/java/
%> cd gw_test
~~~

Copy and paste following into ***src/test/java/ExampleTest.java***
~~~
import org.graphwalker.core.condition.VertexCoverage;
import org.graphwalker.core.generator.RandomPath;
import org.graphwalker.core.machine.*;
import org.graphwalker.core.model.*;
import org.junit.Assert;
import org.junit.Test;

import static org.hamcrest.core.Is.is;

public class ExampleTest extends ExecutionContext {

    public void vertex1() {
        System.out.println("vertex1");
    }

    public void edge1() {
        System.out.println("edge1");
    }

    public void vertex2() {
        System.out.println("vertex2");
    }

    public void vertex3() {
        throw new RuntimeException();
    }

    public boolean isFalse() {
        return false;
    }

    public boolean isTrue() {
        return true;
    }

    public void myAction() {
        System.out.println("Action called");
    }

    @Test
    public void success() {
        Vertex start = new Vertex();
        Model model = new Model().addEdge(new Edge()
                .setName("edge1")
                .setGuard(new Guard("isTrue()"))
                .setSourceVertex(start
                        .setName("vertex1"))
                .setTargetVertex(new Vertex()
                        .setName("vertex2"))
                .addAction(new Action("myAction();")));
        this.setModel(model.build());
        this.setPathGenerator(new RandomPath(new VertexCoverage(100)));
        setNextElement(start);
        Machine machine = new SimpleMachine(this);
        while (machine.hasNextStep()) {
            machine.getNextStep();
        }
    }

    @Test(expected = MachineException.class)
    public void failure() {
        Vertex start = new Vertex();
        Model model = new Model().addEdge(new Edge()
                .setName("edge1")
                .setGuard(new Guard("isFalse()"))
                .setSourceVertex(start
                        .setName("vertex1"))
                .setTargetVertex(new Vertex()
                        .setName("vertex2")));
        this.setModel(model.build());
        this.setPathGenerator(new RandomPath(new VertexCoverage(100)));
        setNextElement(start);
        Machine machine = new SimpleMachine(this);
        while (machine.hasNextStep()) {
            machine.getNextStep();
        }
    }

    @Test
    public void exception() {
        Vertex start = new Vertex();
        Model model = new Model().addEdge(new Edge()
                .setName("edge1")
                .setGuard(new Guard("isTrue()"))
                .setSourceVertex(start
                        .setName("vertex3"))
                .setTargetVertex(new Vertex()
                        .setName("vertex2")));
        this.setModel(model.build());
        this.setPathGenerator(new RandomPath(new VertexCoverage(100)));
        setNextElement(start);
        Machine machine = new SimpleMachine(this);
        Assert.assertThat(getExecutionStatus(), is(ExecutionStatus.NOT_EXECUTED));
        try {
            while (machine.hasNextStep()) {
                machine.getNextStep();
                Assert.assertThat(getExecutionStatus(), is(ExecutionStatus.EXECUTING));
            }
        } catch (Throwable t) {
            Assert.assertTrue(MachineException.class.isAssignableFrom(t.getClass()));
            Assert.assertThat(getExecutionStatus(), is(ExecutionStatus.FAILED));
        }
    }
}
~~~

Also, copy and paste following into ***pom.xml***
~~~
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">

    <modelVersion>4.0.0</modelVersion>

    <groupId>org.myorg</groupId>
    <version>1.0.0-SNAPSHOT</version>
    <artifactId>example</artifactId>
    <name>GraphWalker Core</name>

    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.1</version>
                <configuration>
                    <source>1.7</source>
                    <target>1.7</target>
                </configuration>
            </plugin>
        </plugins>
    </build>


    <dependencies>
        <dependency>
            <groupId>org.graphwalker</groupId>
            <artifactId>graphwalker-core</artifactId>
	    <version>3.0.0</version>
        </dependency>
        <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-api</artifactId>
	    <version>1.7.7</version>
        </dependency>
        <dependency>
            <groupId>ch.qos.logback</groupId>
            <artifactId>logback-classic</artifactId>
	    <version>1.1.2</version>
        </dependency>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
	    <version>4.11</version>
            <scope>test</scope>
        </dependency>
    </dependencies>

</project>
~~~

Your folder and file structure will look like this:
~~~
%> tree
.
├── pom.xml
└── src
    └── test
        └── java
            └── ExampleTest.java
~~~

## Running the test
Run the following:
~~~
%> mvn test
[INFO] Scanning for projects...
[INFO]                                                                         
[INFO] ------------------------------------------------------------------------
[INFO] Building GraphWalker Core 1.0.0-SNAPSHOT
[INFO] ------------------------------------------------------------------------
[INFO] 
[INFO] --- maven-resources-plugin:2.3:resources (default-resources) @ example ---
[WARNING] Using platform encoding (UTF-8 actually) to copy filtered resources, i.e. build is platform dependent!
[INFO] skip non existing resourceDirectory /home/krikar/Documents/src/main/resources
[INFO] 
[INFO] --- maven-compiler-plugin:3.1:compile (default-compile) @ example ---
[INFO] No sources to compile
[INFO] 
[INFO] --- maven-resources-plugin:2.3:testResources (default-testResources) @ example ---
[WARNING] Using platform encoding (UTF-8 actually) to copy filtered resources, i.e. build is platform dependent!
[INFO] skip non existing resourceDirectory /home/krikar/Documents/src/test/resources
[INFO] 
[INFO] --- maven-compiler-plugin:3.1:testCompile (default-testCompile) @ example ---
[INFO] Changes detected - recompiling the module!
[WARNING] File encoding has not been set, using platform encoding UTF-8, i.e. build is platform dependent!
[INFO] Compiling 1 source file to /home/krikar/Documents/target/test-classes
[INFO] 
[INFO] --- maven-surefire-plugin:2.10:test (default-test) @ example ---
[INFO] Surefire report directory: /home/krikar/Documents/target/surefire-reports

-------------------------------------------------------
 T E S T S
-------------------------------------------------------
Running ExampleTest
vertex1
Action called
edge1
vertex2
vertex1
Tests run: 3, Failures: 0, Errors: 0, Skipped: 0, Time elapsed: 0.638 sec

Results :

Tests run: 3, Failures: 0, Errors: 0, Skipped: 0

[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 4.610s
[INFO] Finished at: Thu Sep 25 21:09:25 CEST 2014
[INFO] Final Memory: 10M/27M
[INFO] ------------------------------------------------------------------------
~~~


