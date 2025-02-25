# Remove applicability test from Yaml recipe

**org.openrewrite.java.recipes.RemoveApplicabilityTestFromYamlRecipe**

_Remove the applicability test from the YAML recipe when migrating from Rewrite 7 to 8, as it is no longer supported and may require migrating the recipe to Java code._

### Tags

* Rewrite8 migration

## Source

[GitHub](https://github.com/openrewrite/rewrite/blob/main/rewrite-java/src/main/java/org/openrewrite/java/recipes/RemoveApplicabilityTestFromYamlRecipe.java), [Issue Tracker](https://github.com/openrewrite/rewrite/issues), [Maven Central](https://central.sonatype.com/artifact/org.openrewrite/rewrite-java/8.1.3/jar)

* groupId: org.openrewrite
* artifactId: rewrite-java
* version: 8.1.3

## Example


{% tabs %}
{% tab title="yaml" %}

###### Before
{% code %}
```yaml
type: specs.openrewrite.org/v1beta/recipe
name: org.openrewrite.java.testing.mockito.AnyToNullable
displayName: x
description: x.
tags:
  - testing
applicability:
  anySource:
    - org.openrewrite.java.testing.mockito.UsesMockitoAll
recipeList:
  - org.openrewrite.java.Recipe1
  - org.openrewrite.java.Recipe2
```
{% endcode %}

###### After
{% code %}
```yaml
type: specs.openrewrite.org/v1beta/recipe
name: org.openrewrite.java.testing.mockito.AnyToNullable
displayName: x
description: x.
tags:
  - testing
# Applicability tests are no longer supported for yaml recipes, please remove or require migrating the recipe to Java code
# applicability:
#   anySource:
#     - org.openrewrite.java.testing.mockito.UsesMockitoAll
recipeList:
  - org.openrewrite.java.Recipe1
  - org.openrewrite.java.Recipe2
```
{% endcode %}

{% endtab %}
{% tab title="Diff" %}
{% code %}
```diff
@@ -7,3 +7,4 @@
tags:
  - testing
-applicability:
- anySource:
-   - org.openrewrite.java.testing.mockito.UsesMockitoAll
+# Applicability tests are no longer supported for yaml recipes, please remove or require migrating the recipe to Java code
+# applicability:
+#   anySource:
+#     - org.openrewrite.java.testing.mockito.UsesMockitoAll
recipeList:
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
    activeRecipe("org.openrewrite.java.recipes.RemoveApplicabilityTestFromYamlRecipe")
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
            <recipe>org.openrewrite.java.recipes.RemoveApplicabilityTestFromYamlRecipe</recipe>
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
  -Drewrite.activeRecipes=org.openrewrite.java.recipes.RemoveApplicabilityTestFromYamlRecipe
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Contributors
* [Kun Li](kun@moderne.io)


## See how this recipe works across multiple open-source repositories

[![Moderne Link Image](/.gitbook/assets/ModerneRecipeButton.png)](https://app.moderne.io/recipes/org.openrewrite.java.recipes.RemoveApplicabilityTestFromYamlRecipe)

The community edition of the Moderne platform enables you to easily run recipes across thousands of open-source repositories.

Please [contact Moderne](https://moderne.io/product) for more information about safely running the recipes on your own codebase in a private SaaS.
