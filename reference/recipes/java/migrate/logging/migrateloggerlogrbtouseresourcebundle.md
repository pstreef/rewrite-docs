# Use `Logger#logrb(.., ResourceBundle bundleName, ..)`

**org.openrewrite.java.migrate.logging.MigrateLoggerLogrbToUseResourceBundle**

_Use `Logger#logrb(.., ResourceBundle bundleName, ..)` instead of the deprecated `java.util.logging.Logger#logrb(.., String bundleName, ..)` in Java 8 or higher._

### Tags

* deprecated

## Source

[GitHub](https://github.com/openrewrite/rewrite-migrate-java/blob/main/src/main/java/org/openrewrite/java/migrate/logging/MigrateLoggerLogrbToUseResourceBundle.java), [Issue Tracker](https://github.com/openrewrite/rewrite-migrate-java/issues), [Maven Central](https://central.sonatype.com/artifact/org.openrewrite.recipe/rewrite-migrate-java/2.0.1/jar)

* groupId: org.openrewrite.recipe
* artifactId: rewrite-migrate-java
* version: 2.0.1

## Example


{% tabs %}
{% tab title="org/openrewrite/example/Test.java" %}

###### Before
{% code title="org/openrewrite/example/Test.java" %}
```java
package org.openrewrite.example;

import java.util.logging.Level;
import java.util.logging.Logger;

public class Test {
    Logger logger = Logger.getLogger("myLogger");

    public void method() {
        logger.logrb(Level.parse("0"), "sourceClass", "sourceMethod", "bundleName", "msg");
    }
}
```
{% endcode %}

###### After
{% code title="org/openrewrite/example/Test.java" %}
```java
package org.openrewrite.example;

import java.util.ResourceBundle;
import java.util.logging.Level;
import java.util.logging.Logger;

public class Test {
    Logger logger = Logger.getLogger("myLogger");

    public void method() {
        logger.logrb(Level.parse("0"), "sourceClass", "sourceMethod", ResourceBundle.getBundle("bundleName"), "msg");
    }
}
```
{% endcode %}

{% endtab %}
{% tab title="Diff" %}
{% code %}
```diff
--- org/openrewrite/example/Test.java
+++ org/openrewrite/example/Test.java
@@ -3,0 +3,1 @@
package org.openrewrite.example;

+import java.util.ResourceBundle;
import java.util.logging.Level;
@@ -10,1 +11,1 @@

    public void method() {
-       logger.logrb(Level.parse("0"), "sourceClass", "sourceMethod", "bundleName", "msg");
+       logger.logrb(Level.parse("0"), "sourceClass", "sourceMethod", ResourceBundle.getBundle("bundleName"), "msg");
    }
```
{% endcode %}
{% endtab %}
{% endtabs %}


## Usage

This recipe has no required configuration options. It can be activated by adding a dependency on `org.openrewrite.recipe:rewrite-migrate-java:2.0.1` in your build file or by running a shell command (in which case no build changes are needed): 
{% tabs %}
{% tab title="Gradle" %}
{% code title="build.gradle" %}
```groovy
plugins {
    id("org.openrewrite.rewrite") version("6.1.4")
}

rewrite {
    activeRecipe("org.openrewrite.java.migrate.logging.MigrateLoggerLogrbToUseResourceBundle")
}

repositories {
    mavenCentral()
}

dependencies {
    rewrite("org.openrewrite.recipe:rewrite-migrate-java:2.0.1")
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
            <recipe>org.openrewrite.java.migrate.logging.MigrateLoggerLogrbToUseResourceBundle</recipe>
          </activeRecipes>
        </configuration>
        <dependencies>
          <dependency>
            <groupId>org.openrewrite.recipe</groupId>
            <artifactId>rewrite-migrate-java</artifactId>
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
  -Drewrite.recipeArtifactCoordinates=org.openrewrite.recipe:rewrite-migrate-java:RELEASE \
  -Drewrite.activeRecipes=org.openrewrite.java.migrate.logging.MigrateLoggerLogrbToUseResourceBundle
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Contributors
* [Aaron Gershman](aegershman@gmail.com)
* [Knut Wannheden](knut@moderne.io)
* [Tyler Van Gorder](tkvangorder@users.noreply.github.com)
* [Sam Snyder](sam@moderne.io)
* [Jonathan Schnéider](jkschneider@gmail.com)


## See how this recipe works across multiple open-source repositories

[![Moderne Link Image](/.gitbook/assets/ModerneRecipeButton.png)](https://app.moderne.io/recipes/org.openrewrite.java.migrate.logging.MigrateLoggerLogrbToUseResourceBundle)

The community edition of the Moderne platform enables you to easily run recipes across thousands of open-source repositories.

Please [contact Moderne](https://moderne.io/product) for more information about safely running the recipes on your own codebase in a private SaaS.
