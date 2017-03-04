+++
description = "This is my summary of the same spelling udacity course."
title = "Gradle for Android and Java"
date = "2017-03-05"
topics = ["Development"]
tags = ["udacity","android", "gradle", "java", "google"]

+++
You can find the corresponding udacity course [here] (https://www.udacity.com/course/gradle-for-android-and-java--ud867).

# Gradle Fundamentals

Why Gradle? Allow different app flavours like paid or free. 

## Groovy

Groovy is *the* scripting language for java developers.

Groovy functions always return the last expression in the function block.

### Closure

Closures are like code blocks and are surrounded by ```{``` and ```}```. Example:

```groovy
def myClosure {
	...
	...
}
```
Call it by ```myClosure()```.

Make a one line closure ```def myClosure = { ... }```

Higher order = functions as arguments are possible. Example:
```groovy
def applyTwice(func, arg) {
	func(func(arg))
}
```

If a closure is only taking 1 argument by default that argument is called ```it```. Access it by ```$it```. Example:
```groovy
def myList = ["Gradle", "Groovy", "Android"]
def printItem = {item -> println "list elem: $item"}
myList.each(printItem)
myList.each{println "list item: $it"}
```

### Classes

```groovy
class GroovyGreeter {
	...
	...
}
```
Setters and getters are automatically created, accress them by ```.```

For more Groovy knowledge [Learn X in Y: Groovy](https://learnxinyminutes.com/docs/groovy/) and [Official Groovy user guide](http://www.groovy-lang.org/documentation.html).

## Tasks

A task does an action.

Run tasks with the *Gradle wrapper* 

- ```./gradlew tasks``` Show all tasks runnable from a root project
- ```./gradlew hello``` Run the "hello" task

Daemon = process that hangs around in the background of your operating system. **Always use a daemon if possible.**

- ```gradle taskname``` Run the task "taskname"
- ```gradle -q``` Run in quiet mode to show only the output
- ```gradle -b solution.gradle tasks``` See all tasks of *solution.gradle*

### Typed tasks
Example:
```
task copyFiles(type: Copy)
```
Common types are:

- ```type: Copy``` copy files, unpack archives
- ```type: Zip``` create archives
- ```type: Delete``` delete files and folders

See all task types in the [Gradle DSL Reference](https://docs.gradle.org/current/dsl/). The **Gradle DSL Reference is your best friend: learn it, love it!**

incremental builds = doing the minimum amount necessary

#### Create custom types for tasks

```
class HelloTask extends DefaultTask {
	String firstName

	@TaskAction
	void doAction() {
		... //Use for ex. firstName
  	}
}

task hello(type: HelloTask) {firstName = 'Gunda'}
```

### Relationships between tasks

- ```dependsOn``` A depends on B if task A can't do it's work without task B
- ```finalizedBy``` A is finalized by B if every time task A runs, task B should be run afterwards
- ```mustRunAfter``` B must run after A, whenever both task A and task B will be run

## Build scripts

Gradle build scripts are written in the domain specific language (DSL) that sits on top of Groovy. 

The Gradle plattform is written in Java.

Plugins can be written in any JVM language like Java, Groovy or Scala.

**Keep build scripts declarativ. Low-level logic is for Gradle plugins!**

A build script has a delegate object. = Entire project delegates to a project object.

Declare tasks with method ```task(Tasknames)``` on the project object. Then Gradle tasks show under other tasks the Tasknames.

These are all identic:
```groovy
project.task("myTask")
task("myTask")
task "myTask"
task myTask
```
### Functions on tasks

- ```description``` Give a decription for the task
- ```group``` Name the task group
- ```doLast``` Add a task to the end of the task list
- ```doFirst``` Add a task to the front of the task list

task configuration closure example:
```groovy
task myTask {
	description "The description of my Task" //this is a function
	group "The group of my Task" //call omitting the parentheses
	doLast {
		...
	}
}
```

## Log levels
- ```-d``` Debug
- ```-i``` Info
- ```default``` Warning & Lifecycle
- ```-q``` Error & Quiet

println statements are in the quite logging level.

- ```gradle -s``` Put out the stacktrace
- ```gradle -S``` Put out the full stacktrace

## Build Lifecyle

Has 3 steps:

1. ```Initialization``` Set up multi-project builds
1. ```Configuration``` Execute the build script and configure all the projects tasks
1. ```Execution``` Execute the projects tasks

*The best debugger is clear thought and print statements*

# Gradle for Java

# Gradle for Android

# Advanced Android Builds 

