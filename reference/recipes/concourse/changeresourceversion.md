# Change resource version

**org.openrewrite.concourse.ChangeResourceVersion**

_Pin or unpin a resource to a particular version._

## Source

[GitHub](https://github.com/openrewrite/rewrite-concourse/blob/main/src/main/java/org/openrewrite/concourse/ChangeResourceVersion.java), [Issue Tracker](https://github.com/openrewrite/rewrite-concourse/issues), [Maven Central](https://central.sonatype.com/artifact/org.openrewrite.recipe/rewrite-concourse/2.0.1/jar)

* groupId: org.openrewrite.recipe
* artifactId: rewrite-concourse
* version: 2.0.1

## Options

| Type | Name | Description |
| -- | -- | -- |
| `String` | resourceType | Update any resources of this type |
| `String` | version | *Optional*. If less than this version, update. If not provided, clears pins. |

## Example

###### Parameters
| Parameter | Value |
| -- | -- |
|resourceType|`git`|
|version|`2.0`|


{% tabs %}
{% tab title="yaml" %}

###### Before
{% code %}
```yaml
resources:
  - name: git-repo
    type: git
    version: 1.0
  - name: git-repo2
    type: git
    version: 2.0
  - name: git-repo3
    type: git
```
{% endcode %}

###### After
{% code %}
```yaml
resources:
  - name: git-repo
    type: git
    version: 2.0
  - name: git-repo2
    type: git
    version: 2.0
  - name: git-repo3
    type: git
    version: 2.0
```
{% endcode %}

{% endtab %}
{% tab title="Diff" %}
{% code %}
```diff
@@ -4,1 +4,1 @@
  - name: git-repo
    type: git
-   version: 1.0
+   version: 2.0
  - name: git-repo2
@@ -10,0 +10,1 @@
  - name: git-repo3
    type: git
+   version: 2.0

```
{% endcode %}
{% endtab %}
{% endtabs %}


## Usage

This recipe has required configuration parameters. Recipes with required configuration parameters cannot be activated directly. To activate this recipe you must create a new recipe which fills in the required parameters. In your `rewrite.yml` create a new recipe with a unique name. For example: `com.yourorg.ChangeResourceVersionExample`.
Here's how you can define and customize such a recipe within your rewrite.yml:

{% code title="rewrite.yml" %}
```yaml
---
type: specs.openrewrite.org/v1beta/recipe
name: com.yourorg.ChangeResourceVersionExample
displayName: Change resource version example
recipeList:
  - org.openrewrite.concourse.ChangeResourceVersion:
      resourceType: git
      version: 2.0
```
{% endcode %}

Now that `com.yourorg.ChangeResourceVersionExample` has been defined activate it and take a dependency on org.openrewrite.recipe:rewrite-concourse:2.0.1 in your build file:
{% tabs %}
{% tab title="Gradle" %}
{% code title="build.gradle" %}
```groovy
plugins {
    id("org.openrewrite.rewrite") version("6.1.4")
}

rewrite {
    activeRecipe("com.yourorg.ChangeResourceVersionExample")
}

repositories {
    mavenCentral()
}

dependencies {
    rewrite("org.openrewrite.recipe:rewrite-concourse:2.0.1")
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
            <recipe>com.yourorg.ChangeResourceVersionExample</recipe>
          </activeRecipes>
        </configuration>
        <dependencies>
          <dependency>
            <groupId>org.openrewrite.recipe</groupId>
            <artifactId>rewrite-concourse</artifactId>
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
{% endtabs %}

## Contributors
* [Jonathan Schneider](jkschneider@gmail.com)
* [Knut Wannheden](knut@moderne.io)
* [Kun Li](122563761+kunli2@users.noreply.github.com)
* [traceyyoshima](tracey.yoshima@gmail.com)
* [Aaron Gershman](aegershman@gmail.com)


## See how this recipe works across multiple open-source repositories

[![Moderne Link Image](/.gitbook/assets/ModerneRecipeButton.png)](https://app.moderne.io/recipes/org.openrewrite.concourse.ChangeResourceVersion)

The community edition of the Moderne platform enables you to easily run recipes across thousands of open-source repositories.

Please [contact Moderne](https://moderne.io/product) for more information about safely running the recipes on your own codebase in a private SaaS.
