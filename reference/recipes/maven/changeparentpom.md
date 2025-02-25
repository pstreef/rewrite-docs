# Change Maven Parent Pom

**org.openrewrite.maven.ChangeParentPom**

_Change the parent pom of a Maven pom.xml. Identifies the parent pom to be changed by its groupId and artifactId._

## Source

[GitHub](https://github.com/openrewrite/rewrite/blob/main/rewrite-maven/src/main/java/org/openrewrite/maven/ChangeParentPom.java), [Issue Tracker](https://github.com/openrewrite/rewrite/issues), [Maven Central](https://central.sonatype.com/artifact/org.openrewrite/rewrite-maven/8.1.3/jar)

* groupId: org.openrewrite
* artifactId: rewrite-maven
* version: 8.1.3

## Options

| Type | Name | Description |
| -- | -- | -- |
| `String` | oldGroupId | The groupId of the maven parent pom to be changed away from. |
| `String` | newGroupId | *Optional*. The groupId of the new maven parent pom to be adopted. If this argument is omitted it defaults to the value of `oldGroupId`. |
| `String` | oldArtifactId | The artifactId of the maven parent pom to be changed away from. |
| `String` | newArtifactId | *Optional*. The artifactId of the new maven parent pom to be adopted. If this argument is omitted it defaults to the value of `oldArtifactId`. |
| `String` | newVersion | An exact version number or node-style semver selector used to select the version number. |
| `String` | versionPattern | *Optional*. Allows version selection to be extended beyond the original Node Semver semantics. So for example,Setting 'version' to "25-29" can be paired with a metadata pattern of "-jre" to select Guava 29.0-jre |
| `Boolean` | allowVersionDowngrades | *Optional*. If the new parent has the same group/artifact, this flag can be used to only upgrade the version if the target version is newer than the current. |
| `List` | retainVersions | *Optional*. Accepts a list of GAVs. For each GAV, if it is a project direct dependency, and it is removed from dependency management in the new parent pom, then it will be retained with an explicit version. The version can be omitted from the GAV to use the old value from dependency management |

## Data Tables (Only available on the [Moderne platform](https://app.moderne.io/))

### Maven metadata failures

_Attempts to resolve maven metadata that failed._

| Column Name | Description |
| ----------- | ----------- |

## Examples
##### Example 1

###### Parameters
| Parameter | Value |
| -- | -- |
|oldGroupId|`org.springframework.boot`|
|newGroupId|`com.fasterxml.jackson`|
|oldArtifactId|`spring-boot-starter-parent`|
|newArtifactId|`jackson-parent`|
|newVersion|`2.12`|
|versionPattern|`null`|
|allowVersionDowngrades|`false`|
|retainVersions|`null`|


{% tabs %}
{% tab title="pom.xml" %}

###### Before
{% code title="pom.xml" %}
```xml
<project>
  <modelVersion>4.0.0</modelVersion>

  <parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>1.5.12.RELEASE</version>
  </parent>

  <groupId>com.mycompany.app</groupId>
  <artifactId>my-app</artifactId>
  <version>1</version>
</project>
```
{% endcode %}

###### After
{% code title="pom.xml" %}
```xml
<project>
  <modelVersion>4.0.0</modelVersion>

  <parent>
    <groupId>com.fasterxml.jackson</groupId>
    <artifactId>jackson-parent</artifactId>
    <version>2.12</version>
  </parent>

  <groupId>com.mycompany.app</groupId>
  <artifactId>my-app</artifactId>
  <version>1</version>
</project>
```
{% endcode %}

{% endtab %}
{% tab title="Diff" %}
{% code %}
```diff
--- pom.xml
+++ pom.xml
@@ -5,3 +5,3 @@

  <parent>
-   <groupId>org.springframework.boot</groupId>
-   <artifactId>spring-boot-starter-parent</artifactId>
-   <version>1.5.12.RELEASE</version>
+   <groupId>com.fasterxml.jackson</groupId>
+   <artifactId>jackson-parent</artifactId>
+   <version>2.12</version>
  </parent>
```
{% endcode %}
{% endtab %}
{% endtabs %}

---

##### Example 2

###### Parameters
| Parameter | Value |
| -- | -- |
|oldGroupId|`org.springframework.cloud`|
|newGroupId|`null`|
|oldArtifactId|`spring-cloud-config-dependencies`|
|newArtifactId|`null`|
|newVersion|`3.1.4`|
|versionPattern|`null`|
|allowVersionDowngrades|`null`|
|retainVersions|`List.of("com.jcraft:jsch")`|


{% tabs %}
{% tab title="pom.xml" %}

###### Before
{% code title="pom.xml" %}
```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>org.sample</groupId>
  <artifactId>sample</artifactId>
  <version>1.0.0</version>

  <parent>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-config-dependencies</artifactId>
    <version>3.1.2</version>
  </parent>

  <dependencies>
    <dependency>
      <groupId>com.jcraft</groupId>
      <artifactId>jsch</artifactId>
      <version>0.1.55</version>
    </dependency>
  </dependencies>
</project>
```
{% endcode %}

###### After
{% code title="pom.xml" %}
```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>org.sample</groupId>
  <artifactId>sample</artifactId>
  <version>1.0.0</version>

  <parent>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-config-dependencies</artifactId>
    <version>3.1.4</version>
  </parent>

  <dependencies>
    <dependency>
      <groupId>com.jcraft</groupId>
      <artifactId>jsch</artifactId>
      <version>0.1.55</version>
    </dependency>
  </dependencies>
</project>
```
{% endcode %}

{% endtab %}
{% tab title="Diff" %}
{% code %}
```diff
--- pom.xml
+++ pom.xml
@@ -11,1 +11,1 @@
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-config-dependencies</artifactId>
-   <version>3.1.2</version>
+   <version>3.1.4</version>
  </parent>
```
{% endcode %}
{% endtab %}
{% endtabs %}


## Usage

This recipe has required configuration parameters. Recipes with required configuration parameters cannot be activated directly. To activate this recipe you must create a new recipe which fills in the required parameters. In your `rewrite.yml` create a new recipe with a unique name. For example: `com.yourorg.ChangeParentPomExample`.
Here's how you can define and customize such a recipe within your rewrite.yml:

{% code title="rewrite.yml" %}
```yaml
---
type: specs.openrewrite.org/v1beta/recipe
name: com.yourorg.ChangeParentPomExample
displayName: Change Maven Parent Pom example
recipeList:
  - org.openrewrite.maven.ChangeParentPom:
      oldGroupId: org.springframework.boot
      newGroupId: org.springframework.boot
      oldArtifactId: spring-boot-starter-parent
      newArtifactId: spring-boot-starter-parent
      newVersion: 29.X
      versionPattern: '-jre'
      allowVersionDowngrades: null
      retainVersions: com.jcraft:jsch
```
{% endcode %}

Now that `com.yourorg.ChangeParentPomExample` has been defined activate it in your build file:
{% tabs %}

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
            <recipe>com.yourorg.ChangeParentPomExample</recipe>
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
* [Jonathan Schneider](jkschneider@gmail.com)
* [Nick McKinney](mckinneynicholas@gmail.com)
* [Tyler Van Gorder](tkvangorder@users.noreply.github.com)
* [Knut Wannheden](knut@moderne.io)
* [Jonathan Leitschuh](jonathan.leitschuh@gmail.com)


## See how this recipe works across multiple open-source repositories

[![Moderne Link Image](/.gitbook/assets/ModerneRecipeButton.png)](https://app.moderne.io/recipes/org.openrewrite.maven.ChangeParentPom)

The community edition of the Moderne platform enables you to easily run recipes across thousands of open-source repositories.

Please [contact Moderne](https://moderne.io/product) for more information about safely running the recipes on your own codebase in a private SaaS.
