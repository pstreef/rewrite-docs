# Change Maven plugin dependencies

**org.openrewrite.maven.ChangePluginDependencies**

_Applies the specified dependencies to a Maven plugin. Will not add the plugin if it does not already exist in the pom._

## Source

[GitHub](https://github.com/openrewrite/rewrite/blob/main/rewrite-maven/src/main/java/org/openrewrite/maven/ChangePluginDependencies.java), [Issue Tracker](https://github.com/openrewrite/rewrite/issues), [Maven Central](https://central.sonatype.com/artifact/org.openrewrite/rewrite-maven/8.1.3/jar)

* groupId: org.openrewrite
* artifactId: rewrite-maven
* version: 8.1.3

## Options

| Type | Name | Description |
| -- | -- | -- |
| `String` | groupId | The first part of a dependency coordinate 'org.openrewrite.maven:rewrite-maven-plugin:VERSION'. |
| `String` | artifactId | The second part of a dependency coordinate 'org.openrewrite.maven:rewrite-maven-plugin:VERSION'. |
| `String` | dependencies | *Optional*. Plugin dependencies provided as dependency coordinates of format "groupId:artifactId:version". When supplying multiple coordinates separate them with ",". Supplying `null` will remove any existing plugin dependencies. |

## Example

###### Parameters
| Parameter | Value |
| -- | -- |
|groupId|`org.openrewrite.maven`|
|artifactId|`rewrite-maven-plugin`|
|dependencies|`null`|


{% tabs %}
{% tab title="pom.xml" %}

###### Before
{% code title="pom.xml" %}
```xml
<project>
    <groupId>org.example</groupId>
    <artifactId>foo</artifactId>
    <version>1.0</version>

    <build>
        <plugins>
            <plugin>
                <groupId>org.openrewrite.maven</groupId>
                <artifactId>rewrite-maven-plugin</artifactId>
                <version>4.1.5</version>
                <dependencies>
                    <dependency>
                        <groupId>org.openrewrite.recipe</groupId>
                        <artifactId>rewrite-spring</artifactId>
                        <version>1.0.0</version>
                    </dependency>
                </dependencies>
            </plugin>
        </plugins>
    </build>
</project>
```
{% endcode %}

###### After
{% code title="pom.xml" %}
```xml
<project>
    <groupId>org.example</groupId>
    <artifactId>foo</artifactId>
    <version>1.0</version>

    <build>
        <plugins>
            <plugin>
                <groupId>org.openrewrite.maven</groupId>
                <artifactId>rewrite-maven-plugin</artifactId>
                <version>4.1.5</version>
            </plugin>
        </plugins>
    </build>
</project>
```
{% endcode %}

{% endtab %}
{% tab title="Diff" %}
{% code %}
```diff
--- pom.xml
+++ pom.xml
@@ -12,7 +12,0 @@
                <artifactId>rewrite-maven-plugin</artifactId>
                <version>4.1.5</version>
-               <dependencies>
-                   <dependency>
-                       <groupId>org.openrewrite.recipe</groupId>
-                       <artifactId>rewrite-spring</artifactId>
-                       <version>1.0.0</version>
-                   </dependency>
-               </dependencies>
            </plugin>
```
{% endcode %}
{% endtab %}
{% endtabs %}


## Usage

This recipe has required configuration parameters. Recipes with required configuration parameters cannot be activated directly. To activate this recipe you must create a new recipe which fills in the required parameters. In your `rewrite.yml` create a new recipe with a unique name. For example: `com.yourorg.ChangePluginDependenciesExample`.
Here's how you can define and customize such a recipe within your rewrite.yml:

{% code title="rewrite.yml" %}
```yaml
---
type: specs.openrewrite.org/v1beta/recipe
name: com.yourorg.ChangePluginDependenciesExample
displayName: Change Maven plugin dependencies example
recipeList:
  - org.openrewrite.maven.ChangePluginDependencies:
      groupId: org.openrewrite.maven
      artifactId: rewrite-maven-plugin
      dependencies: org.openrewrite.recipe:rewrite-spring:1.0.0, org.openrewrite.recipe:rewrite-testing-frameworks:1.0.0
```
{% endcode %}

Now that `com.yourorg.ChangePluginDependenciesExample` has been defined activate it in your build file:
{% tabs %}

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
            <recipe>com.yourorg.ChangePluginDependenciesExample</recipe>
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
* [Sam Snyder](sam@moderne.io)
* [Jonathan Schnéider](jkschneider@gmail.com)


## See how this recipe works across multiple open-source repositories

[![Moderne Link Image](/.gitbook/assets/ModerneRecipeButton.png)](https://app.moderne.io/recipes/org.openrewrite.maven.ChangePluginDependencies)

The community edition of the Moderne platform enables you to easily run recipes across thousands of open-source repositories.

Please [contact Moderne](https://moderne.io/product) for more information about safely running the recipes on your own codebase in a private SaaS.
