= Calculib =
Calculib is a hobby project that I'm using to 1) brush up on my math and calculus skills and 2) explore the Scala programming language.

The goal is to take an input expression string and perform operations like differentiation and integration on the expression.
The library should also simplify the differentiated / integrated expression. 
Scala was chosen for its powerful pattern matching features and strong FP (and OOP) support. 
Pattern matching allows us to breeze through expression tree manipulations so easily that we don't even need to have a tree to represent the expression. 

== Dependency Management ==
To introduce external libraries and manage our dependencies I use (sbt)[https://www.scala-sbt.org/index.html]
* sbt uses a build.sbt file to specify project dependencies
* sbt ships with a cli command `sbt` that gives you an interactive shell to compile and run your application 
* using sbt requires your project to follow a pretty specific directory structure:
 
* build.sbt
* src/
    * main/   
        * scala/
            * *.scala resources
    * test/
        * scala/
            * *.scala test resources


== Unit Testing ==
So far everything has been self contained and we didn't need any external libraries. But scala doesn't have a builtin unit testing suite, so we need to introduce one.
Scalatest seems to be the recommended approach.
