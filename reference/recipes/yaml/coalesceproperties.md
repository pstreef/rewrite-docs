# Coalesce YAML properties

**org.openrewrite.yaml.CoalesceProperties**

_Simplify nested map hierarchies into their simplest dot separated property form, i.e. as Spring Boot interprets application.yml files._

## Source

[GitHub](https://github.com/openrewrite/rewrite/blob/main/rewrite-yaml/src/main/java/org/openrewrite/yaml/CoalesceProperties.java), [Issue Tracker](https://github.com/openrewrite/rewrite/issues), [Maven Central](https://central.sonatype.com/artifact/org.openrewrite/rewrite-yaml/8.1.3/jar)

* groupId: org.openrewrite
* artifactId: rewrite-yaml
* version: 8.1.3

## Example


{% tabs %}
{% tab title="yaml" %}

###### Before
{% code %}
```yaml
    management:
        metrics:
            enable.process.files: true
        endpoint:
            health:
                show-components: always
                show-details: always
```
{% endcode %}

###### After
{% code %}
```yaml
    management:
        metrics.enable.process.files: true
        endpoint.health:
            show-components: always
            show-details: always
```
{% endcode %}

{% endtab %}
{% tab title="Diff" %}
{% code %}
```diff
@@ -2,6 +2,4 @@
    management:
-       metrics:
-           enable.process.files: true
-       endpoint:
-           health:
-               show-components: always
-               show-details: always
+       metrics.enable.process.files: true
+       endpoint.health:
+           show-components: always
+           show-details: always

```
{% endcode %}
{% endtab %}
{% endtabs %}


## Usage

This recipe has no required configuration parameters and comes from a rewrite core library. It can be activated directly without adding any dependencies.
{% tabs %}
{% tab title="Gradle" %}
{% code title="build.gradle" %}
```groovy
plugins {
    id("org.openrewrite.rewrite") version("6.1.4")
}

rewrite {
    activeRecipe("org.openrewrite.yaml.CoalesceProperties")
}

repositories {
    mavenCentral()
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
            <recipe>org.openrewrite.yaml.CoalesceProperties</recipe>
          </activeRecipes>
        </configuration>
      </plugin>
    </plugins>
  </build>
</project>
```
{% endcode %}
{% endtab %}

{% tab title="Maven Command Line" %}
You will need to have [Maven](https://maven.apache.org/download.cgi) installed on your machine before you can run the following command.
{% code title="shell" %}
```shell
mvn -U org.openrewrite.maven:rewrite-maven-plugin:run \
  -Drewrite.activeRecipes=org.openrewrite.yaml.CoalesceProperties
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Contributors
* [Jonathan Leitschuh](jonathan.leitschuh@gmail.com)
* [Sam Snyder](sam@moderne.io)


## See how this recipe works across multiple open-source repositories

[![Moderne Link Image](/.gitbook/assets/ModerneRecipeButton.png)](https://app.moderne.io/recipes/org.openrewrite.yaml.CoalesceProperties)

The community edition of the Moderne platform enables you to easily run recipes across thousands of open-source repositories.

Please [contact Moderne](https://moderne.io/product) for more information about safely running the recipes on your own codebase in a private SaaS.
