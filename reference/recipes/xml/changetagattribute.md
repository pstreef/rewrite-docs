# Change XML Attribute

**org.openrewrite.xml.ChangeTagAttribute**

_Alters XML Attribute value within specified element._

## Source

[GitHub](https://github.com/openrewrite/rewrite/blob/main/rewrite-xml/src/main/java/org/openrewrite/xml/ChangeTagAttribute.java), [Issue Tracker](https://github.com/openrewrite/rewrite/issues), [Maven Central](https://central.sonatype.com/artifact/org.openrewrite/rewrite-xml/8.1.3/jar)

* groupId: org.openrewrite
* artifactId: rewrite-xml
* version: 8.1.3

## Options

| Type | Name | Description |
| -- | -- | -- |
| `String` | elementName | The name of the element whose attribute's value is to be changed. Interpreted as an XPath Expression. |
| `String` | attributeName | The name of the attribute whose value is to be changed. |
| `String` | newValue | The new value to be used for key specified by `attributeName`, Set to null if you want to remove the attribute. |
| `String` | oldValue | *Optional*. Only change the property value if it matches the configured `oldValue`. |

## Example

###### Parameters
| Parameter | Value |
| -- | -- |
|elementName|`bean`|
|attributeName|`id`|
|newValue|`myBean2.subpackage`|
|oldValue|`myBean.subpackage`|


{% tabs %}
{% tab title="xml" %}

###### Before
{% code %}
```xml
<beans>
    <bean id='myBean.subpackage.subpackage2'/>
    <other id='myBean.subpackage.subpackage2'/>
</beans>
```
{% endcode %}

###### After
{% code %}
```xml
<beans>
    <bean id='myBean2.subpackage.subpackage2'/>
    <other id='myBean.subpackage.subpackage2'/>
</beans>
```
{% endcode %}

{% endtab %}
{% tab title="Diff" %}
{% code %}
```diff
@@ -2,1 +2,1 @@
<beans>
-   <bean id='myBean.subpackage.subpackage2'/>
+   <bean id='myBean2.subpackage.subpackage2'/>
    <other id='myBean.subpackage.subpackage2'/>
```
{% endcode %}
{% endtab %}
{% endtabs %}


## Usage

This recipe has required configuration parameters. Recipes with required configuration parameters cannot be activated directly. To activate this recipe you must create a new recipe which fills in the required parameters. In your `rewrite.yml` create a new recipe with a unique name. For example: `com.yourorg.ChangeTagAttributeExample`.
Here's how you can define and customize such a recipe within your rewrite.yml:

{% code title="rewrite.yml" %}
```yaml
---
type: specs.openrewrite.org/v1beta/recipe
name: com.yourorg.ChangeTagAttributeExample
displayName: Change XML Attribute example
recipeList:
  - org.openrewrite.xml.ChangeTagAttribute:
      elementName: property
      attributeName: name
      newValue: newfoo.bar.attribute.value.string
      oldValue: foo.bar.attribute.value.string
```
{% endcode %}

Now that `com.yourorg.ChangeTagAttributeExample` has been defined activate it in your build file:
{% tabs %}
{% tab title="Gradle" %}
{% code title="build.gradle" %}
```groovy
plugins {
    id("org.openrewrite.rewrite") version("6.1.4")
}

rewrite {
    activeRecipe("com.yourorg.ChangeTagAttributeExample")
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
            <recipe>com.yourorg.ChangeTagAttributeExample</recipe>
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
* [Mark Brophy](36955467+m-brophy@users.noreply.github.com)
* [Kun Li](kun@moderne.io)
* [Jonathan Schnéider](jkschneider@gmail.com)
* [Sam Snyder](sam@moderne.io)


## See how this recipe works across multiple open-source repositories

[![Moderne Link Image](/.gitbook/assets/ModerneRecipeButton.png)](https://app.moderne.io/recipes/org.openrewrite.xml.ChangeTagAttribute)

The community edition of the Moderne platform enables you to easily run recipes across thousands of open-source repositories.

Please [contact Moderne](https://moderne.io/product) for more information about safely running the recipes on your own codebase in a private SaaS.
