# JUnit 4 `@RunWith` to JUnit Jupiter `@ExtendWith`

**org.openrewrite.java.testing.junit5.RunnerToExtension**

_Replace runners with the JUnit Jupiter extension equivalent._

## Source

[GitHub](https://github.com/openrewrite/rewrite-testing-frameworks/blob/main/src/main/java/org/openrewrite/java/testing/junit5/RunnerToExtension.java), [Issue Tracker](https://github.com/openrewrite/rewrite-testing-frameworks/issues), [Maven Central](https://central.sonatype.com/artifact/org.openrewrite.recipe/rewrite-testing-frameworks/2.0.2/jar)

* groupId: org.openrewrite.recipe
* artifactId: rewrite-testing-frameworks
* version: 2.0.2

## Options

| Type | Name | Description |
| -- | -- | -- |
| `List` | runners | The fully qualified class names of the JUnit 4 runners to replace. Sometimes several runners are replaced by a single JUnit Jupiter extension. |
| `String` | extension | The fully qualified class names of the JUnit Jupiter extension. |

## Example

###### Parameters
| Parameter | Value |
| -- | -- |
|runners|`List.of("org.mockito.runners.MockitoJUnitRunner")`|
|extension|`org.mockito.junit.jupiter.MockitoExtension`|


{% tabs %}
{% tab title="MyTest.java" %}

###### Before
{% code title="MyTest.java" %}
```java
import org.junit.runner.RunWith;
import org.mockito.runners.MockitoJUnitRunner;

@RunWith(MockitoJUnitRunner.class)
public class MyTest {
}
```
{% endcode %}

###### After
{% code title="MyTest.java" %}
```java
import org.junit.jupiter.api.extension.ExtendWith;
import org.mockito.junit.jupiter.MockitoExtension;

@ExtendWith(MockitoExtension.class)
public class MyTest {
}
```
{% endcode %}

{% endtab %}
{% tab title="Diff" %}
{% code %}
```diff
--- MyTest.java
+++ MyTest.java
@@ -1,2 +1,2 @@
-import org.junit.runner.RunWith;
-import org.mockito.runners.MockitoJUnitRunner;
+import org.junit.jupiter.api.extension.ExtendWith;
+import org.mockito.junit.jupiter.MockitoExtension;

@@ -4,1 +4,1 @@
import org.mockito.runners.MockitoJUnitRunner;

-@RunWith(MockitoJUnitRunner.class)
+@ExtendWith(MockitoExtension.class)
public class MyTest {
```
{% endcode %}
{% endtab %}
{% endtabs %}


## Usage

This recipe has required configuration parameters. Recipes with required configuration parameters cannot be activated directly. To activate this recipe you must create a new recipe which fills in the required parameters. In your `rewrite.yml` create a new recipe with a unique name. For example: `com.yourorg.RunnerToExtensionExample`.
Here's how you can define and customize such a recipe within your rewrite.yml:

{% code title="rewrite.yml" %}
```yaml
---
type: specs.openrewrite.org/v1beta/recipe
name: com.yourorg.RunnerToExtensionExample
displayName: JUnit 4 `@RunWith` to JUnit Jupiter `@ExtendWith` example
recipeList:
  - org.openrewrite.java.testing.junit5.RunnerToExtension:
      runners: org.springframework.test.context.junit4.SpringRunner
      extension: org.springframework.test.context.junit.jupiter.SpringExtension
```
{% endcode %}

Now that `com.yourorg.RunnerToExtensionExample` has been defined activate it and take a dependency on org.openrewrite.recipe:rewrite-testing-frameworks:2.0.2 in your build file:
{% tabs %}
{% tab title="Gradle" %}
{% code title="build.gradle" %}
```groovy
plugins {
    id("org.openrewrite.rewrite") version("6.1.4")
}

rewrite {
    activeRecipe("com.yourorg.RunnerToExtensionExample")
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
{% tab title="Maven" %}
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
            <recipe>com.yourorg.RunnerToExtensionExample</recipe>
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
{% endtabs %}

## Contributors
* [Jonathan Schneider](jkschneider@gmail.com)
* [Greg Adams](greg@moderne.io)
* [Sam Snyder](sam@moderne.io)
* [Knut Wannheden](knut@moderne.io)
* [Scott Jungling](scott.jungling@gmail.com)
* [Aaron Gershman](aegershman@gmail.com)
* [Tyler Van Gorder](tkvangorder@users.noreply.github.com)
* [Patrick Way](pway99@users.noreply.github.com)
* [Tim te Beek](tim.te.beek@jdriven.com)
* [Michael Keppler](bananeweizen@gmx.de)
* [Patrick](patway99@gmail.com)


## See how this recipe works across multiple open-source repositories

[![Moderne Link Image](/.gitbook/assets/ModerneRecipeButton.png)](https://app.moderne.io/recipes/org.openrewrite.java.testing.junit5.RunnerToExtension)

The community edition of the Moderne platform enables you to easily run recipes across thousands of open-source repositories.

Please [contact Moderne](https://moderne.io/product) for more information about safely running the recipes on your own codebase in a private SaaS.
