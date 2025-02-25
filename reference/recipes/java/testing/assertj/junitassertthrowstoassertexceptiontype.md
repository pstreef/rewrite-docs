# JUnit AssertThrows to AssertJ exceptionType

**org.openrewrite.java.testing.assertj.JUnitAssertThrowsToAssertExceptionType**

_Convert `JUnit#AssertThrows` to `AssertJ#assertThatExceptionOfType` to allow for chained assertions on the thrown exception._

## Source

[GitHub](https://github.com/openrewrite/rewrite-testing-frameworks/blob/main/src/main/java/org/openrewrite/java/testing/assertj/JUnitAssertThrowsToAssertExceptionType.java), [Issue Tracker](https://github.com/openrewrite/rewrite-testing-frameworks/issues), [Maven Central](https://central.sonatype.com/artifact/org.openrewrite.recipe/rewrite-testing-frameworks/2.0.2/jar)

* groupId: org.openrewrite.recipe
* artifactId: rewrite-testing-frameworks
* version: 2.0.2

## Example


{% tabs %}
{% tab title="SimpleExpectedExceptionTest.java" %}

###### Before
{% code title="SimpleExpectedExceptionTest.java" %}
```java
import static org.junit.jupiter.api.Assertions.assertThrows;

public class SimpleExpectedExceptionTest {
    public void throwsExceptionWithSpecificType() {
        assertThrows(NullPointerException.class, () -> {
            throw new NullPointerException();
        });
    }
}
```
{% endcode %}

###### After
{% code title="SimpleExpectedExceptionTest.java" %}
```java
import static org.assertj.core.api.AssertionsForClassTypes.assertThatExceptionOfType;

public class SimpleExpectedExceptionTest {
    public void throwsExceptionWithSpecificType() {
        assertThatExceptionOfType(NullPointerException.class).isThrownBy(() -> {
            throw new NullPointerException();
        });
    }
}
```
{% endcode %}

{% endtab %}
{% tab title="Diff" %}
{% code %}
```diff
--- SimpleExpectedExceptionTest.java
+++ SimpleExpectedExceptionTest.java
@@ -1,1 +1,1 @@
-import static org.junit.jupiter.api.Assertions.assertThrows;
+import static org.assertj.core.api.AssertionsForClassTypes.assertThatExceptionOfType;

@@ -5,1 +5,1 @@
public class SimpleExpectedExceptionTest {
    public void throwsExceptionWithSpecificType() {
-       assertThrows(NullPointerException.class, () -> {
+       assertThatExceptionOfType(NullPointerException.class).isThrownBy(() -> {
            throw new NullPointerException();
```
{% endcode %}
{% endtab %}
{% endtabs %}


## Usage

This recipe has no required configuration options. It can be activated by adding a dependency on `org.openrewrite.recipe:rewrite-testing-frameworks:2.0.2` in your build file or by running a shell command (in which case no build changes are needed): 
{% tabs %}
{% tab title="Gradle" %}
{% code title="build.gradle" %}
```groovy
plugins {
    id("org.openrewrite.rewrite") version("6.1.4")
}

rewrite {
    activeRecipe("org.openrewrite.java.testing.assertj.JUnitAssertThrowsToAssertExceptionType")
}

repositories {
    mavenCentral()
}

dependencies {
    rewrite("org.openrewrite.recipe:rewrite-testing-frameworks:2.0.2")
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
            <recipe>org.openrewrite.java.testing.assertj.JUnitAssertThrowsToAssertExceptionType</recipe>
          </activeRecipes>
        </configuration>
        <dependencies>
          <dependency>
            <groupId>org.openrewrite.recipe</groupId>
            <artifactId>rewrite-testing-frameworks</artifactId>
            <version>2.0.2</version>
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
  -Drewrite.recipeArtifactCoordinates=org.openrewrite.recipe:rewrite-testing-frameworks:RELEASE \
  -Drewrite.activeRecipes=org.openrewrite.java.testing.assertj.JUnitAssertThrowsToAssertExceptionType
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Contributors
* [Patrick Way](pway99@users.noreply.github.com)
* [Jeroen Meijer](jjgmeijer@gmail.com)
* [Jonathan Schnéider](jkschneider@gmail.com)
* [Knut Wannheden](knut@moderne.io)
* [Sam Snyder](sam@moderne.io)


## See how this recipe works across multiple open-source repositories

[![Moderne Link Image](/.gitbook/assets/ModerneRecipeButton.png)](https://app.moderne.io/recipes/org.openrewrite.java.testing.assertj.JUnitAssertThrowsToAssertExceptionType)

The community edition of the Moderne platform enables you to easily run recipes across thousands of open-source repositories.

Please [contact Moderne](https://moderne.io/product) for more information about safely running the recipes on your own codebase in a private SaaS.
