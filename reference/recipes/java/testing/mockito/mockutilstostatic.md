# Use static form of Mockito `MockUtil`

**org.openrewrite.java.testing.mockito.MockUtilsToStatic**

_Best-effort attempt to remove Mockito `MockUtil` instances._

## Source

[GitHub](https://github.com/openrewrite/rewrite-testing-frameworks/blob/main/src/main/java/org/openrewrite/java/testing/mockito/MockUtilsToStatic.java), [Issue Tracker](https://github.com/openrewrite/rewrite-testing-frameworks/issues), [Maven Central](https://central.sonatype.com/artifact/org.openrewrite.recipe/rewrite-testing-frameworks/2.0.2/jar)

* groupId: org.openrewrite.recipe
* artifactId: rewrite-testing-frameworks
* version: 2.0.2

## Example


{% tabs %}
{% tab title="mockito/example/MockitoMockUtils.java" %}

###### Before
{% code title="mockito/example/MockitoMockUtils.java" %}
```java
package mockito.example;

import org.mockito.internal.util.MockUtil;

public class MockitoMockUtils {
    public void isMockExample() {
        new MockUtil().isMock("I am a real String");
    }
}
```
{% endcode %}

###### After
{% code title="mockito/example/MockitoMockUtils.java" %}
```java
package mockito.example;

import org.mockito.internal.util.MockUtil;

public class MockitoMockUtils {
    public void isMockExample() {
        MockUtil.isMock("I am a real String");
    }
}
```
{% endcode %}

{% endtab %}
{% tab title="Diff" %}
{% code %}
```diff
--- mockito/example/MockitoMockUtils.java
+++ mockito/example/MockitoMockUtils.java
@@ -7,1 +7,1 @@
public class MockitoMockUtils {
    public void isMockExample() {
-       new MockUtil().isMock("I am a real String");
+       MockUtil.isMock("I am a real String");
    }
```
{% endcode %}
{% endtab %}
{% endtabs %}


## Usage

This recipe has no required configuration options. It can be activated by adding a dependency on `org.openrewrite.recipe:rewrite-testing-frameworks:2.0.2` in your build file or by running a shell command (in which case no build changes are needed): 
{% tabs %}
{% tab title="Gradle" %}
{% code title="build.gradle" %}
```groovy
plugins {
    id("org.openrewrite.rewrite") version("6.1.4")
}

rewrite {
    activeRecipe("org.openrewrite.java.testing.mockito.MockUtilsToStatic")
}

repositories {
    mavenCentral()
}

dependencies {
    rewrite("org.openrewrite.recipe:rewrite-testing-frameworks:2.0.2")
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
            <recipe>org.openrewrite.java.testing.mockito.MockUtilsToStatic</recipe>
          </activeRecipes>
        </configuration>
        <dependencies>
          <dependency>
            <groupId>org.openrewrite.recipe</groupId>
            <artifactId>rewrite-testing-frameworks</artifactId>
            <version>2.0.2</version>
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
  -Drewrite.recipeArtifactCoordinates=org.openrewrite.recipe:rewrite-testing-frameworks:RELEASE \
  -Drewrite.activeRecipes=org.openrewrite.java.testing.mockito.MockUtilsToStatic
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Contributors
* [Greg Adams](gadams@gmail.com)
* [Jonathan Schneider](jkschneider@gmail.com)
* [Patrick Way](pway99@users.noreply.github.com)
* [Sam Snyder](sam@moderne.io)
* [Knut Wannheden](knut@moderne.io)
* [Tim te Beek](timtebeek@gmail.com)
* [Aaron Gershman](aegershman@gmail.com)
* [Patrick](patway99@gmail.com)


## See how this recipe works across multiple open-source repositories

[![Moderne Link Image](/.gitbook/assets/ModerneRecipeButton.png)](https://app.moderne.io/recipes/org.openrewrite.java.testing.mockito.MockUtilsToStatic)

The community edition of the Moderne platform enables you to easily run recipes across thousands of open-source repositories.

Please [contact Moderne](https://moderne.io/product) for more information about safely running the recipes on your own codebase in a private SaaS.
