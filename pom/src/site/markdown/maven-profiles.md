# Maven Profiles

There are following maven profiles:

* __staticCodeAnalysis__:   runs the static code analysis tools and fails the build if a major issue is found (it's active per default)
* __execITs__:              executes the integration tests
* __skipTests__:            skips the unit tests and integration tests


## Examples

__Enable Integration Tests__

    mvn goal -P execITs

__Disable Static Code Analysis__

    mvn goal -P !staticCodeAnalysis

__Disable Tests__

    mvn goal -P skipTests

## Information

[Introduction to Maven profiles](https://maven.apache.org/guides/introduction/introduction-to-profiles.html)

To enable profiles use

    mvn goal -P profile-1,profile-2

To disable profiles use

    mvn goal -P !profile-1,!profile-2
