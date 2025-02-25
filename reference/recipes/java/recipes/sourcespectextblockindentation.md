# Minimal indentation for `SourceSpecs` text blocks

**org.openrewrite.java.recipes.SourceSpecTextBlockIndentation**

_Text blocks that assert before and after source code should have minimal indentation._

## Source

[GitHub](https://github.com/openrewrite/rewrite/blob/main/rewrite-java/src/main/java/org/openrewrite/java/recipes/SourceSpecTextBlockIndentation.java), [Issue Tracker](https://github.com/openrewrite/rewrite/issues), [Maven Central](https://central.sonatype.com/artifact/org.openrewrite/rewrite-java/8.1.3/jar)

* groupId: org.openrewrite
* artifactId: rewrite-java
* version: 8.1.3

## Example


{% tabs %}
{% tab title="MyRecipeTest.java" %}

###### Before
{% code title="MyRecipeTest.java" %}
```java
import org.openrewrite.test.RewriteTest;
import static org.openrewrite.test.SourceSpecs.text;

class MyRecipeTest implements RewriteTest {
    void test() {
      rewriteRun(
         text(
           """
               class Test {
 
                   
                   void test() {
                       System.out.println("Hello, world!");
                   }
               }
             """
         )
      );
    }
}
```
{% endcode %}

###### After
{% code title="MyRecipeTest.java" %}
```java
import org.openrewrite.test.RewriteTest;
import static org.openrewrite.test.SourceSpecs.text;

class MyRecipeTest implements RewriteTest {
    void test() {
      rewriteRun(
         text(
           """
             class Test {
 
                 
                 void test() {
                     System.out.println("Hello, world!");
                 }
             }
             """
         )
      );
    }
}
```
{% endcode %}

{% endtab %}
{% tab title="Diff" %}
{% code %}
```diff
--- MyRecipeTest.java
+++ MyRecipeTest.java
@@ -9,1 +9,1 @@
         text(
           """
-              class Test {
+            class Test {
 
@@ -11,5 +11,5 @@
               class Test {
 
-                  
-                  void test() {
-                      System.out.println("Hello, world!");
-                  }
-              }
+                
+                void test() {
+                    System.out.println("Hello, world!");
+                }
+            }
             """
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
    activeRecipe("org.openrewrite.java.recipes.SourceSpecTextBlockIndentation")
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
            <recipe>org.openrewrite.java.recipes.SourceSpecTextBlockIndentation</recipe>
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
  -Drewrite.activeRecipes=org.openrewrite.java.recipes.SourceSpecTextBlockIndentation
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Contributors
* [Jonathan Schneider](jkschneider@gmail.com)


## See how this recipe works across multiple open-source repositories

[![Moderne Link Image](/.gitbook/assets/ModerneRecipeButton.png)](https://app.moderne.io/recipes/org.openrewrite.java.recipes.SourceSpecTextBlockIndentation)

The community edition of the Moderne platform enables you to easily run recipes across thousands of open-source repositories.

Please [contact Moderne](https://moderne.io/product) for more information about safely running the recipes on your own codebase in a private SaaS.
