# Control Flow Visualization

**org.openrewrite.analysis.controlflow.ControlFlowVisualization**

_Visualize the control flow of a Java program._

## Source

[GitHub](https://github.com/openrewrite/rewrite-analysis/blob/main/src/main/java/org/openrewrite/analysis/controlflow/ControlFlowVisualization.java), [Issue Tracker](https://github.com/openrewrite/rewrite-analysis/issues), [Maven Central](https://central.sonatype.com/artifact/org.openrewrite.meta/rewrite-analysis/2.0.1/jar)

* groupId: org.openrewrite.meta
* artifactId: rewrite-analysis
* version: 2.0.1

## Options

| Type | Name | Description |
| -- | -- | -- |
| `boolean` | includeDotfile | Also output with a Dotfile which can be then later visualized by Graphviz. |

## Example

###### Parameters
| Parameter | Value |
| -- | -- |
|includeDotfile|`false`|


{% tabs %}
{% tab title="Test.java" %}

###### Before
{% code title="Test.java" %}
```java
abstract class Test {
    abstract int start();
    void test() {
        int x = start();
        x++;
    }
}
```
{% endcode %}

###### After
{% code title="Test.java" %}
```java
abstract class Test {
    abstract int start();
    void test() /*~~(BB: 1 CN: 0 EX: 1 | 1L)~~>*/{
        int x = start();
        x++;
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
@@ -3,1 +3,1 @@
abstract class Test {
    abstract int start();
-   void test() {
+   void test() /*~~(BB: 1 CN: 0 EX: 1 | 1L)~~>*/{
        int x = start();
```
{% endcode %}
{% endtab %}
{% endtabs %}


## Usage

This recipe has required configuration parameters. Recipes with required configuration parameters cannot be activated directly. To activate this recipe you must create a new recipe which fills in the required parameters. In your `rewrite.yml` create a new recipe with a unique name. For example: `com.yourorg.ControlFlowVisualizationExample`.
Here's how you can define and customize such a recipe within your rewrite.yml:

{% code title="rewrite.yml" %}
```yaml
---
type: specs.openrewrite.org/v1beta/recipe
name: com.yourorg.ControlFlowVisualizationExample
displayName: Control Flow Visualization example
recipeList:
  - org.openrewrite.analysis.controlflow.ControlFlowVisualization:
      includeDotfile: null
```
{% endcode %}

Now that `com.yourorg.ControlFlowVisualizationExample` has been defined activate it and take a dependency on org.openrewrite.meta:rewrite-analysis:2.0.1 in your build file:
{% tabs %}
{% tab title="Gradle" %}
{% code title="build.gradle" %}
```groovy
plugins {
    id("org.openrewrite.rewrite") version("6.1.4")
}

rewrite {
    activeRecipe("com.yourorg.ControlFlowVisualizationExample")
}

repositories {
    mavenCentral()
}

dependencies {
    rewrite("org.openrewrite.meta:rewrite-analysis:2.0.1")
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
            <recipe>com.yourorg.ControlFlowVisualizationExample</recipe>
          </activeRecipes>
        </configuration>
        <dependencies>
          <dependency>
            <groupId>org.openrewrite.meta</groupId>
            <artifactId>rewrite-analysis</artifactId>
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
{% endtabs %}

## Contributors
* [Jonathan Leitschuh](Jonathan.Leitschuh@gmail.com)
* [Knut Wannheden](knut@moderne.io)


## See how this recipe works across multiple open-source repositories

[![Moderne Link Image](/.gitbook/assets/ModerneRecipeButton.png)](https://app.moderne.io/recipes/org.openrewrite.analysis.controlflow.ControlFlowVisualization)

The community edition of the Moderne platform enables you to easily run recipes across thousands of open-source repositories.

Please [contact Moderne](https://moderne.io/product) for more information about safely running the recipes on your own codebase in a private SaaS.
