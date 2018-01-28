# Gradle 4 Exercises

This is a set of simple exercises for the Entelect 2018 Bootcamp, designed to
give you a light introduction to Gradle. Since the bulk of the time you spend
in Bootcamp will be spent using Maven, this is just intended to broaden your
experience a bit (it might come in handy if you end up working on an Android
project).

As prerequisite to starting these exercises you will need to ensure that you
have:

 * JDK 8 installed and available on the PATH.
 * Gradle installed and available on the PATH (https://gradle.org/install/). 

To start the exercise check out branch `exercise1` and check back here for
instructions.

## Exercise 1

You have been provided with some code that calculates some basic information
about superheroes belonging to different comic book publishers, but
unfortunately the code repository does not seem to include any way to build
and run the code... let's use Gradle to get it building and running.

The `gradle init` task can be used to add Gradle to a project, but we don't
know the details of calling, so let's get some help first:

```
gradle help --task init
```

So let's use `--type java-application` with init to see what happens:

```
gradle init --type java-application
```

You'll see Gradle has created a number of files for us:
 * `build.gradle`: Our build script (we'll need to tweak this).
 * `settings.gradle`: Our build configuration.
 * Several files for the Graddle wrapper:
   * `gradlew`
   * `gradlew.bat`
   * `gradle/`

Now open up `build.gradle` and make the following changes to it:
 * Change `mainClassName`'s value to `za.co.entelect.bootcamp.Application`.
 * Fix the dependencies to be correct for a Spring Boot project.
 * Add the Spring Boot Gradle plugin.
 
The dependencies needed by this project are:

```
dependencies {
    compile 'org.springframework.boot:spring-boot-starter'
    testCompile 'org.springframework.boot:spring-boot-starter-test'
}
```


Finally add the Spring Boot Gradle plugin to your `plugins` section:

```
plugins {
    ...
    id 'org.springframework.boot' version '1.5.9.RELEASE'
}
```

Now try to build the application with `gradle build` (or `./gradlew build`).
You'll get some compile errors that essentially amount to the application
not being configured to use Java 8. Fix it by adding the following somewhere
in your `build.gradle`, then try again:

```
sourceCompatibility = 1.8
```

Your build should succeed now, so then you can try running the application
with: `java -jar build/libs/gradle4-exercises.jar`.

Since this is a Spring Boot application and you have the Boot plugin in your
build configuration you can also run it with:
`./gradlew bootRun`.

You can always see available tasks in a Gradle project with `./gradlew tasks`.
The list of available tasks will change as you add and remove plugins, but many
of the tasks are built into Gradle's core.

Solution branch: `solution1`.

Next exercise branch: `exercise2`. 