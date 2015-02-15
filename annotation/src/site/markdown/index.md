# POM - Annotation

Contains the ```@ThreadUnsafe``` annotation which is used to mark unit tests which can't run in parallel on one JVM.

All marked tests will be still be running in parallel but in forked JVMs. So that there can't be any multi threading issues.

## Usage

Annotate the test class which isn't thread safe with ```@Category(ThreadUnsafe.class)```.

    import at.rseiler.annotation.junit.ThreadUnsafe;
    import org.junit.experimental.categories.Category;

    @Category(ThreadUnsafe.class)
    public class ThreadUnsafeTest {
    }

To use the annotation this dependency is needed:

    <dependency>
        <groupId>at.rseiler.pom-project</groupId>
        <artifactId>annotation</artifactId>
        <version>1.0</version>
    </dependency>
