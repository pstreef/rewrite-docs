# Add Gradle Enterprise Maven Extension to maven projects

**org.openrewrite.maven.AddGradleEnterpriseMavenExtension**

_To integrate gradle enterprise maven extension into maven projects, ensure that the `gradle-enterprise-maven-extension` is added to the `.mvn/extensions.xml` file if not already present. Additionally, configure the extension by adding the `.mvn/gradle-enterprise.xml` configuration file._

## Source

[GitHub](https://github.com/openrewrite/rewrite/blob/main/rewrite-maven/src/main/java/org/openrewrite/maven/AddGradleEnterpriseMavenExtension.java), [Issue Tracker](https://github.com/openrewrite/rewrite/issues), [Maven Central](https://central.sonatype.com/artifact/org.openrewrite/rewrite-maven/8.1.3/jar)

* groupId: org.openrewrite
* artifactId: rewrite-maven
* version: 8.1.3

## Options

| Type | Name | Description |
| -- | -- | -- |
| `String` | version | An exact version number or node-style semver selector used to select the gradle-enterprise-maven-extension version. |
| `String` | server | The URL of the Gradle Enterprise server. |
| `Boolean` | allowUntrustedServer | *Optional*. When set to `true` the plugin will be configured to allow unencrypted http connections with the server. If set to `false` or omitted, the plugin will refuse to communicate without transport layer security enabled. |
| `Boolean` | captureGoalInputFiles | *Optional*. When set to `true` the extension will capture additional information about the inputs to Maven goals. This increases the size of build scans, but is useful for diagnosing issues with goal caching.  |
| `Boolean` | uploadInBackground | *Optional*. When set to `false` the extension will not upload build scan in the background. By default, build scans are uploaded in the background after the build has finished to avoid blocking the build process. |
| `PublishCriteria` | publishCriteria | *Optional*. When set to `always` the extension will publish build scans of every single build. This is the default behavior when omitted.When set to `failure` the extension will only publish build scans when the build fails. When set to `demand` the extension will only publish build scans when explicitly requested. |


## Example

###### Parameters
| Parameter | Value |
| -- | -- |
|version|`1.17`|
|server|`https://foo`|
|allowUntrustedServer|`null`|
|captureGoalInputFiles|`null`|
|uploadInBackground|`null`|
|publishCriteria|`null`|


###### Unchanged
{% code title="pom.xml" %}
```xml
<project>
    <groupId>com.mycompany.app</groupId>
    <artifactId>my-app</artifactId>
    <version>1</version>
</project>
```
{% endcode %}

{% tabs %}
{% tab title=".mvn/extensions.xml" %}

###### Before
{% code title=".mvn/extensions.xml" %}
```xml
<?xml version="1.0" encoding="UTF-8"?>
<extensions>
</extensions>
```
{% endcode %}

###### After
{% code title=".mvn/extensions.xml" %}
```xml
<?xml version="1.0" encoding="UTF-8"?>
<extensions>
  <extension>
    <groupId>com.gradle</groupId>
    <artifactId>gradle-enterprise-maven-extension</artifactId>
    <version>1.17</version>
  </extension>
</extensions>
```
{% endcode %}

{% endtab %}
{% tab title="Diff" %}
{% code %}
```diff
--- .mvn/extensions.xml
+++ .mvn/extensions.xml
@@ -3,0 +3,5 @@
<?xml version="1.0" encoding="UTF-8"?>
<extensions>
+ <extension>
+   <groupId>com.gradle</groupId>
+   <artifactId>gradle-enterprise-maven-extension</artifactId>
+   <version>1.17</version>
+ </extension>
</extensions>
```
{% endcode %}
{% endtab %}
{% endtabs %}


###### New file
{% code title=".mvn/gradle-enterprise.xml" %}
```xml
<gradleEnterprise>
  <server>
    <url>https://foo</url>
  </server>
</gradleEnterprise>
```
{% endcode %}



## Usage

This recipe has required configuration parameters. Recipes with required configuration parameters cannot be activated directly. To activate this recipe you must create a new recipe which fills in the required parameters. In your `rewrite.yml` create a new recipe with a unique name. For example: `com.yourorg.AddGradleEnterpriseMavenExtensionExample`.
Here's how you can define and customize such a recipe within your rewrite.yml:

{% code title="rewrite.yml" %}
```yaml
---
type: specs.openrewrite.org/v1beta/recipe
name: com.yourorg.AddGradleEnterpriseMavenExtensionExample
displayName: Add Gradle Enterprise Maven Extension to maven projects example
recipeList:
  - org.openrewrite.maven.AddGradleEnterpriseMavenExtension:
      version: 1.x
      server: https://scans.gradle.com/
      allowUntrustedServer: true
      captureGoalInputFiles: true
      uploadInBackground: false
      publishCriteria: true
```
{% endcode %}

Now that `com.yourorg.AddGradleEnterpriseMavenExtensionExample` has been defined activate it in your build file:
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
            <recipe>com.yourorg.AddGradleEnterpriseMavenExtensionExample</recipe>
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

## See how this recipe works across multiple open-source repositories

[![Moderne Link Image](/.gitbook/assets/ModerneRecipeButton.png)](https://app.moderne.io/recipes/org.openrewrite.maven.AddGradleEnterpriseMavenExtension)

The community edition of the Moderne platform enables you to easily run recipes across thousands of open-source repositories.

Please [contact Moderne](https://moderne.io/product) for more information about safely running the recipes on your own codebase in a private SaaS.
