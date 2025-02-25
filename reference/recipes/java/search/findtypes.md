# Find types

**org.openrewrite.java.search.FindTypes**

_Find type references by name._

## Source

[GitHub](https://github.com/openrewrite/rewrite/blob/main/rewrite-java/src/main/java/org/openrewrite/java/search/FindTypes.java), [Issue Tracker](https://github.com/openrewrite/rewrite/issues), [Maven Central](https://central.sonatype.com/artifact/org.openrewrite/rewrite-java/8.1.3/jar)

* groupId: org.openrewrite
* artifactId: rewrite-java
* version: 8.1.3

## Options

| Type | Name | Description |
| -- | -- | -- |
| `String` | fullyQualifiedTypeName | A fully-qualified type name, that is used to find matching type references. Supports glob expressions. `java..*` finds every type from every subpackage of the `java` package. |
| `Boolean` | checkAssignability | *Optional*. When enabled, find type references that are assignable to the provided type. |

## Example

###### Parameters
| Parameter | Value |
| -- | -- |
|fullyQualifiedTypeName|`a.A1`|
|checkAssignability|`false`|


{% tabs %}
{% tab title="B.java" %}

###### Before
{% code title="B.java" %}
```java
import a.A1;
public class B extends A1 {}
```
{% endcode %}

###### After
{% code title="B.java" %}
```java
import a.A1;
public class B extends /*~~>*/A1 {}
```
{% endcode %}

{% endtab %}
{% tab title="Diff" %}
{% code %}
```diff
--- B.java
+++ B.java
@@ -2,1 +2,1 @@
import a.A1;
-public class B extends A1 {}
+public class B extends /*~~>*/A1 {}

```
{% endcode %}
{% endtab %}
{% endtabs %}


## Usage

This recipe has required configuration parameters. Recipes with required configuration parameters cannot be activated directly. To activate this recipe you must create a new recipe which fills in the required parameters. In your `rewrite.yml` create a new recipe with a unique name. For example: `com.yourorg.FindTypesExample`.
Here's how you can define and customize such a recipe within your rewrite.yml:

{% code title="rewrite.yml" %}
```yaml
---
type: specs.openrewrite.org/v1beta/recipe
name: com.yourorg.FindTypesExample
displayName: Find types example
recipeList:
  - org.openrewrite.java.search.FindTypes:
      fullyQualifiedTypeName: java.util.List
      checkAssignability: null
```
{% endcode %}

Now that `com.yourorg.FindTypesExample` has been defined activate it in your build file:
{% tabs %}
{% tab title="Gradle" %}
{% code title="build.gradle" %}
```groovy
plugins {
    id("org.openrewrite.rewrite") version("6.1.4")
}

rewrite {
    activeRecipe("com.yourorg.FindTypesExample")
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
            <recipe>com.yourorg.FindTypesExample</recipe>
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
* [Greg Adams](greg@moderne.io)
* [Tyler Van Gorder](tkvangorder@users.noreply.github.com)


## See how this recipe works across multiple open-source repositories

[![Moderne Link Image](/.gitbook/assets/ModerneRecipeButton.png)](https://app.moderne.io/recipes/org.openrewrite.java.search.FindTypes)

The community edition of the Moderne platform enables you to easily run recipes across thousands of open-source repositories.

Please [contact Moderne](https://moderne.io/product) for more information about safely running the recipes on your own codebase in a private SaaS.
