# Find uses of JCache

**org.openrewrite.cloudsuitability.FindJCache**

_Convert to redis or consider TKG._

### Tags

* java-jcache

## Source

[GitHub](https://github.com/openrewrite/rewrite-cloud-suitability-analyzer/blob/main/src/main/resources/META-INF/rewrite/finders.yml), [Issue Tracker](https://github.com/openrewrite/rewrite-cloud-suitability-analyzer/issues), [Maven Central](https://central.sonatype.com/artifact/org.openrewrite.recipe/rewrite-cloud-suitability-analyzer/2.0.1/jar)

* groupId: org.openrewrite.recipe
* artifactId: rewrite-cloud-suitability-analyzer
* version: 2.0.1


## Usage

This recipe has no required configuration options. It can be activated by adding a dependency on `org.openrewrite.recipe:rewrite-cloud-suitability-analyzer:2.0.1` in your build file or by running a shell command (in which case no build changes are needed): 
{% tabs %}
{% tab title="Gradle" %}
{% code title="build.gradle" %}
```groovy
plugins {
    id("org.openrewrite.rewrite") version("6.1.4")
}

rewrite {
    activeRecipe("org.openrewrite.cloudsuitability.FindJCache")
}

repositories {
    mavenCentral()
}

dependencies {
    rewrite("org.openrewrite.recipe:rewrite-cloud-suitability-analyzer:2.0.1")
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
            <recipe>org.openrewrite.cloudsuitability.FindJCache</recipe>
          </activeRecipes>
        </configuration>
        <dependencies>
          <dependency>
            <groupId>org.openrewrite.recipe</groupId>
            <artifactId>rewrite-cloud-suitability-analyzer</artifactId>
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

{% tab title="Maven Command Line" %}
{% code title="shell" %}
You will need to have [Maven](https://maven.apache.org/download.cgi) installed on your machine before you can run the following command.

```shell
mvn -U org.openrewrite.maven:rewrite-maven-plugin:run \
  -Drewrite.recipeArtifactCoordinates=org.openrewrite.recipe:rewrite-cloud-suitability-analyzer:RELEASE \
  -Drewrite.activeRecipes=org.openrewrite.cloudsuitability.FindJCache
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Definition

{% tabs %}
{% tab title="Recipe List" %}
* [Find types](../java/search/findtypes.md)
  * fullyQualifiedTypeName: `javax.cache..*`

{% endtab %}

{% tab title="Yaml Recipe List" %}
```yaml
---
type: specs.openrewrite.org/v1beta/recipe
name: org.openrewrite.cloudsuitability.FindJCache
displayName: Find uses of JCache
description: Convert to redis or consider TKG.
tags:
  - java-jcache
recipeList:
  - org.openrewrite.java.search.FindTypes:
      fullyQualifiedTypeName: javax.cache..*

```
{% endtab %}
{% endtabs %}

## See how this recipe works across multiple open-source repositories

[![Moderne Link Image](/.gitbook/assets/ModerneRecipeButton.png)](https://app.moderne.io/recipes/org.openrewrite.cloudsuitability.FindJCache)

The community edition of the Moderne platform enables you to easily run recipes across thousands of open-source repositories.

Please [contact Moderne](https://moderne.io/product) for more information about safely running the recipes on your own codebase in a private SaaS.
