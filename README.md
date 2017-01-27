# POM-Project

The POM-Project is just a wrapper project to build the POM module and it's dependencies.


# POM

The POM is indented to be used as a parent POM, to speed up the setup/configuration of a new project.

## Features

* Static Code Analysis
    * [Error Prone](http://errorprone.info/)
    * [FindBugs](http://findbugs.sourceforge.net/)
    * [PMD](http://pmd.sourceforge.net/)
    * [CheckStyle](http://checkstyle.sourceforge.net/)
    * reasonable configuration included
    * fails the build if an major issue is found
* [JaCoCo](http://www.eclemma.org/jacoco/) for coverage reports
* [Surefire](https://maven.apache.org/surefire/) for unit tests with two configurations
    * tests which are thread safe and will be executed in parallel on the same JVM
    * tests which aren't thread safe and therefor will be run in JVM forks
* [Failsafe](https://maven.apache.org/surefire/maven-failsafe-plugin/) for integration tests
* [Maven Site](https://maven.apache.org/plugins/maven-site-plugin/)
    * [Markdown](https://en.wikipedia.org/wiki/Markdown) for the documentation
    * Project info reports
    * Generated Javadoc
    * Source Code as HTML for code references
    * Genereated tag lists for todo/fixme and @deprecated
    * JaCoCo, Surfire and Failsafe reports
* Maven Profiles (see [Maven Profiles](maven-profiles.html))


# Usage

This project isn't in the Maven Central Repository, yet.
Therefor you need to clone the GIT repository or download the repository and install it locally with ```mvn clean install```.
Afterwards you can deploy the artifacts to your Maven repository (e.g. Nexus).


# Documentation

Visit the documentation at: [Latest Documentation](https://rseiler.github.io/pom-project/pom/index.html)


# License

The pom-project is licensed under the terms of the
[Apache License, Version 2.0](https://www.apache.org/licenses/LICENSE-2.0.html)


# Thank you!

We really appreciate all kind of feedback and contributions. Thanks for using and supporting the POM-project.