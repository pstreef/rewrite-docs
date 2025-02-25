# Replace constant with literal value

**org.openrewrite.java.ReplaceConstant**

_Replace a named constant with a literal value when you wish to remove the old constant. A `String` literal must include escaped quotes._

## Source

[GitHub](https://github.com/openrewrite/rewrite/blob/main/rewrite-java/src/main/java/org/openrewrite/java/ReplaceConstant.java), [Issue Tracker](https://github.com/openrewrite/rewrite/issues), [Maven Central](https://central.sonatype.com/artifact/org.openrewrite/rewrite-java/8.1.3/jar)

* groupId: org.openrewrite
* artifactId: rewrite-java
* version: 8.1.3

## Options

| Type | Name | Description |
| -- | -- | -- |
| `String` | owningType | The target type in which the constant to be replaced is defined. |
| `String` | constantName | The name of the constant field to replace. |
| `String` | literalValue | The literal value to replace. |

## Example

###### Parameters
| Parameter | Value |
| -- | -- |
|owningType|`com.google.common.base.Charsets`|
|constantName|`UTF_8`|
|literalValue|`"UTF_8"`|


{% tabs %}
{% tab title="Test.java" %}

###### Before
{% code title="Test.java" %}
```java
import com.google.common.base.Charsets;
class Test {
    Object o = Charsets.UTF_8;
}
```
{% endcode %}

###### After
{% code title="Test.java" %}
```java
class Test {
    Object o = "UTF_8";
}
```
{% endcode %}

{% endtab %}
{% tab title="Diff" %}
{% code %}
```diff
--- Test.java
+++ Test.java
@@ -1,1 +1,0 @@
-import com.google.common.base.Charsets;
class Test {
@@ -3,1 +2,1 @@
import com.google.common.base.Charsets;
class Test {
-   Object o = Charsets.UTF_8;
+   Object o = "UTF_8";
}
```
{% endcode %}
{% endtab %}
{% endtabs %}


## Usage

This recipe has required configuration parameters. Recipes with required configuration parameters cannot be activated directly. To activate this recipe you must create a new recipe which fills in the required parameters. In your `rewrite.yml` create a new recipe with a unique name. For example: `com.yourorg.ReplaceConstantExample`.
Here's how you can define and customize such a recipe within your rewrite.yml:

{% code title="rewrite.yml" %}
```yaml
---
type: specs.openrewrite.org/v1beta/recipe
name: com.yourorg.ReplaceConstantExample
displayName: Replace constant with literal value example
recipeList:
  - org.openrewrite.java.ReplaceConstant:
      owningType: com.google.common.base.Charsets
      constantName: UTF_8
      literalValue: UTF_8
```
{% endcode %}

Now that `com.yourorg.ReplaceConstantExample` has been defined activate it in your build file:
{% tabs %}
{% tab title="Gradle" %}
{% code title="build.gradle" %}
```groovy
plugins {
    id("org.openrewrite.rewrite") version("6.1.4")
}

rewrite {
    activeRecipe("com.yourorg.ReplaceConstantExample")
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
            <recipe>com.yourorg.ReplaceConstantExample</recipe>
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
* [Tracey Yoshima](tracey.yoshima@gmail.com)
* [Knut Wannheden](knut.wannheden@mobi.ch)
* [Tyler Van Gorder](tkvangorder@users.noreply.github.com)


## See how this recipe works across multiple open-source repositories

[![Moderne Link Image](/.gitbook/assets/ModerneRecipeButton.png)](https://app.moderne.io/recipes/org.openrewrite.java.ReplaceConstant)

The community edition of the Moderne platform enables you to easily run recipes across thousands of open-source repositories.

Please [contact Moderne](https://moderne.io/product) for more information about safely running the recipes on your own codebase in a private SaaS.
