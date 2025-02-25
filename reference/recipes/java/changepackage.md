# Rename package name

**org.openrewrite.java.ChangePackage**

_A recipe that will rename a package name in package statements, imports, and fully-qualified types._

## Source

[GitHub](https://github.com/openrewrite/rewrite/blob/main/rewrite-java/src/main/java/org/openrewrite/java/ChangePackage.java), [Issue Tracker](https://github.com/openrewrite/rewrite/issues), [Maven Central](https://central.sonatype.com/artifact/org.openrewrite/rewrite-java/8.1.3/jar)

* groupId: org.openrewrite
* artifactId: rewrite-java
* version: 8.1.3

## Options

| Type | Name | Description |
| -- | -- | -- |
| `String` | oldPackageName | The package name to replace. |
| `String` | newPackageName | New package name to replace the old package name with. |
| `Boolean` | recursive | *Optional*. Recursively change subpackage names |

## Examples
##### Example 1

###### Parameters
| Parameter | Value |
| -- | -- |
|oldPackageName|`a.b`|
|newPackageName|`x.y`|
|recursive|`false`|


{% tabs %}
{% tab title="kotlin" %}

###### Before
{% code %}
```kotlin
package a.b
class Original
```
{% endcode %}

###### After
{% code %}
```kotlin
package x.y
class Original
```
{% endcode %}

{% endtab %}
{% tab title="Diff" %}
{% code %}
```diff
@@ -1,1 +1,1 @@
-package a.b
+package x.y
class Original
```
{% endcode %}
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="kotlin" %}

###### Before
{% code %}
```kotlin
import a.b.Original

class A {
    val type = Original()
}
```
{% endcode %}

###### After
{% code %}
```kotlin
import x.y.Original

class A {
    val type = Original()
}
```
{% endcode %}

{% endtab %}
{% tab title="Diff" %}
{% code %}
```diff
@@ -1,1 +1,1 @@
-import a.b.Original
+import x.y.Original

```
{% endcode %}
{% endtab %}
{% endtabs %}

---

##### Example 2

###### Parameters
| Parameter | Value |
| -- | -- |
|oldPackageName|`a.b`|
|newPackageName|`x.y`|
|recursive|`false`|


{% tabs %}
{% tab title="groovy" %}

###### Before
{% code %}
```groovy
package a.b
class Original {}
```
{% endcode %}

###### After
{% code %}
```groovy
package x.y
class Original {}
```
{% endcode %}

{% endtab %}
{% tab title="Diff" %}
{% code %}
```diff
@@ -1,1 +1,1 @@
-package a.b
+package x.y
class Original {}
```
{% endcode %}
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="groovy" %}

###### Before
{% code %}
```groovy
import a.b.Original

class A {
    Original type
}
```
{% endcode %}

###### After
{% code %}
```groovy
import x.y.Original

class A {
    Original type
}
```
{% endcode %}

{% endtab %}
{% tab title="Diff" %}
{% code %}
```diff
@@ -1,1 +1,1 @@
-import a.b.Original
+import x.y.Original

```
{% endcode %}
{% endtab %}
{% endtabs %}

---

##### Example 3

###### Parameters
| Parameter | Value |
| -- | -- |
|oldPackageName|`org.openrewrite`|
|newPackageName|`openrewrite`|
|recursive|`false`|


{% tabs %}
{% tab title="Test.java" %}

###### Before
{% code title="Test.java" %}
```java
import org.openrewrite.Foo;
class Test {
}
```
{% endcode %}

###### After
{% code title="Test.java" %}
```java
import openrewrite.Foo;
class Test {
}
```
{% endcode %}

{% endtab %}
{% tab title="Diff" %}
{% code %}
```diff
--- Test.java
+++ Test.java
@@ -1,1 +1,1 @@
-import org.openrewrite.Foo;
+import openrewrite.Foo;
class Test {
```
{% endcode %}
{% endtab %}
{% endtabs %}


## Usage

This recipe has required configuration parameters. Recipes with required configuration parameters cannot be activated directly. To activate this recipe you must create a new recipe which fills in the required parameters. In your `rewrite.yml` create a new recipe with a unique name. For example: `com.yourorg.ChangePackageExample`.
Here's how you can define and customize such a recipe within your rewrite.yml:

{% code title="rewrite.yml" %}
```yaml
---
type: specs.openrewrite.org/v1beta/recipe
name: com.yourorg.ChangePackageExample
displayName: Rename package name example
recipeList:
  - org.openrewrite.java.ChangePackage:
      oldPackageName: com.yourorg.foo
      newPackageName: com.yourorg.bar
      recursive: null
```
{% endcode %}

Now that `com.yourorg.ChangePackageExample` has been defined activate it in your build file:
{% tabs %}
{% tab title="Gradle" %}
{% code title="build.gradle" %}
```groovy
plugins {
    id("org.openrewrite.rewrite") version("6.1.4")
}

rewrite {
    activeRecipe("com.yourorg.ChangePackageExample")
}

repositories {
    mavenCentral()
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
            <recipe>com.yourorg.ChangePackageExample</recipe>
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
* [Tracey Yoshima](tracey.yoshima@gmail.com)
* [Jonathan Schnéider](jkschneider@gmail.com)
* [Knut Wannheden](knut@moderne.io)
* [Patrick](patway99@gmail.com)
* [Sam Snyder](sam@moderne.io)
* [Patrick Way](pway99@users.noreply.github.com)
* [Roberto Cortez](radcortez@yahoo.com)


## See how this recipe works across multiple open-source repositories

[![Moderne Link Image](/.gitbook/assets/ModerneRecipeButton.png)](https://app.moderne.io/recipes/org.openrewrite.java.ChangePackage)

The community edition of the Moderne platform enables you to easily run recipes across thousands of open-source repositories.

Please [contact Moderne](https://moderne.io/product) for more information about safely running the recipes on your own codebase in a private SaaS.
