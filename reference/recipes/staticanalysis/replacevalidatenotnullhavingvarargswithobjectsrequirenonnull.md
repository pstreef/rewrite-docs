# Replace `org.apache.commons.lang3.Validate#notNull` with `Objects#requireNonNull`

**org.openrewrite.staticanalysis.ReplaceValidateNotNullHavingVarargsWithObjectsRequireNonNull**

_Replace `org.apache.commons.lang3.Validate.notNull(Object, String, Object[])` with `Objects.requireNonNull(Object, String)`._

## Source

[GitHub](https://github.com/openrewrite/rewrite-static-analysis/blob/main/src/main/java/org/openrewrite/staticanalysis/ReplaceValidateNotNullHavingVarargsWithObjectsRequireNonNull.java), [Issue Tracker](https://github.com/openrewrite/rewrite-static-analysis/issues), [Maven Central](https://central.sonatype.com/artifact/org.openrewrite.recipe/rewrite-static-analysis/1.0.1/jar)

* groupId: org.openrewrite.recipe
* artifactId: rewrite-static-analysis
* version: 1.0.1

## Example


{% tabs %}
{% tab title="Test.java" %}

###### Before
{% code title="Test.java" %}
```java
import org.apache.commons.lang3.Validate;
class Test {
    void test(Object obj) {
        Validate.notNull(obj, "Object should not be null");
    }
}
```
{% endcode %}

###### After
{% code title="Test.java" %}
```java
import java.util.Objects;

class Test {
    void test(Object obj) {
        Objects.requireNonNull(obj, "Object should not be null");
    }
}
```
{% endcode %}

{% endtab %}
{% tab title="Diff" %}
{% code %}
```diff
--- Test.java
+++ Test.java
@@ -1,1 +1,2 @@
-import org.apache.commons.lang3.Validate;
+import java.util.Objects;
+
class Test {
@@ -4,1 +5,1 @@
class Test {
    void test(Object obj) {
-       Validate.notNull(obj, "Object should not be null");
+       Objects.requireNonNull(obj, "Object should not be null");
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
    activeRecipe("org.openrewrite.staticanalysis.ReplaceValidateNotNullHavingVarargsWithObjectsRequireNonNull")
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
            <recipe>org.openrewrite.staticanalysis.ReplaceValidateNotNullHavingVarargsWithObjectsRequireNonNull</recipe>
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
  -Drewrite.activeRecipes=org.openrewrite.staticanalysis.ReplaceValidateNotNullHavingVarargsWithObjectsRequireNonNull
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Contributors
* [srmalkan](smitmalkan99@gmail.com)
* [Knut Wannheden](knut@moderne.io)


## See how this recipe works across multiple open-source repositories

[![Moderne Link Image](/.gitbook/assets/ModerneRecipeButton.png)](https://app.moderne.io/recipes/org.openrewrite.staticanalysis.ReplaceValidateNotNullHavingVarargsWithObjectsRequireNonNull)

The community edition of the Moderne platform enables you to easily run recipes across thousands of open-source repositories.

Please [contact Moderne](https://moderne.io/product) for more information about safely running the recipes on your own codebase in a private SaaS.
