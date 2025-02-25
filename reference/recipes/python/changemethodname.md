# Example recipe to change a method name

**org.openrewrite.python.ChangeMethodName**

_Renames a method._

## Source

[GitHub](https://github.com/openrewrite/rewrite-python/blob/main/src/main/java/org/openrewrite/python/ChangeMethodName.java), [Issue Tracker](https://github.com/openrewrite/rewrite-python/issues), [Maven Central](https://central.sonatype.com/artifact/org.openrewrite/rewrite-python/1.0.1/jar)

* groupId: org.openrewrite
* artifactId: rewrite-python
* version: 1.0.1

## Options

| Type | Name | Description |
| -- | -- | -- |
| `String` | oldMethodName | The method name that will replace the existing name. |
| `String` | newMethodName | The method name that will replace the existing name. |
| `Boolean` | ignoreDefinition | *Optional*. When set to `true` the definition of the old type will be left untouched. This is useful when you're replacing usage of a class but don't want to rename it. |


## Usage

This recipe has required configuration parameters. Recipes with required configuration parameters cannot be activated directly. To activate this recipe you must create a new recipe which fills in the required parameters. In your `rewrite.yml` create a new recipe with a unique name. For example: `com.yourorg.ChangeMethodNameExample`.
Here's how you can define and customize such a recipe within your rewrite.yml:

{% code title="rewrite.yml" %}
```yaml
---
type: specs.openrewrite.org/v1beta/recipe
name: com.yourorg.ChangeMethodNameExample
displayName: Example recipe to change a method name example
recipeList:
  - org.openrewrite.python.ChangeMethodName:
      oldMethodName: any
      newMethodName: any
      ignoreDefinition: null
```
{% endcode %}

Now that `com.yourorg.ChangeMethodNameExample` has been defined activate it and take a dependency on org.openrewrite:rewrite-python:1.0.1 in your build file:
{% tabs %}
{% tab title="Gradle" %}
{% code title="build.gradle" %}
```groovy
plugins {
    id("org.openrewrite.rewrite") version("6.1.4")
}

rewrite {
    activeRecipe("com.yourorg.ChangeMethodNameExample")
}

repositories {
    mavenCentral()
}

dependencies {
    rewrite("org.openrewrite:rewrite-python:1.0.1")
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
            <recipe>com.yourorg.ChangeMethodNameExample</recipe>
          </activeRecipes>
        </configuration>
        <dependencies>
          <dependency>
            <groupId>org.openrewrite</groupId>
            <artifactId>rewrite-python</artifactId>
            <version>1.0.1</version>
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
* [traceyyoshima](tracey.yoshima@gmail.com)
* [Knut Wannheden](knut@moderne.io)


## See how this recipe works across multiple open-source repositories

[![Moderne Link Image](/.gitbook/assets/ModerneRecipeButton.png)](https://app.moderne.io/recipes/org.openrewrite.python.ChangeMethodName)

The community edition of the Moderne platform enables you to easily run recipes across thousands of open-source repositories.

Please [contact Moderne](https://moderne.io/product) for more information about safely running the recipes on your own codebase in a private SaaS.
