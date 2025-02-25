# Result of method call ignored

**org.openrewrite.java.search.ResultOfMethodCallIgnored**

_Find locations where the result of the method call is being ignored._

## Source

[GitHub](https://github.com/openrewrite/rewrite/blob/main/rewrite-java/src/main/java/org/openrewrite/java/search/ResultOfMethodCallIgnored.java), [Issue Tracker](https://github.com/openrewrite/rewrite/issues), [Maven Central](https://central.sonatype.com/artifact/org.openrewrite/rewrite-java/8.1.3/jar)

* groupId: org.openrewrite
* artifactId: rewrite-java
* version: 8.1.3

## Options

| Type | Name | Description |
| -- | -- | -- |
| `String` | methodPattern | A [method pattern](/reference/method-patterns.md) that is used to find matching method invocations. |

## Example

###### Parameters
| Parameter | Value |
| -- | -- |
|methodPattern|`java.io.File mkdir*()`|


{% tabs %}
{% tab title="Test.java" %}

###### Before
{% code title="Test.java" %}
```java
import java.io.File;
class Test {
    void test() {
        new File("dir").mkdirs();
        new File("dir").mkdir();
        boolean b1 = new File("dir").mkdirs();
        if(!new File("dir").mkdirs()) {
            throw new IllegalStateException("oops");
        }
    }
}
```
{% endcode %}

###### After
{% code title="Test.java" %}
```java
import java.io.File;
class Test {
    void test() {
        /*~~>*/new File("dir").mkdirs();
        /*~~>*/new File("dir").mkdir();
        boolean b1 = new File("dir").mkdirs();
        if(!new File("dir").mkdirs()) {
            throw new IllegalStateException("oops");
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
@@ -4,2 +4,2 @@
class Test {
    void test() {
-       new File("dir").mkdirs();
-       new File("dir").mkdir();
+       /*~~>*/new File("dir").mkdirs();
+       /*~~>*/new File("dir").mkdir();
        boolean b1 = new File("dir").mkdirs();
```
{% endcode %}
{% endtab %}
{% endtabs %}


## Usage

This recipe has required configuration parameters. Recipes with required configuration parameters cannot be activated directly. To activate this recipe you must create a new recipe which fills in the required parameters. In your `rewrite.yml` create a new recipe with a unique name. For example: `com.yourorg.ResultOfMethodCallIgnoredExample`.
Here's how you can define and customize such a recipe within your rewrite.yml:

{% code title="rewrite.yml" %}
```yaml
---
type: specs.openrewrite.org/v1beta/recipe
name: com.yourorg.ResultOfMethodCallIgnoredExample
displayName: Result of method call ignored example
recipeList:
  - org.openrewrite.java.search.ResultOfMethodCallIgnored:
      methodPattern: java.io.File mkdir*()
```
{% endcode %}

Now that `com.yourorg.ResultOfMethodCallIgnoredExample` has been defined activate it in your build file:
{% tabs %}
{% tab title="Gradle" %}
{% code title="build.gradle" %}
```groovy
plugins {
    id("org.openrewrite.rewrite") version("6.1.4")
}

rewrite {
    activeRecipe("com.yourorg.ResultOfMethodCallIgnoredExample")
}

repositories {
    mavenCentral()
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
            <recipe>com.yourorg.ResultOfMethodCallIgnoredExample</recipe>
          </activeRecipes>
        </configuration>
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
* [Sam Snyder](sam@moderne.io)
* [Aaron Gershman](aegershman@gmail.com)


## See how this recipe works across multiple open-source repositories

[![Moderne Link Image](/.gitbook/assets/ModerneRecipeButton.png)](https://app.moderne.io/recipes/org.openrewrite.java.search.ResultOfMethodCallIgnored)

The community edition of the Moderne platform enables you to easily run recipes across thousands of open-source repositories.

Please [contact Moderne](https://moderne.io/product) for more information about safely running the recipes on your own codebase in a private SaaS.
