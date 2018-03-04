# POM

This POM is indented to be used as a parent POM, to speed up the setup/configuration of a project.

## Features

* Static Code Analysis
    * [FindBugs](http://findbugs.sourceforge.net/)
    * [PMD](http://pmd.sourceforge.net/)
    * [CheckStyle](http://checkstyle.sourceforge.net/)
    * reasonable configuration included
    * fails the build if an major issue is found
* [JaCoCo](http://www.eclemma.org/jacoco/) for coverage reports
* [Surefire](https://maven.apache.org/surefire/) for unit tests with two configurations
    * tests which are thread safe and will be executed in parallel on the same JVM
    * tests which aren't thread safe and therefore will be run in JVM forks
* [Failsafe](https://maven.apache.org/surefire/maven-failsafe-plugin/) for integration tests
* [Maven Site](https://maven.apache.org/plugins/maven-site-plugin/)
    * [Markdown](https://en.wikipedia.org/wiki/Markdown) for the documentation
    * Project info reports
    * Generated Javadoc
    * Source Code as HTML for code references
    * Generated tag lists for todo/fixme and @deprecated
    * JaCoCo, Surfire and Failsafe reports
* Maven Profiles (see [Maven Profiles](maven-profiles.html))
