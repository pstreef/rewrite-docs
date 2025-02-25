# Find property

**org.openrewrite.properties.search.FindProperties**

_Finds occurrences of a property key._

## Source

[GitHub](https://github.com/openrewrite/rewrite/blob/main/rewrite-properties/src/main/java/org/openrewrite/properties/search/FindProperties.java), [Issue Tracker](https://github.com/openrewrite/rewrite/issues), [Maven Central](https://central.sonatype.com/artifact/org.openrewrite/rewrite-properties/8.1.3/jar)

* groupId: org.openrewrite
* artifactId: rewrite-properties
* version: 8.1.3

## Options

| Type | Name | Description |
| -- | -- | -- |
| `String` | propertyKey | The property key to look for. |
| `Boolean` | relaxedBinding | *Optional*. Whether to match the `propertyKey` using [relaxed binding](https://docs.spring.io/spring-boot/docs/2.5.6/reference/html/features.html#features.external-config.typesafe-configuration-properties.relaxed-binding) rules. Default is `true`. Set to `false`  to use exact matching. |

## Example

###### Parameters
| Parameter | Value |
| -- | -- |
|propertyKey|`management.metrics.binders.files.enabled`|
|relaxedBinding|`null`|


{% tabs %}
{% tab title="properties" %}

###### Before
{% code %}
```properties
management.metrics.binders.files.enabled=true
```
{% endcode %}

###### After
{% code %}
```properties
management.metrics.binders.files.enabled=~~>true
```
{% endcode %}

{% endtab %}
{% tab title="Diff" %}
{% code %}
```diff
@@ -1,1 +1,1 @@
-management.metrics.binders.files.enabled=true
+management.metrics.binders.files.enabled=~~>true
```
{% endcode %}
{% endtab %}
{% endtabs %}


## Usage

This recipe has required configuration parameters. Recipes with required configuration parameters cannot be activated directly. To activate this recipe you must create a new recipe which fills in the required parameters. In your `rewrite.yml` create a new recipe with a unique name. For example: `com.yourorg.FindPropertiesExample`.
Here's how you can define and customize such a recipe within your rewrite.yml:

{% code title="rewrite.yml" %}
```yaml
---
type: specs.openrewrite.org/v1beta/recipe
name: com.yourorg.FindPropertiesExample
displayName: Find property example
recipeList:
  - org.openrewrite.properties.search.FindProperties:
      propertyKey: management.metrics.binders.files.enabled
      relaxedBinding: null
```
{% endcode %}

Now that `com.yourorg.FindPropertiesExample` has been defined activate it in your build file:
{% tabs %}
{% tab title="Gradle" %}
{% code title="build.gradle" %}
```groovy
plugins {
    id("org.openrewrite.rewrite") version("6.1.4")
}

rewrite {
    activeRecipe("com.yourorg.FindPropertiesExample")
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
            <recipe>com.yourorg.FindPropertiesExample</recipe>
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
* [Greg Adams](greg@moderne.io)
* [Jonathan Schneider](jkschneider@gmail.com)
* [Aaron Gershman](aegershman@gmail.com)
* [Sam Snyder](sam@moderne.io)


## See how this recipe works across multiple open-source repositories

[![Moderne Link Image](/.gitbook/assets/ModerneRecipeButton.png)](https://app.moderne.io/recipes/org.openrewrite.properties.search.FindProperties)

The community edition of the Moderne platform enables you to easily run recipes across thousands of open-source repositories.

Please [contact Moderne](https://moderne.io/product) for more information about safely running the recipes on your own codebase in a private SaaS.
