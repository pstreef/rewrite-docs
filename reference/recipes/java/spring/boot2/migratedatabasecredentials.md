# Migrate flyway and liquibase credentials

**org.openrewrite.java.spring.boot2.MigrateDatabaseCredentials**

_If you currently define a `spring.flyway.url` or `spring.liquibase.url` you may need to provide additional username and password properties. In earlier versions of Spring Boot, these settings were derived from `spring.datasource` properties but this turned out to be problematic for people that provided their own `DataSource` beans._

## Source

[GitHub](https://github.com/openrewrite/rewrite-spring/blob/main/src/main/java/org/openrewrite/java/spring/boot2/MigrateDatabaseCredentials.java), [Issue Tracker](https://github.com/openrewrite/rewrite-spring/issues), [Maven Central](https://central.sonatype.com/artifact/org.openrewrite.recipe/rewrite-spring/5.0.1/jar)

* groupId: org.openrewrite.recipe
* artifactId: rewrite-spring
* version: 5.0.1

## Example


{% tabs %}
{% tab title="yaml" %}

###### Before
{% code %}
```yaml
spring:
  liquibase:
    url: host
```
{% endcode %}

###### After
{% code %}
```yaml
spring.liquibase:
  url: host
  username: ${spring.datasource.username}
  password: ${spring.datasource.password}
```
{% endcode %}

{% endtab %}
{% tab title="Diff" %}
{% code %}
```diff
@@ -1,3 +1,4 @@
-spring:
- liquibase:
-   url: host
+spring.liquibase:
+ url: host
+ username: ${spring.datasource.username}
+ password: ${spring.datasource.password}

```
{% endcode %}
{% endtab %}
{% endtabs %}


## Usage

This recipe has no required configuration options. It can be activated by adding a dependency on `org.openrewrite.recipe:rewrite-spring:5.0.1` in your build file or by running a shell command (in which case no build changes are needed): 
{% tabs %}
{% tab title="Gradle" %}
{% code title="build.gradle" %}
```groovy
plugins {
    id("org.openrewrite.rewrite") version("6.1.4")
}

rewrite {
    activeRecipe("org.openrewrite.java.spring.boot2.MigrateDatabaseCredentials")
}

repositories {
    mavenCentral()
}

dependencies {
    rewrite("org.openrewrite.recipe:rewrite-spring:5.0.1")
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
            <recipe>org.openrewrite.java.spring.boot2.MigrateDatabaseCredentials</recipe>
          </activeRecipes>
        </configuration>
        <dependencies>
          <dependency>
            <groupId>org.openrewrite.recipe</groupId>
            <artifactId>rewrite-spring</artifactId>
            <version>5.0.1</version>
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
  -Drewrite.recipeArtifactCoordinates=org.openrewrite.recipe:rewrite-spring:RELEASE \
  -Drewrite.activeRecipes=org.openrewrite.java.spring.boot2.MigrateDatabaseCredentials
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Definition

{% tabs %}
{% tab title="Recipe List" %}
* [Migrate flyway credentials](../../../java/spring/boot2/migratedatabasecredentials$migratedatabasecredentialsfortoolyaml.md)
* [Migrate flyway credentials](../../../java/spring/boot2/migratedatabasecredentials$migratedatabasecredentialsfortoolproperties.md)
* [Migrate liquibase credentials](../../../java/spring/boot2/migratedatabasecredentials$migratedatabasecredentialsfortoolyaml.md)
* [Migrate liquibase credentials](../../../java/spring/boot2/migratedatabasecredentials$migratedatabasecredentialsfortoolproperties.md)

{% endtab %}

{% tab title="Yaml Recipe List" %}
```yaml
---
type: specs.openrewrite.org/v1beta/recipe
name: org.openrewrite.java.spring.boot2.MigrateDatabaseCredentials
displayName: Migrate flyway and liquibase credentials
description: If you currently define a `spring.flyway.url` or `spring.liquibase.url` you may need to provide additional username and password properties. In earlier versions of Spring Boot, these settings were derived from `spring.datasource` properties but this turned out to be problematic for people that provided their own `DataSource` beans.
recipeList:
  - org.openrewrite.java.spring.boot2.MigrateDatabaseCredentials$MigrateDatabaseCredentialsForToolYaml
  - org.openrewrite.java.spring.boot2.MigrateDatabaseCredentials$MigrateDatabaseCredentialsForToolProperties
  - org.openrewrite.java.spring.boot2.MigrateDatabaseCredentials$MigrateDatabaseCredentialsForToolYaml
  - org.openrewrite.java.spring.boot2.MigrateDatabaseCredentials$MigrateDatabaseCredentialsForToolProperties

```
{% endtab %}
{% endtabs %}

## Contributors
* [Jonathan Schneider](jkschneider@gmail.com)
* [Knut Wannheden](knut@moderne.io)
* [Kyle Scully](scullykns@gmail.com)


## See how this recipe works across multiple open-source repositories

[![Moderne Link Image](/.gitbook/assets/ModerneRecipeButton.png)](https://app.moderne.io/recipes/org.openrewrite.java.spring.boot2.MigrateDatabaseCredentials)

The community edition of the Moderne platform enables you to easily run recipes across thousands of open-source repositories.

Please [contact Moderne](https://moderne.io/product) for more information about safely running the recipes on your own codebase in a private SaaS.
