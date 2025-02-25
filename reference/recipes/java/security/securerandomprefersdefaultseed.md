# SecureRandom seeds are not constant or predictable

**org.openrewrite.java.security.SecureRandomPrefersDefaultSeed**

_Remove `SecureRandom#setSeed(*)` method invocations having constant or predictable arguments._

### Tags

* RSPEC-4347

## Source

[GitHub](https://github.com/openrewrite/rewrite-java-security/blob/main/src/main/java/org/openrewrite/java/security/SecureRandomPrefersDefaultSeed.java), [Issue Tracker](https://github.com/openrewrite/rewrite-java-security/issues), [Maven Central](https://central.sonatype.com/artifact/org.openrewrite.recipe/rewrite-java-security/2.0.1/jar)

* groupId: org.openrewrite.recipe
* artifactId: rewrite-java-security
* version: 2.0.1

## Example


{% tabs %}
{% tab title="A.java" %}

###### Before
{% code title="A.java" %}
```java
import java.security.SecureRandom;

public class A {
    void test(byte[] bytes) {
        SecureRandom r = new SecureRandom();
        r.setSeed(System.currentTimeMillis());
        r.setSeed(System.nanoTime());
    }
}
```
{% endcode %}

###### After
{% code title="A.java" %}
```java
import java.security.SecureRandom;

public class A {
    void test(byte[] bytes) {
        SecureRandom r = new SecureRandom();
    }
}
```
{% endcode %}

{% endtab %}
{% tab title="Diff" %}
{% code %}
```diff
--- A.java
+++ A.java
@@ -6,2 +6,0 @@
    void test(byte[] bytes) {
        SecureRandom r = new SecureRandom();
-       r.setSeed(System.currentTimeMillis());
-       r.setSeed(System.nanoTime());
    }
```
{% endcode %}
{% endtab %}
{% endtabs %}


## Usage

This recipe has no required configuration options. It can be activated by adding a dependency on `org.openrewrite.recipe:rewrite-java-security:2.0.1` in your build file or by running a shell command (in which case no build changes are needed): 
{% tabs %}
{% tab title="Gradle" %}
{% code title="build.gradle" %}
```groovy
plugins {
    id("org.openrewrite.rewrite") version("6.1.4")
}

rewrite {
    activeRecipe("org.openrewrite.java.security.SecureRandomPrefersDefaultSeed")
}

repositories {
    mavenCentral()
}

dependencies {
    rewrite("org.openrewrite.recipe:rewrite-java-security:2.0.1")
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
            <recipe>org.openrewrite.java.security.SecureRandomPrefersDefaultSeed</recipe>
          </activeRecipes>
        </configuration>
        <dependencies>
          <dependency>
            <groupId>org.openrewrite.recipe</groupId>
            <artifactId>rewrite-java-security</artifactId>
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
  -Drewrite.recipeArtifactCoordinates=org.openrewrite.recipe:rewrite-java-security:RELEASE \
  -Drewrite.activeRecipes=org.openrewrite.java.security.SecureRandomPrefersDefaultSeed
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Contributors
* [Patrick](patway99@gmail.com)
* [Knut Wannheden](knut@moderne.io)
* [Sam Snyder](sam@moderne.io)
* [Jonathan Schnéider](jkschneider@gmail.com)


## See how this recipe works across multiple open-source repositories

[![Moderne Link Image](/.gitbook/assets/ModerneRecipeButton.png)](https://app.moderne.io/recipes/org.openrewrite.java.security.SecureRandomPrefersDefaultSeed)

The community edition of the Moderne platform enables you to easily run recipes across thousands of open-source repositories.

Please [contact Moderne](https://moderne.io/product) for more information about safely running the recipes on your own codebase in a private SaaS.
