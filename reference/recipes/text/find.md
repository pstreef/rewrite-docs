# Find text

**org.openrewrite.text.Find**

_Search for text, treating all textual sources as plain text._

## Source

[GitHub](https://github.com/openrewrite/rewrite/blob/main/rewrite-core/src/main/java/org/openrewrite/text/Find.java), [Issue Tracker](https://github.com/openrewrite/rewrite/issues), [Maven Central](https://central.sonatype.com/artifact/org.openrewrite/rewrite-core/8.1.3/jar)

* groupId: org.openrewrite
* artifactId: rewrite-core
* version: 8.1.3

## Options

| Type | Name | Description |
| -- | -- | -- |
| `String` | find | The text to find. |
| `Boolean` | regex | *Optional*. If true, `find` will be interpreted as a Regular Expression. Default `false`. |
| `Boolean` | caseInsensitive | *Optional*. If `true` the search will be insensitive to case. Default `false`. |
| `Boolean` | multiline | *Optional*. When performing a regex search setting this to `true` allows "^" and "$" to match the beginning and end of lines, respectively. When performing a regex search when this is `false` "^" and "$" will match only the beginning and ending of the entire source file, respectively.Has no effect when not performing a regex search. Default `false`. |
| `Boolean` | dotAll | *Optional*. When performing a regex search setting this to `true` allows "." to match line terminators.Has no effect when not performing a regex search. Default `false`. |
| `String` | filePattern | A glob expression that can be used to constrain which directories or source files should be searched. When not set, all source files are searched. |


## Usage

This recipe has required configuration parameters. Recipes with required configuration parameters cannot be activated directly. To activate this recipe you must create a new recipe which fills in the required parameters. In your `rewrite.yml` create a new recipe with a unique name. For example: `com.yourorg.FindExample`.
Here's how you can define and customize such a recipe within your rewrite.yml:

{% code title="rewrite.yml" %}
```yaml
---
type: specs.openrewrite.org/v1beta/recipe
name: com.yourorg.FindExample
displayName: Find text example
recipeList:
  - org.openrewrite.text.Find:
      find: blacklist
      regex: null
      caseInsensitive: null
      multiline: null
      dotAll: null
      filePattern: '**/*.java'
```
{% endcode %}

Now that `com.yourorg.FindExample` has been defined activate it in your build file:
{% tabs %}
{% tab title="Gradle" %}
{% code title="build.gradle" %}
```groovy
plugins {
    id("org.openrewrite.rewrite") version("6.1.4")
}

rewrite {
    activeRecipe("com.yourorg.FindExample")
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
            <recipe>com.yourorg.FindExample</recipe>
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

[![Moderne Link Image](/.gitbook/assets/ModerneRecipeButton.png)](https://app.moderne.io/recipes/org.openrewrite.text.Find)

The community edition of the Moderne platform enables you to easily run recipes across thousands of open-source repositories.

Please [contact Moderne](https://moderne.io/product) for more information about safely running the recipes on your own codebase in a private SaaS.
