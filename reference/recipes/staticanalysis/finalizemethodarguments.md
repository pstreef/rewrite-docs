# Finalize method arguments

**org.openrewrite.staticanalysis.FinalizeMethodArguments**

_Adds the `final` modifier keyword to method parameters._

## Source

[GitHub](https://github.com/openrewrite/rewrite-static-analysis/blob/main/src/main/java/org/openrewrite/staticanalysis/FinalizeMethodArguments.java), [Issue Tracker](https://github.com/openrewrite/rewrite-static-analysis/issues), [Maven Central](https://central.sonatype.com/artifact/org.openrewrite.recipe/rewrite-static-analysis/1.0.1/jar)

* groupId: org.openrewrite.recipe
* artifactId: rewrite-static-analysis
* version: 1.0.1

## Example


{% tabs %}
{% tab title="TestClass.java" %}

###### Before
{% code title="TestClass.java" %}
```java
    package com.test;

    class TestClass {

        private void getAccaCouponData(String responsiveRequestConfig, String card) {

        }
    }
```
{% endcode %}

###### After
{% code title="TestClass.java" %}
```java
    package com.test;

    class TestClass {

        private void getAccaCouponData(final String responsiveRequestConfig, final String card) {

        }
    }
```
{% endcode %}

{% endtab %}
{% tab title="Diff" %}
{% code %}
```diff
--- TestClass.java
+++ TestClass.java
@@ -5,1 +5,1 @@
    class TestClass {

-       private void getAccaCouponData(String responsiveRequestConfig, String card) {
+       private void getAccaCouponData(final String responsiveRequestConfig, final String card) {

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
    activeRecipe("org.openrewrite.staticanalysis.FinalizeMethodArguments")
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
            <recipe>org.openrewrite.staticanalysis.FinalizeMethodArguments</recipe>
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
  -Drewrite.activeRecipes=org.openrewrite.staticanalysis.FinalizeMethodArguments
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Contributors
* [Ioannis Tsiftzis](ioannis.tsiftzis@gmail.com)
* [Knut Wannheden](knut@moderne.io)
* [Kun Li](kun@moderne.io)
* [Jonathan Leitschuh](jonathan.leitschuh@gmail.com)


## See how this recipe works across multiple open-source repositories

[![Moderne Link Image](/.gitbook/assets/ModerneRecipeButton.png)](https://app.moderne.io/recipes/org.openrewrite.staticanalysis.FinalizeMethodArguments)

The community edition of the Moderne platform enables you to easily run recipes across thousands of open-source repositories.

Please [contact Moderne](https://moderne.io/product) for more information about safely running the recipes on your own codebase in a private SaaS.
