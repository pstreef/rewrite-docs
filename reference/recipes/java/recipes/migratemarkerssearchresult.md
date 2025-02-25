# Migrate deprecated `org.openrewrite.marker.Markers#SearchResult(..)`

**org.openrewrite.java.recipes.MigrateMarkersSearchResult**

_Methods of `org.openrewrite.marker.Markers#SearchResult(..)` are deprecated and removed in rewrite 8, use `SearchResult.found()` instead._

### Tags

* Rewrite8 migration

## Source

[GitHub](https://github.com/openrewrite/rewrite/blob/main/rewrite-java/src/main/java/org/openrewrite/java/recipes/MigrateMarkersSearchResult.java), [Issue Tracker](https://github.com/openrewrite/rewrite/issues), [Maven Central](https://central.sonatype.com/artifact/org.openrewrite/rewrite-java/8.1.3/jar)

* groupId: org.openrewrite
* artifactId: rewrite-java
* version: 8.1.3

## Example


{% tabs %}
{% tab title="org/openrewrite/kubernetes/resource/FindExceedsResourceRatio.java" %}

###### Before
{% code title="org/openrewrite/kubernetes/resource/FindExceedsResourceRatio.java" %}
```java
package org.openrewrite.kubernetes.resource;

import lombok.EqualsAndHashCode;
import lombok.Value;
import org.openrewrite.*;
import org.openrewrite.yaml.YamlIsoVisitor;
import org.openrewrite.yaml.tree.Yaml;

@Value
@EqualsAndHashCode(callSuper = true)
public class FindExceedsResourceRatio extends Recipe {
    @Override
    public String getDisplayName() {
        return "Find exceeds resource ratio";
    }

    @Override
    protected TreeVisitor<?, ExecutionContext> getVisitor() {
        return new YamlIsoVisitor<ExecutionContext>() {
            @Override
            public Yaml.Mapping.Entry visitMappingEntry(Yaml.Mapping.Entry entry, ExecutionContext ctx) {
                Yaml.Mapping.Entry e = super.visitMappingEntry(entry, ctx);
                return e.withMarkers(e.getMarkers().searchResult("foo"));
            }
        };
    }
}
```
{% endcode %}

###### After
{% code title="org/openrewrite/kubernetes/resource/FindExceedsResourceRatio.java" %}
```java
package org.openrewrite.kubernetes.resource;

import lombok.EqualsAndHashCode;
import lombok.Value;
import org.openrewrite.*;
import org.openrewrite.marker.SearchResult;
import org.openrewrite.yaml.YamlIsoVisitor;
import org.openrewrite.yaml.tree.Yaml;

@Value
@EqualsAndHashCode(callSuper = true)
public class FindExceedsResourceRatio extends Recipe {
    @Override
    public String getDisplayName() {
        return "Find exceeds resource ratio";
    }

    @Override
    protected TreeVisitor<?, ExecutionContext> getVisitor() {
        return new YamlIsoVisitor<ExecutionContext>() {
            @Override
            public Yaml.Mapping.Entry visitMappingEntry(Yaml.Mapping.Entry entry, ExecutionContext ctx) {
                Yaml.Mapping.Entry e = super.visitMappingEntry(entry, ctx);
                return SearchResult.found(e, "foo");
            }
        };
    }
}
```
{% endcode %}

{% endtab %}
{% tab title="Diff" %}
{% code %}
```diff
--- org/openrewrite/kubernetes/resource/FindExceedsResourceRatio.java
+++ org/openrewrite/kubernetes/resource/FindExceedsResourceRatio.java
@@ -6,0 +6,1 @@
import lombok.Value;
import org.openrewrite.*;
+import org.openrewrite.marker.SearchResult;
import org.openrewrite.yaml.YamlIsoVisitor;
@@ -23,1 +24,1 @@
            public Yaml.Mapping.Entry visitMappingEntry(Yaml.Mapping.Entry entry, ExecutionContext ctx) {
                Yaml.Mapping.Entry e = super.visitMappingEntry(entry, ctx);
-               return e.withMarkers(e.getMarkers().searchResult("foo"));
+               return SearchResult.found(e, "foo");
            }
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
    activeRecipe("org.openrewrite.java.recipes.MigrateMarkersSearchResult")
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
            <recipe>org.openrewrite.java.recipes.MigrateMarkersSearchResult</recipe>
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
  -Drewrite.activeRecipes=org.openrewrite.java.recipes.MigrateMarkersSearchResult
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Contributors
* [Kun Li](kun@moderne.io)
* [Jonathan Schnéider](jkschneider@gmail.com)


## See how this recipe works across multiple open-source repositories

[![Moderne Link Image](/.gitbook/assets/ModerneRecipeButton.png)](https://app.moderne.io/recipes/org.openrewrite.java.recipes.MigrateMarkersSearchResult)

The community edition of the Moderne platform enables you to easily run recipes across thousands of open-source repositories.

Please [contact Moderne](https://moderne.io/product) for more information about safely running the recipes on your own codebase in a private SaaS.
