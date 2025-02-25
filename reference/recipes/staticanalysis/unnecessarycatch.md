# Remove catch for a checked exception if the try block does not throw that exception

**org.openrewrite.staticanalysis.UnnecessaryCatch**

_A refactoring operation may result in a checked exception that is no longer thrown from a `try` block. This recipe will find and remove unnecessary catch blocks._

## Source

[GitHub](https://github.com/openrewrite/rewrite-static-analysis/blob/main/src/main/java/org/openrewrite/staticanalysis/UnnecessaryCatch.java), [Issue Tracker](https://github.com/openrewrite/rewrite-static-analysis/issues), [Maven Central](https://central.sonatype.com/artifact/org.openrewrite.recipe/rewrite-static-analysis/1.0.1/jar)

* groupId: org.openrewrite.recipe
* artifactId: rewrite-static-analysis
* version: 1.0.1

## Options

| Type | Name | Description |
| -- | -- | -- |
| `boolean` | includeJavaLangException | *Optional*. Whether to include java.lang.Exception in the list of checked exceptions to remove. Unlike other checked exceptions, `java.lang.Exception` is also the superclass of unchecked exceptions. So removing `catch(Exception e)` may result in changed runtime behavior in the presence of unchecked exceptions. Default `false` |

## Example

###### Parameters
| Parameter | Value |
| -- | -- |
|includeJavaLangException|`false`|


{% tabs %}
{% tab title="AnExample.java" %}

###### Before
{% code title="AnExample.java" %}
```java
import java.io.IOException;

public class AnExample {
    public void method() {
        try {
            java.util.Base64.getDecoder().decode("abc".getBytes());
        } catch (IOException e) {
            System.out.println("an exception!");
        }
    }
}
```
{% endcode %}

###### After
{% code title="AnExample.java" %}
```java
public class AnExample {
    public void method() {
        java.util.Base64.getDecoder().decode("abc".getBytes());
    }
}
```
{% endcode %}

{% endtab %}
{% tab title="Diff" %}
{% code %}
```diff
--- AnExample.java
+++ AnExample.java
@@ -1,2 +1,0 @@
-import java.io.IOException;
-
public class AnExample {
@@ -5,5 +3,1 @@
public class AnExample {
    public void method() {
-       try {
-           java.util.Base64.getDecoder().decode("abc".getBytes());
-       } catch (IOException e) {
-           System.out.println("an exception!");
-       }
+       java.util.Base64.getDecoder().decode("abc".getBytes());
    }
```
{% endcode %}
{% endtab %}
{% endtabs %}


## Usage

This recipe has no required configuration options. It can be activated by adding a dependency on `org.openrewrite.recipe:rewrite-static-analysis:1.0.1` in your build file or by running a shell command (in which case no build changes are needed): 
{% tabs %}
{% tab title="Gradle" %}
{% code title="build.gradle" %}
```groovy
plugins {
    id("org.openrewrite.rewrite") version("6.1.4")
}

rewrite {
    activeRecipe("org.openrewrite.staticanalysis.UnnecessaryCatch")
}

repositories {
    mavenCentral()
}

dependencies {
    rewrite("org.openrewrite.recipe:rewrite-static-analysis:1.0.1")
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
            <recipe>org.openrewrite.staticanalysis.UnnecessaryCatch</recipe>
          </activeRecipes>
        </configuration>
        <dependencies>
          <dependency>
            <groupId>org.openrewrite.recipe</groupId>
            <artifactId>rewrite-static-analysis</artifactId>
            <version>1.0.1</version>
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
  -Drewrite.recipeArtifactCoordinates=org.openrewrite.recipe:rewrite-static-analysis:RELEASE \
  -Drewrite.activeRecipes=org.openrewrite.staticanalysis.UnnecessaryCatch
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Contributors
* [Tyler Van Gorder](1878529+tkvangorder@users.noreply.github.com)
* [Sam Snyder](sam@moderne.io)
* [Knut Wannheden](knut@moderne.io)


## See how this recipe works across multiple open-source repositories

[![Moderne Link Image](/.gitbook/assets/ModerneRecipeButton.png)](https://app.moderne.io/recipes/org.openrewrite.staticanalysis.UnnecessaryCatch)

The community edition of the Moderne platform enables you to easily run recipes across thousands of open-source repositories.

Please [contact Moderne](https://moderne.io/product) for more information about safely running the recipes on your own codebase in a private SaaS.
