+++
description = "This is my summary of the same spelling udacity course."
title = "Gradle for Android and Java"
date = "2017-03-05"
topics = ["Development"]
tags = ["udacity","android", "gradle", "java", "google"]

+++
You can find the corresponding udacity course [here] (https://www.udacity.com/course/gradle-for-android-and-java--ud867).

# Gradle Fundamentals

Why Gradle? Allow different app flavours like paid or free, debug and release. 

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

*The best debugger is clear thought and print statements.*

# Gradle for Java

Use gradle plugins available for gradle instead of reinventing the wheel.

Add the java plugin with ```apply plugin: "java"```. Find a quickstart guide [here](https://docs.gradle.org/current/userguide/tutorial_java_projects.html#gsc.tab=0).

Create a JAR with the command ```gradle assemble``` and execute it with ```gradle execute```.

Add repositories to your project by ```repository {...}```. Define dependencies on artifacts contained on your repositories. Ex.: ```dependencies { compile ... }```.

Generate a dependency report with ```gradle dependencies```.

**Identify version conflicts** with ```gradle dependencyInsight --dependency dependency-name``` what generates the dependency insight report.

Create fancy file collections with custom configurations:
```
configurations {
	custom
}

dependencies {
	custom 'com.google.guava:guava:18.0'
}
```

The scheme for archive names goes ```basename-appendix-version-classifier-extension```.

*High quality software depends on rigorous testing.* That's why tests need to be automated. There exist two sorts of tests:

- **Unit tests**: Test individual classes or methods in isolation.
- **Integration tests**: Test your code in conjunction with some other systems, libraries or environements.

Add test dependency by```testCompile 'junit:junit:4.12'```. 

Execute tests with ```gradle test``` and get detailed test reports from the ```build/reports``` directory.

Find Gradle Plugins on the [Gradle Plugin Portal](https://plugins.gradle.org/) or look at the [Standard Gradle plugins](https://docs.gradle.org/3.3/userguide/standard_plugins.html#gsc.tab=0).

Set the Gradle version to use in the ```gradle-wrapper.properties``` file and always version control it.

Generate the wrapper with ```gradle wrapper```.

# Gradle for Android

The entire Android build process is done by Gradle.

Build an APK is executing a Gradle script with the Android Gradle plugin provided by Google. 

Get a *"failed to sync"* message is usually an error in one of your build scripts.

Generated folders and files by Android Studio in a Gradle project:

| Folder        | What holds it?           |
| -------------- |-------------------------|
| .gradle | Information for incremental build support like tasks inputs and outputs. |
| .idea | Android Studio's model of your project |
| build | Outputs generated by your build |
| gradle | Wrapper JAR and wrapper properties |

| File        | What contains it?           |
| -------------- |-------------------------|
| build.gradle | Your Gradle script |
| .iml | Part of Android Studio's project model |
| gradlew / gradlew.bat | The wrapper scripts |
| local.properties | The Location of Android sdk on your machine |

Use build types (app/build.gradle) to build different versions of an app.

Find the DAC (developer.android.com) documentation on the Android Gradle plugin [here](https://developer.android.com/studio/build/index.html).

Create app flavors by adding the following underneath the buildTypes block:

```
productFlavors {
	free {
		applicationId "com.example.udacity.flavors.free"
	}
	paid {
		applicationId "com.example.udacity.flavors.paid"
	}
}
```

Create flavor specific content by right click on ```app>New>Android resources file``` enter a file name like "strings" and choose the source set like "paid" or "free".

# Advanced Android Builds 

## Application Libraries for Multiproject Builds

Two sorts of libraries:

- .jar : Java Library file, can be used on non-android projects
- .aar : Android Library file, can include manifest, fragments, layouts etc.

Create an Android Library by right click on the project>New>Module select "Android Library". Add your custom in project library with ```compile project(":mylibrary")``` in the dependencies block of your build.gradle. Like this we can create Activities that are easy to reuse between applications.

## Application Signing
Three things needed:

1. Create a key store and a key
1. Create a signing config
1. Assign the signing config to a build type

### Create a key store and a key

One time signing: Navigate to Build>Generate Signed APK and go through the wizzard.

Automatic signing: Right click on app>Open Module Settings switch to the Signing tab and create a new signing configuration. Go to the Build Types tab, select a build type and assign the Signing Config.

## Multi Deck Support

Turn Java byte code into Davik byte code = dexing. This creates 1 table limited to 65,000 entries.

If you have more then 65,000 methods in a project, set ```multiDexEnabled true``` in the defaultConfig in the build.gradle file. This will break up the dexing table into multiple tables.

## Proguard

Reduce size of your app by stripping out unused code and ressources. Add ```minifyEnabled true``` and ```shrinkResources true``` to your buildTypes in your build.gradle file.

You can also obfuscate your code with proguard.

## Android Testing

- **Unit tests**: Run on a regular Java VM on your computer. Use it to test generic, non-Android related classes. To test code that calls the Android API use a mocking framework like Mockito or connected tests.
- **Connected tests**: Run on an Android device or emulator.

| Test locations     | unit test        | connected           |
| -------------- | -------------- |-------------------------|
| general | /src/test | /src/androidTest |
| flavor "free" | /src/testFree | /src/androidTestFree |

# Special Topics

Add [Gradle Versions Plugin](https://github.com/ben-manes/gradle-versions-plugin) to your project hold your non-google plugins versions up to date.

More videos on Gradle can be found on [Gradle's youtube channel](https://www.youtube.com/channel/UCvClhveoEjokKIuBAsSjEwQ).

**Written with <span style="color:firebrick">&hearts;</span> for Gradle in Kiel.**
