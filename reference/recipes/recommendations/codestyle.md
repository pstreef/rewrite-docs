# Code Style

**org.openrewrite.recommendations.CodeStyle**

_Used for Code Style metric on moderne radar._

### Tags

* radar
* health check

## Source

[GitHub](https://github.com/openrewrite/rewrite-recommendations/blob/main/src/main/resources/META-INF/rewrite/radar.yml), [Issue Tracker](https://github.com/openrewrite/rewrite-recommendations/issues), [Maven Central](https://central.sonatype.com/artifact/org.openrewrite.recipe/rewrite-recommendations/1.0.1/jar)

* groupId: org.openrewrite.recipe
* artifactId: rewrite-recommendations
* version: 1.0.1


## Usage

This recipe has no required configuration options. It can be activated by adding a dependency on `org.openrewrite.recipe:rewrite-recommendations:1.0.1` in your build file or by running a shell command (in which case no build changes are needed): 
{% tabs %}
{% tab title="Gradle" %}
{% code title="build.gradle" %}
```groovy
plugins {
    id("org.openrewrite.rewrite") version("6.1.4")
}

rewrite {
    activeRecipe("org.openrewrite.recommendations.CodeStyle")
}

repositories {
    mavenCentral()
}

dependencies {
    rewrite("org.openrewrite.recipe:rewrite-recommendations:1.0.1")
}
```
{% endcode %}
{% endtab %}
{% tab title="Maven POM" %}
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
            <recipe>org.openrewrite.recommendations.CodeStyle</recipe>
          </activeRecipes>
        </configuration>
        <dependencies>
          <dependency>
            <groupId>org.openrewrite.recipe</groupId>
            <artifactId>rewrite-recommendations</artifactId>
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

{% tab title="Maven Command Line" %}
{% code title="shell" %}
You will need to have [Maven](https://maven.apache.org/download.cgi) installed on your machine before you can run the following command.

```shell
mvn -U org.openrewrite.maven:rewrite-maven-plugin:run \
  -Drewrite.recipeArtifactCoordinates=org.openrewrite.recipe:rewrite-recommendations:RELEASE \
  -Drewrite.activeRecipes=org.openrewrite.recommendations.CodeStyle
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Definition

{% tabs %}
{% tab title="Recipe List" %}
* [Format Java code](../java/format/autoformat.md)
* [Blank lines](../java/format/blanklines.md)
* [Remove trailing whitespace](../java/format/removetrailingwhitespace.md)
* [Wrapping and braces](../java/format/wrappingandbraces.md)
* [No C-style array declarations](../staticanalysis/usejavastylearraydeclarations.md)
* [Format HCL code](../hcl/format/autoformat.md)
* [Remove unnecessary parentheses](../java/cleanup/unnecessaryparentheses.md)
* [Remove extra semicolons](../staticanalysis/removeextrasemicolons.md)

{% endtab %}

{% tab title="Yaml Recipe List" %}
```yaml
---
type: specs.openrewrite.org/v1beta/recipe
name: org.openrewrite.recommendations.CodeStyle
displayName: Code Style
description: Used for Code Style metric on moderne radar.
tags:
  - radar
  - health check
recipeList:
  - org.openrewrite.java.format.AutoFormat
  - org.openrewrite.java.format.BlankLines
  - org.openrewrite.java.format.RemoveTrailingWhitespace
  - org.openrewrite.java.format.WrappingAndBraces
  - org.openrewrite.staticanalysis.UseJavaStyleArrayDeclarations
  - org.openrewrite.hcl.format.AutoFormat
  - org.openrewrite.java.cleanup.UnnecessaryParentheses
  - org.openrewrite.staticanalysis.RemoveExtraSemicolons

```
{% endtab %}
{% endtabs %}

## See how this recipe works across multiple open-source repositories

[![Moderne Link Image](/.gitbook/assets/ModerneRecipeButton.png)](https://app.moderne.io/recipes/org.openrewrite.recommendations.CodeStyle)

The community edition of the Moderne platform enables you to easily run recipes across thousands of open-source repositories.

Please [contact Moderne](https://moderne.io/product) for more information about safely running the recipes on your own codebase in a private SaaS.
