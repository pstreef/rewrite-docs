# Enhances logging of exceptions by including the full stack trace in addition to the exception message

**org.openrewrite.java.logging.slf4j.CompleteExceptionLogging**

_It is a common mistake to call `Exception.getMessage()` when passing an exception into a log method. Not all exception types have useful messages, and even if the message is useful this omits the stack trace. Including a complete stack trace of the error along with the exception message in the log allows developers to better understand the context of the exception and identify the source of the error more quickly and accurately. 
 If the method invocation includes any call to `Exception.getMessage()` or `Exception.getLocalizedMessage()` and not an exception is already passed as the last parameter to the log method, then we will append the exception as the last parameter in the log method._

### Tags

* slf4j
* logging

## Source

[GitHub](https://github.com/openrewrite/rewrite-logging-frameworks/blob/main/src/main/java/org/openrewrite/java/logging/slf4j/CompleteExceptionLogging.java), [Issue Tracker](https://github.com/openrewrite/rewrite-logging-frameworks/issues), [Maven Central](https://central.sonatype.com/artifact/org.openrewrite.recipe/rewrite-logging-frameworks/2.0.1/jar)

* groupId: org.openrewrite.recipe
* artifactId: rewrite-logging-frameworks
* version: 2.0.1

## Example


{% tabs %}
{% tab title="Test.java" %}

###### Before
{% code title="Test.java" %}
```java
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

class Test {
    Logger logger = LoggerFactory.getLogger(Test.class);
    void doSomething() {
        try {
            Integer num = Integer.valueOf("a");
        } catch (NumberFormatException e) {
            // TEST CASE #1:
            logger.error(e.getMessage());

            // TEST CASE #2:
            logger.error("BEFORE MESSAGE " + e.getMessage());

            // TEST CASE #3:
            logger.error("BEFORE MESSAGE " + e.getMessage() + " AFTER MESSAGE");

            // TEST CASE #4: No Changes, since stack trace already being logged
            logger.error("BEFORE MESSAGE " + e.getMessage() + " AFTER MESSAGE", e);
        }
    }
}
```
{% endcode %}

###### After
{% code title="Test.java" %}
```java

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

class Test {
    Logger logger = LoggerFactory.getLogger(Test.class);
    void doSomething() {
        try {
            Integer num = Integer.valueOf("a");
        } catch (NumberFormatException e) {
            // TEST CASE #1:
            logger.error("", e);

            // TEST CASE #2:
            logger.error("BEFORE MESSAGE " + e.getMessage(), e);

            // TEST CASE #3:
            logger.error("BEFORE MESSAGE " + e.getMessage() + " AFTER MESSAGE", e);

            // TEST CASE #4: No Changes, since stack trace already being logged
            logger.error("BEFORE MESSAGE " + e.getMessage() + " AFTER MESSAGE", e);
        }
    }
}
```
{% endcode %}

{% endtab %}
{% tab title="Diff" %}
{% code %}
```diff
--- Test.java
+++ Test.java
@@ -1,0 +1,1 @@
+
import org.slf4j.Logger;
@@ -11,1 +12,1 @@
        } catch (NumberFormatException e) {
            // TEST CASE #1:
-           logger.error(e.getMessage());
+           logger.error("", e);

@@ -14,1 +15,1 @@

            // TEST CASE #2:
-           logger.error("BEFORE MESSAGE " + e.getMessage());
+           logger.error("BEFORE MESSAGE " + e.getMessage(), e);

@@ -17,1 +18,1 @@

            // TEST CASE #3:
-           logger.error("BEFORE MESSAGE " + e.getMessage() + " AFTER MESSAGE");
+           logger.error("BEFORE MESSAGE " + e.getMessage() + " AFTER MESSAGE", e);

```
{% endcode %}
{% endtab %}
{% endtabs %}


## Usage

This recipe has no required configuration options. It can be activated by adding a dependency on `org.openrewrite.recipe:rewrite-logging-frameworks:2.0.1` in your build file or by running a shell command (in which case no build changes are needed): 
{% tabs %}
{% tab title="Gradle" %}
{% code title="build.gradle" %}
```groovy
plugins {
    id("org.openrewrite.rewrite") version("6.1.4")
}

rewrite {
    activeRecipe("org.openrewrite.java.logging.slf4j.CompleteExceptionLogging")
}

repositories {
    mavenCentral()
}

dependencies {
    rewrite("org.openrewrite.recipe:rewrite-logging-frameworks:2.0.1")
}
```
{% endcode %}
{% endtab %}
{% tab title="Maven POM" %}
{% code title="pom.xml" %}
```markup
<project>
  <build>
    <plugins>
      <plugin>
        <groupId>org.openrewrite.maven</groupId>
        <artifactId>rewrite-maven-plugin</artifactId>
        <version>5.2.4</version>
        <configuration>
          <activeRecipes>
            <recipe>org.openrewrite.java.logging.slf4j.CompleteExceptionLogging</recipe>
          </activeRecipes>
        </configuration>
        <dependencies>
          <dependency>
            <groupId>org.openrewrite.recipe</groupId>
            <artifactId>rewrite-logging-frameworks</artifactId>
            <version>2.0.1</version>
          </dependency>
        </dependencies>
      </plugin>
    </plugins>
  </build>
</project>
```
{% endcode %}
{% endtab %}

{% tab title="Maven Command Line" %}
{% code title="shell" %}
You will need to have [Maven](https://maven.apache.org/download.cgi) installed on your machine before you can run the following command.

```shell
mvn -U org.openrewrite.maven:rewrite-maven-plugin:run \
  -Drewrite.recipeArtifactCoordinates=org.openrewrite.recipe:rewrite-logging-frameworks:RELEASE \
  -Drewrite.activeRecipes=org.openrewrite.java.logging.slf4j.CompleteExceptionLogging
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Contributors
* [Kun Li](kun@moderne.io)
* [Knut Wannheden](knut@moderne.io)


## See how this recipe works across multiple open-source repositories

[![Moderne Link Image](/.gitbook/assets/ModerneRecipeButton.png)](https://app.moderne.io/recipes/org.openrewrite.java.logging.slf4j.CompleteExceptionLogging)

The community edition of the Moderne platform enables you to easily run recipes across thousands of open-source repositories.

Please [contact Moderne](https://moderne.io/product) for more information about safely running the recipes on your own codebase in a private SaaS.
