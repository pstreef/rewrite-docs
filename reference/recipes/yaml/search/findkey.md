# Find YAML entries

**org.openrewrite.yaml.search.FindKey**

_Find YAML entries by JsonPath expression._

## Source

[GitHub](https://github.com/openrewrite/rewrite/blob/main/rewrite-yaml/src/main/java/org/openrewrite/yaml/search/FindKey.java), [Issue Tracker](https://github.com/openrewrite/rewrite/issues), [Maven Central](https://central.sonatype.com/artifact/org.openrewrite/rewrite-yaml/8.1.3/jar)

* groupId: org.openrewrite
* artifactId: rewrite-yaml
* version: 8.1.3

## Options

| Type | Name | Description |
| -- | -- | -- |
| `String` | key | A JsonPath expression used to find matching keys. |

## Example

###### Parameters
| Parameter | Value |
| -- | -- |
|key|`$.metadata.name`|


{% tabs %}
{% tab title="yaml" %}

###### Before
{% code %}
```yaml
    apiVersion: v1
    metadata:
      name: monitoring-tools
      namespace: monitoring-tools
```
{% endcode %}

###### After
{% code %}
```yaml
    apiVersion: v1
    metadata:
      ~~>name: monitoring-tools
      namespace: monitoring-tools
```
{% endcode %}

{% endtab %}
{% tab title="Diff" %}
{% code %}
```diff
@@ -3,1 +3,1 @@
    apiVersion: v1
    metadata:
-     name: monitoring-tools
+     ~~>name: monitoring-tools
      namespace: monitoring-tools
```
{% endcode %}
{% endtab %}
{% endtabs %}


## Usage

This recipe has required configuration parameters. Recipes with required configuration parameters cannot be activated directly. To activate this recipe you must create a new recipe which fills in the required parameters. In your `rewrite.yml` create a new recipe with a unique name. For example: `com.yourorg.FindKeyExample`.
Here's how you can define and customize such a recipe within your rewrite.yml:

{% code title="rewrite.yml" %}
```yaml
---
type: specs.openrewrite.org/v1beta/recipe
name: com.yourorg.FindKeyExample
displayName: Find YAML entries example
recipeList:
  - org.openrewrite.yaml.search.FindKey:
      key: $.subjects.kind
```
{% endcode %}

Now that `com.yourorg.FindKeyExample` has been defined activate it in your build file:
{% tabs %}
{% tab title="Gradle" %}
{% code title="build.gradle" %}
```groovy
plugins {
    id("org.openrewrite.rewrite") version("6.1.4")
}

rewrite {
    activeRecipe("com.yourorg.FindKeyExample")
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
            <recipe>com.yourorg.FindKeyExample</recipe>
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

[![Moderne Link Image](/.gitbook/assets/ModerneRecipeButton.png)](https://app.moderne.io/recipes/org.openrewrite.yaml.search.FindKey)

The community edition of the Moderne platform enables you to easily run recipes across thousands of open-source repositories.

Please [contact Moderne](https://moderne.io/product) for more information about safely running the recipes on your own codebase in a private SaaS.
