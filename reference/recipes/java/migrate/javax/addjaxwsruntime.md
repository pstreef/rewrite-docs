# Use the latest JAX-WS API and runtime for Jakarta EE 8

**org.openrewrite.java.migrate.javax.AddJaxwsRuntime**

_Update build files to use the latest JAX-WS runtime from Jakarta EE 8 to maintain compatibility with Java version 11 or greater. The recipe will add a JAX-WS run-time, in Gradle `compileOnly`+`testImplementation` and Maven `provided` scope, to any project that has a transitive dependency on the JAX-WS API. **The resulting dependencies still use the `javax` namespace, despite the move to the Jakarta artifact**._

### Tags

* javax
* javaee
* java11
* jakarta
* jaxws

## Source

[GitHub](https://github.com/openrewrite/rewrite-migrate-java/blob/main/src/main/java/org/openrewrite/java/migrate/javax/AddJaxwsRuntime.java), [Issue Tracker](https://github.com/openrewrite/rewrite-migrate-java/issues), [Maven Central](https://central.sonatype.com/artifact/org.openrewrite.recipe/rewrite-migrate-java/2.0.1/jar)

* groupId: org.openrewrite.recipe
* artifactId: rewrite-migrate-java
* version: 2.0.1


## Usage

This recipe has no required configuration options. It can be activated by adding a dependency on `org.openrewrite.recipe:rewrite-migrate-java:2.0.1` in your build file or by running a shell command (in which case no build changes are needed): 
{% tabs %}
{% tab title="Gradle" %}
{% code title="build.gradle" %}
```groovy
plugins {
    id("org.openrewrite.rewrite") version("6.1.4")
}

rewrite {
    activeRecipe("org.openrewrite.java.migrate.javax.AddJaxwsRuntime")
}

repositories {
    mavenCentral()
}

dependencies {
    rewrite("org.openrewrite.recipe:rewrite-migrate-java:2.0.1")
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
            <recipe>org.openrewrite.java.migrate.javax.AddJaxwsRuntime</recipe>
          </activeRecipes>
        </configuration>
        <dependencies>
          <dependency>
            <groupId>org.openrewrite.recipe</groupId>
            <artifactId>rewrite-migrate-java</artifactId>
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
  -Drewrite.recipeArtifactCoordinates=org.openrewrite.recipe:rewrite-migrate-java:RELEASE \
  -Drewrite.activeRecipes=org.openrewrite.java.migrate.javax.AddJaxwsRuntime
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Definition

{% tabs %}
{% tab title="Recipe List" %}
* [Use the latest JAX-WS API and runtime for Jakarta EE 8](../../../java/migrate/javax/addjaxwsruntime$addjaxwsruntimegradle.md)
* [Use the latest JAX-WS API and runtime for Jakarta EE 8](../../../java/migrate/javax/addjaxwsruntime$addjaxwsruntimemaven.md)

{% endtab %}

{% tab title="Yaml Recipe List" %}
```yaml
---
type: specs.openrewrite.org/v1beta/recipe
name: org.openrewrite.java.migrate.javax.AddJaxwsRuntime
displayName: Use the latest JAX-WS API and runtime for Jakarta EE 8
description: Update build files to use the latest JAX-WS runtime from Jakarta EE 8 to maintain compatibility with Java version 11 or greater. The recipe will add a JAX-WS run-time, in Gradle `compileOnly`+`testImplementation` and Maven `provided` scope, to any project that has a transitive dependency on the JAX-WS API. **The resulting dependencies still use the `javax` namespace, despite the move to the Jakarta artifact**.
tags:
  - javax
  - javaee
  - java11
  - jakarta
  - jaxws
recipeList:
  - org.openrewrite.java.migrate.javax.AddJaxwsRuntime$AddJaxwsRuntimeGradle
  - org.openrewrite.java.migrate.javax.AddJaxwsRuntime$AddJaxwsRuntimeMaven

```
{% endtab %}
{% endtabs %}

## Contributors
* [Shannon Pamperl](shanman190@gmail.com)
* [Tyler Van Gorder](tkvangorder@users.noreply.github.com)
* [Sam Snyder](sam@moderne.io)


## See how this recipe works across multiple open-source repositories

[![Moderne Link Image](/.gitbook/assets/ModerneRecipeButton.png)](https://app.moderne.io/recipes/org.openrewrite.java.migrate.javax.AddJaxwsRuntime)

The community edition of the Moderne platform enables you to easily run recipes across thousands of open-source repositories.

Please [contact Moderne](https://moderne.io/product) for more information about safely running the recipes on your own codebase in a private SaaS.
