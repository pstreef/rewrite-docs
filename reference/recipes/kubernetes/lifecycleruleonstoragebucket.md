# Ensure lifecycle rule on `StorageBucket`

**org.openrewrite.kubernetes.LifecycleRuleOnStorageBucket**

_When defining a rule, you can specify any set of conditions for any action. The following configuration defines a rule to delete all objects older than 7 days in a bucket._

### Tags

* kubernetes

## Source

[GitHub](https://github.com/openrewrite/rewrite-kubernetes/blob/main/src/main/resources/META-INF/rewrite/kubernetes.yml), [Issue Tracker](https://github.com/openrewrite/rewrite-kubernetes/issues), [Maven Central](https://central.sonatype.com/artifact/org.openrewrite.recipe/rewrite-kubernetes/2.0.1/jar)

* groupId: org.openrewrite.recipe
* artifactId: rewrite-kubernetes
* version: 2.0.1


## Usage

This recipe has no required configuration options. It can be activated by adding a dependency on `org.openrewrite.recipe:rewrite-kubernetes:2.0.1` in your build file or by running a shell command (in which case no build changes are needed): 
{% tabs %}
{% tab title="Gradle" %}
{% code title="build.gradle" %}
```groovy
plugins {
    id("org.openrewrite.rewrite") version("6.1.4")
}

rewrite {
    activeRecipe("org.openrewrite.kubernetes.LifecycleRuleOnStorageBucket")
}

repositories {
    mavenCentral()
}

dependencies {
    rewrite("org.openrewrite.recipe:rewrite-kubernetes:2.0.1")
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
            <recipe>org.openrewrite.kubernetes.LifecycleRuleOnStorageBucket</recipe>
          </activeRecipes>
        </configuration>
        <dependencies>
          <dependency>
            <groupId>org.openrewrite.recipe</groupId>
            <artifactId>rewrite-kubernetes</artifactId>
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
  -Drewrite.recipeArtifactCoordinates=org.openrewrite.recipe:rewrite-kubernetes:RELEASE \
  -Drewrite.activeRecipes=org.openrewrite.kubernetes.LifecycleRuleOnStorageBucket
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Definition

{% tabs %}
{% tab title="Recipe List" %}
* [Add Kubernetes configuration](../kubernetes/addconfiguration.md)
  * apiVersion: `storage.cnrm.cloud.google.com/v1beta1`
  * resourceKind: `StorageBucket`
  * configurationPath: `$.spec`
  * value: `lifecycleRule:
  - action:
      type: Delete
    condition:
      age: 7`

{% endtab %}

{% tab title="Yaml Recipe List" %}
```yaml
---
type: specs.openrewrite.org/v1beta/recipe
name: org.openrewrite.kubernetes.LifecycleRuleOnStorageBucket
displayName: Ensure lifecycle rule on `StorageBucket`
description: When defining a rule, you can specify any set of conditions for any action. The following configuration defines a rule to delete all objects older than 7 days in a bucket.
tags:
  - kubernetes
recipeList:
  - org.openrewrite.kubernetes.AddConfiguration:
      apiVersion: storage.cnrm.cloud.google.com/v1beta1
      resourceKind: StorageBucket
      configurationPath: $.spec
      value: lifecycleRule:
  - action:
      type: Delete
    condition:
      age: 7

```
{% endtab %}
{% endtabs %}

## Contributors
* [Jonathan Schneider](jkschneider@gmail.com)
* [Tyler Van Gorder](1878529+tkvangorder@users.noreply.github.com)
* [Aaron Gershman](aegershman@gmail.com)
* [Knut Wannheden](knut.wannheden@gmail.com)
* [Jon Brisbin](jon@jbrisbin.com)


## See how this recipe works across multiple open-source repositories

[![Moderne Link Image](/.gitbook/assets/ModerneRecipeButton.png)](https://app.moderne.io/recipes/org.openrewrite.kubernetes.LifecycleRuleOnStorageBucket)

The community edition of the Moderne platform enables you to easily run recipes across thousands of open-source repositories.

Please [contact Moderne](https://moderne.io/product) for more information about safely running the recipes on your own codebase in a private SaaS.
