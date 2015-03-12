# Usage

To use this POM as parent POM add this configuration to your POM:

    <parent>
        <groupId>at.rseiler.pom-project</groupId>
        <artifactId>pom</artifactId>
        <version>1.1</version>
    </parent>

Then your own parent POM must define this property:

    <properties>
        <main.basedir>${project.basedir}</main.basedir>
    </properties>

The all sub modules must define this property:

    <properties>
        <main.basedir>${project.parent.basedir}</main.basedir>
    </properties>

That's needed to correctly reference the configuration files for the static code analysis.

## Features and Tips & Tricks

### Static Code Analysis

If not [disabled](maven-profiles.html) then the static code analysis are executed by default. If a major issue is found
then the build will fail.

#### Disabling for a specific module

To disable the static code analysis for a specific module just set the ```skipCodeAnalysis``` property to ```true```:

    <properties>
        <skipCodeAnalysis>true</skipCodeAnalysis>
    </properties>

This makes sense if there is no Java code in the module to check.

#### Config

The configuration for the static code analysis tools will automatically be unpacked to ```${project.basedir}/config/code-analysis```.

* checkstyle.xml
* checkstyle-suppressions.xml
* pmd-ruleset.xml

If you want to provide these files yourself then disable the unpacking like this:

    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-dependency-plugin</artifactId>
                <executions>
                    <execution>
                        <id>unpack</id>
                        <phase>none</phase>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>

#### FindBugs

If Dependency Injection is used with setters or with fields then FindBugs needs to be configured to ignore the
```UWF_FIELD_NOT_INITIALIZED_IN_CONSTRUCTOR: Field not initialized in constructor but dereferenced without null check```
check. Sadly it's not possible to use the annotations (@Autowired or @Inject) to suppress this check. It's needed to use
the name of the class or the name of the field.

__Example__

First create the ```file://${project.basedir}/config/code-analysis/findbugs-exclude.xml``` which should like this:

    <FindBugsFilter>
        <Match>
            <Or>
                <Class name="~.*Service"/>
                <Class name="~.*ServiceImpl"/>
                <Class name="~.*Controller"/>
                <Class name="~.*Interceptor"/>
                <Class name="~.*Validator"/>
                <Field name="~.*Service"/>
                <Field name="~.*Controller"/>
                <Field name="~.*Interceptor"/>
                <Field name="~.*Validator"/>
            </Or>
            <Bug pattern="UWF_FIELD_NOT_INITIALIZED_IN_CONSTRUCTOR"/>
        </Match>
    </FindBugsFilter>

Then configure the _findbugs-maven-plugin_:

    <build>
        <pluginManagement>
            <plugins>
                <plugin>
                    <groupId>org.codehaus.mojo</groupId>
                    <artifactId>findbugs-maven-plugin</artifactId>
                    <configuration>
                        <excludeFilterFile>${main.basedir}/config/code-analysis/findbugs-exclude.xml</excludeFilterFile>
                    </configuration>
                </plugin>
            </plugins>
        </pluginManagement>
    </build>

### Disable Unit Tests for a specific module

To disable the unit tests for a specific module just set the ```skipTests``` property to ```true```:

    <properties>
        <skipTests>true</skipTests>
    </properties>

### Build

Nothing is changed. Just use maven:

    mvn clean install

### Parallel Build

In a multi module maven project it's possible to build the modules in parallel - if the dependencies allow this.

Use the ```-T``` argument. Ether define a fix thread count with ```-T 4``` or define the thread count depended on the
cores of the computer with ```-T 2C```. 2C means for each core 2 threads will be used. E.g.: 4 cores => 8 threads.

    mvn install -T 4
    mvn install -T 2C

### Speed Up the Build

There is another option to speed up the build. With the ```-o``` (offline) argument maven won't check and download the
dependencies which gives you a speed boost. But be careful. If there is a dependency which isn't in your local
repository then the build will fail.

    mvn install -o
    mvn install -o -T 2C

### Documentation

To generate the documentation use maven site:

    mvn clean test site -P execITs,!staticCodeAnalysis

* disable the static code analysis because the static code analysis are executed from the report plugins
* execute the integration tests for the coverage report
