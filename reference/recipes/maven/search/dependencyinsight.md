# Maven dependency insight

**org.openrewrite.maven.search.DependencyInsight**

_Find direct and transitive dependencies matching a group, artifact, and scope. Results include dependencies that either directly match or transitively include a matching dependency._

## Source

[GitHub](https://github.com/openrewrite/rewrite/blob/main/rewrite-maven/src/main/java/org/openrewrite/maven/search/DependencyInsight.java), [Issue Tracker](https://github.com/openrewrite/rewrite/issues), [Maven Central](https://central.sonatype.com/artifact/org.openrewrite/rewrite-maven/8.1.3/jar)

* groupId: org.openrewrite
* artifactId: rewrite-maven
* version: 8.1.3

## Options

| Type | Name | Description |
| -- | -- | -- |
| `String` | groupIdPattern | Group glob pattern used to match dependencies. |
| `String` | artifactIdPattern | Artifact glob pattern used to match dependencies. |
| `String` | scope | Match dependencies with the specified scope |
| `Boolean` | onlyDirect | *Optional*. Default false. If enabled, transitive dependencies will not be considered. |

## Data Tables (Only available on the [Moderne platform](https://app.moderne.io/))

### Dependencies in use

_Direct and transitive dependencies in use._

| Column Name | Description |
| ----------- | ----------- |
| Project name | The name of the project that contains the dependency. |
| Source set | The source set that contains the dependency. |
| Group | The first part of a dependency coordinate `com.google.guava:guava:VERSION`. |
| Artifact | The second part of a dependency coordinate `com.google.guava:guava:VERSION`. |
| Version | The resolved version. |
| Dated snapshot version | The resolved dated snapshot version or `null` if this dependency is not a snapshot. |
| Scope | Dependency scope. This will be `compile` if the dependency is direct and a scope is not explicitly specified in the POM. |
| Depth | How many levels removed from a direct dependency. This will be 0 for direct dependencies. |

## Example

###### Parameters
| Parameter | Value |
| -- | -- |
|groupIdPattern|`*guava*`|
|artifactIdPattern|`*`|
|scope|`compile`|
|onlyDirect|`null`|


{% tabs %}
{% tab title="pom.xml" %}

###### Before
{% code title="pom.xml" %}
```xml
<project>
  <groupId>com.mycompany.app</groupId>
  <artifactId>my-app</artifactId>
  <version>1</version>
  <dependencies>
    <dependency>
        <groupId>com.google.guava</groupId>
        <artifactId>guava</artifactId>
        <version>29.0-jre</version>
    </dependency>
  </dependencies>
</project>
```
{% endcode %}

###### After
{% code title="pom.xml" %}
```xml
<project>
  <groupId>com.mycompany.app</groupId>
  <artifactId>my-app</artifactId>
  <version>1</version>
  <dependencies>
    <!--~~>--><dependency>
        <groupId>com.google.guava</groupId>
        <artifactId>guava</artifactId>
        <version>29.0-jre</version>
    </dependency>
  </dependencies>
</project>
```
{% endcode %}

{% endtab %}
{% tab title="Diff" %}
{% code %}
```diff
--- pom.xml
+++ pom.xml
@@ -6,1 +6,1 @@
  <version>1</version>
  <dependencies>
-   <dependency>
+   <!--~~>--><dependency>
        <groupId>com.google.guava</groupId>
```
{% endcode %}
{% endtab %}
{% endtabs %}


## Usage

This recipe has required configuration parameters. Recipes with required configuration parameters cannot be activated directly. To activate this recipe you must create a new recipe which fills in the required parameters. In your `rewrite.yml` create a new recipe with a unique name. For example: `com.yourorg.DependencyInsightExample`.
Here's how you can define and customize such a recipe within your rewrite.yml:

{% code title="rewrite.yml" %}
```yaml
---
type: specs.openrewrite.org/v1beta/recipe
name: com.yourorg.DependencyInsightExample
displayName: Maven dependency insight example
recipeList:
  - org.openrewrite.maven.search.DependencyInsight:
      groupIdPattern: com.fasterxml.jackson.module
      artifactIdPattern: jackson-module-*
      scope: compile
      onlyDirect: true
```
{% endcode %}

Now that `com.yourorg.DependencyInsightExample` has been defined activate it in your build file:
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
            <recipe>com.yourorg.DependencyInsightExample</recipe>
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
* [Nick McKinney](mckinneynicholas@gmail.com)
* [Sam Snyder](sam@moderne.io)
* [Tracey Yoshima](tracey.yoshima@gmail.com)
* [Jonathan Leitschuh](jonathan.leitschuh@gmail.com)


## See how this recipe works across multiple open-source repositories

[![Moderne Link Image](/.gitbook/assets/ModerneRecipeButton.png)](https://app.moderne.io/recipes/org.openrewrite.maven.search.DependencyInsight)

The community edition of the Moderne platform enables you to easily run recipes across thousands of open-source repositories.

Please [contact Moderne](https://moderne.io/product) for more information about safely running the recipes on your own codebase in a private SaaS.
