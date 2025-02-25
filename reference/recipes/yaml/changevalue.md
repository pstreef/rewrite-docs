# Change value

**org.openrewrite.yaml.ChangeValue**

_Change a YAML mapping entry value leaving the key intact._

## Source

[GitHub](https://github.com/openrewrite/rewrite/blob/main/rewrite-yaml/src/main/java/org/openrewrite/yaml/ChangeValue.java), [Issue Tracker](https://github.com/openrewrite/rewrite/issues), [Maven Central](https://central.sonatype.com/artifact/org.openrewrite/rewrite-yaml/8.1.3/jar)

* groupId: org.openrewrite
* artifactId: rewrite-yaml
* version: 8.1.3

## Options

| Type | Name | Description |
| -- | -- | -- |
| `String` | oldKeyPath | A JsonPath expression to locate a YAML entry. |
| `String` | value | The new value to set for the key identified by oldKeyPath. |

## Example

###### Parameters
| Parameter | Value |
| -- | -- |
|oldKeyPath|`$.metadata.name`|
|value|`monitoring`|


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
      name: monitoring
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
+     name: monitoring
      namespace: monitoring-tools
```
{% endcode %}
{% endtab %}
{% endtabs %}


## Usage

This recipe has required configuration parameters. Recipes with required configuration parameters cannot be activated directly. To activate this recipe you must create a new recipe which fills in the required parameters. In your `rewrite.yml` create a new recipe with a unique name. For example: `com.yourorg.ChangeValueExample`.
Here's how you can define and customize such a recipe within your rewrite.yml:

{% code title="rewrite.yml" %}
```yaml
---
type: specs.openrewrite.org/v1beta/recipe
name: com.yourorg.ChangeValueExample
displayName: Change value example
recipeList:
  - org.openrewrite.yaml.ChangeValue:
      oldKeyPath: $.subjects.kind
      value: Deployment
```
{% endcode %}

Now that `com.yourorg.ChangeValueExample` has been defined activate it in your build file:
{% tabs %}
{% tab title="Gradle" %}
{% code title="build.gradle" %}
```groovy
plugins {
    id("org.openrewrite.rewrite") version("6.1.4")
}

rewrite {
    activeRecipe("com.yourorg.ChangeValueExample")
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
            <recipe>com.yourorg.ChangeValueExample</recipe>
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
* [traceyyoshima](tracey.yoshima@gmail.com)
* [Aaron Gershman](5619476+aegershman@users.noreply.github.com)
* [Sam Snyder](sam@moderne.io)


## See how this recipe works across multiple open-source repositories

[![Moderne Link Image](/.gitbook/assets/ModerneRecipeButton.png)](https://app.moderne.io/recipes/org.openrewrite.yaml.ChangeValue)

The community edition of the Moderne platform enables you to easily run recipes across thousands of open-source repositories.

Please [contact Moderne](https://moderne.io/product) for more information about safely running the recipes on your own codebase in a private SaaS.
