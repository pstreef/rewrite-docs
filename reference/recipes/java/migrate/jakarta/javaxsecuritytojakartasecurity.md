# Migrate deprecated `javax.security.enterprise` packages to `jakarta.security.enterprise`

**org.openrewrite.java.migrate.jakarta.JavaxSecurityToJakartaSecurity**

_Java EE has been rebranded to Jakarta EE, necessitating a package relocation._

## Source

[GitHub](https://github.com/openrewrite/rewrite-migrate-java/blob/main/src/main/resources/META-INF/rewrite/jakarta-ee-9.yml), [Issue Tracker](https://github.com/openrewrite/rewrite-migrate-java/issues), [Maven Central](https://central.sonatype.com/artifact/org.openrewrite.recipe/rewrite-migrate-java/2.0.1/jar)

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
    activeRecipe("org.openrewrite.java.migrate.jakarta.JavaxSecurityToJakartaSecurity")
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
            <recipe>org.openrewrite.java.migrate.jakarta.JavaxSecurityToJakartaSecurity</recipe>
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
  -Drewrite.activeRecipes=org.openrewrite.java.migrate.jakarta.JavaxSecurityToJakartaSecurity
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Definition

{% tabs %}
{% tab title="Recipe List" %}
* [Add Gradle or Maven dependency](../../../java/dependencies/adddependency.md)
  * groupId: `jakarta.security.enterprise`
  * artifactId: `jakarta.security.enterprise-api`
  * version: `latest.release`
  * onlyIfUsing: `javax.security.enterprise..*`
  * acceptTransitive: `true`
* [Upgrade Gradle or Maven dependency versions](../../../java/dependencies/upgradedependencyversion.md)
  * groupId: `jakarta.security.enterprise`
  * artifactId: `jakarta.security.enterprise-api`
  * newVersion: `latest.release`
* [Rename package name](../../../java/changepackage.md)
  * oldPackageName: `javax.security.enterprise`
  * newPackageName: `jakarta.security.enterprise`
  * recursive: `true`
* [Remove a Gradle or Maven dependency](../../../java/dependencies/removedependency.md)
  * groupId: `javax.security.enterprise`
  * artifactId: `javax.security.enterprise-api`

{% endtab %}

{% tab title="Yaml Recipe List" %}
```yaml
---
type: specs.openrewrite.org/v1beta/recipe
name: org.openrewrite.java.migrate.jakarta.JavaxSecurityToJakartaSecurity
displayName: Migrate deprecated `javax.security.enterprise` packages to `jakarta.security.enterprise`
description: Java EE has been rebranded to Jakarta EE, necessitating a package relocation.
recipeList:
  - org.openrewrite.java.dependencies.AddDependency:
      groupId: jakarta.security.enterprise
      artifactId: jakarta.security.enterprise-api
      version: latest.release
      onlyIfUsing: javax.security.enterprise..*
      acceptTransitive: true
  - org.openrewrite.java.dependencies.UpgradeDependencyVersion:
      groupId: jakarta.security.enterprise
      artifactId: jakarta.security.enterprise-api
      newVersion: latest.release
  - org.openrewrite.java.ChangePackage:
      oldPackageName: javax.security.enterprise
      newPackageName: jakarta.security.enterprise
      recursive: true
  - org.openrewrite.java.dependencies.RemoveDependency:
      groupId: javax.security.enterprise
      artifactId: javax.security.enterprise-api

```
{% endtab %}
{% endtabs %}

## See how this recipe works across multiple open-source repositories

[![Moderne Link Image](/.gitbook/assets/ModerneRecipeButton.png)](https://app.moderne.io/recipes/org.openrewrite.java.migrate.jakarta.JavaxSecurityToJakartaSecurity)

The community edition of the Moderne platform enables you to easily run recipes across thousands of open-source repositories.

Please [contact Moderne](https://moderne.io/product) for more information about safely running the recipes on your own codebase in a private SaaS.
