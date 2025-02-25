# Spaces

**org.openrewrite.hcl.format.Spaces**

_Format whitespace in HCL code._

## Source

[GitHub](https://github.com/openrewrite/rewrite/blob/main/rewrite-hcl/src/main/java/org/openrewrite/hcl/format/Spaces.java), [Issue Tracker](https://github.com/openrewrite/rewrite/issues), [Maven Central](https://central.sonatype.com/artifact/org.openrewrite/rewrite-hcl/8.1.3/jar)

* groupId: org.openrewrite
* artifactId: rewrite-hcl
* version: 8.1.3

## Example


{% tabs %}
{% tab title="hcl" %}

###### Before
{% code %}
```hcl
resource "aws_ebs_volume" {
  size =1
  encrypted =true
}
```
{% endcode %}

###### After
{% code %}
```hcl
resource "aws_ebs_volume" {
  size      = 1
  encrypted = true
}
```
{% endcode %}

{% endtab %}
{% tab title="Diff" %}
{% code %}
```diff
@@ -2,2 +2,2 @@
resource "aws_ebs_volume" {
- size =1
- encrypted =true
+ size      = 1
+ encrypted = true
}
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
    activeRecipe("org.openrewrite.hcl.format.Spaces")
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
            <recipe>org.openrewrite.hcl.format.Spaces</recipe>
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
  -Drewrite.activeRecipes=org.openrewrite.hcl.format.Spaces
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Contributors
* [Jonathan Schneider](jkschneider@gmail.com)


## See how this recipe works across multiple open-source repositories

[![Moderne Link Image](/.gitbook/assets/ModerneRecipeButton.png)](https://app.moderne.io/recipes/org.openrewrite.hcl.format.Spaces)

The community edition of the Moderne platform enables you to easily run recipes across thousands of open-source repositories.

Please [contact Moderne](https://moderne.io/product) for more information about safely running the recipes on your own codebase in a private SaaS.
