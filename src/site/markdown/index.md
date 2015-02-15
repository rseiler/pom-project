# POM Project

This is just the wrapper project to build the [POM](pom/index.html) and it's dependencies.

__The build POM is indented to be used as a parent POM, to speed up the setup/configuration of a new project.__

Please go to the [__POM module__](pom/index.html) for more details.


## Build

To build the project use maven:

    mvn clean install


## Documentation

To generate this documentation use maven site:

    mvn clean test site -P !staticCodeAnalysis

Disable the static code analysis because it's executed from the report plugins.
