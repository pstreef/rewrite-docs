# Remove plugin from `build.gradle(.kts)`

**org.openrewrite.gradle.plugins.RemoveBuildPlugin**

_Remove plugin from `build.gradle(.kts)`._

## Source

[GitHub](https://github.com/openrewrite/rewrite/blob/main/rewrite-gradle/src/main/java/org/openrewrite/gradle/plugins/RemoveBuildPlugin.java), [Issue Tracker](https://github.com/openrewrite/rewrite/issues), [Maven Central](https://central.sonatype.com/artifact/org.openrewrite/rewrite-gradle/8.1.3/jar)

* groupId: org.openrewrite
* artifactId: rewrite-gradle
* version: 8.1.3

## Options

| Type | Name | Description |
| -- | -- | -- |
| `String` | pluginId | The plugin id to remove. |

## Example

###### Parameters
| Parameter | Value |
| -- | -- |
|pluginId|`com.jfrog.bintray`|


###### Unchanged
{% code title="build.gradle" %}
```groovy
plugins {
    id "com.jfrog.bintray" version "1.0"
}
```
{% endcode %}


## Usage

This recipe has required configuration parameters. Recipes with required configuration parameters cannot be activated directly. To activate this recipe you must create a new recipe which fills in the required parameters. In your `rewrite.yml` create a new recipe with a unique name. For example: `com.yourorg.RemoveBuildPluginExample`.
Here's how you can define and customize such a recipe within your rewrite.yml:

{% code title="rewrite.yml" %}
```yaml
---
type: specs.openrewrite.org/v1beta/recipe
name: com.yourorg.RemoveBuildPluginExample
displayName: Remove plugin from `build.gradle(.kts)` example
recipeList:
  - org.openrewrite.gradle.plugins.RemoveBuildPlugin:
      pluginId: com.jfrog.bintray
```
{% endcode %}

Now that `com.yourorg.RemoveBuildPluginExample` has been defined activate it in your build file:
{% tabs %}
{% tab title="Gradle" %}
{% code title="build.gradle" %}
```groovy
plugins {
    id("org.openrewrite.rewrite") version("6.1.4")
}

rewrite {
    activeRecipe("com.yourorg.RemoveBuildPluginExample")
}

repositories {
    mavenCentral()
}
```
{% endcode %}
{% endtab %}

{% endtabs %}

## Contributors
* [Shannon Pamperl](shanman190@gmail.com)
* [Jonathan Schnéider](jkschneider@gmail.com)


## See how this recipe works across multiple open-source repositories

[![Moderne Link Image](/.gitbook/assets/ModerneRecipeButton.png)](https://app.moderne.io/recipes/org.openrewrite.gradle.plugins.RemoveBuildPlugin)

The community edition of the Moderne platform enables you to easily run recipes across thousands of open-source repositories.

Please [contact Moderne](https://moderne.io/product) for more information about safely running the recipes on your own codebase in a private SaaS.
