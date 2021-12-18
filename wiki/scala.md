# Scala 

## Dependency Management 
To introduce external libraries and manage our dependencies I use (sbt)[https://www.scala-sbt.org/index.html]
* sbt uses a build.sbt file to specify project dependencies
* sbt ships with a cli command `sbt` that gives you an interactive shell to compile and run your application 
* using sbt requires your project to follow a pretty specific directory structure 
    * (you can create this automatically with `sbt new scala/scala3.g8`)
 
* build.sbt
* src/
    * main/   
        * scala/
            * *.scala resources
    * test/
        * scala/
            * *.scala test resources


## Unit Testing 
So far everything has been self contained and we didn't need any external libraries. But scala doesn't have a builtin unit testing suite, so we need to introduce one.
Scalatest seems to be the recommended approach.
