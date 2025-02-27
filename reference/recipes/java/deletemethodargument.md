# Delete method argument

 **org.openrewrite.java.DeleteMethodArgument** _Delete an argument from method invocations._

## Source

[Github](https://github.com/openrewrite/rewrite), [Issue Tracker](https://github.com/openrewrite/rewrite/issues), [Maven Central](https://search.maven.org/artifact/org.openrewrite/rewrite-java/7.10.0/jar)

* groupId: org.openrewrite
* artifactId: rewrite-java
* version: 7.10.0

## Options

| Type | Name | Description |
| :--- | :--- | :--- |
| `String` | methodPattern | A method pattern, expressed as a [pointcut expression](https://github.com/openrewrite/rewrite-docs/tree/655780b8d7b50826bb9e9df40aa5263379183ba8/v1beta/pointcut-expressions/README.md), that is used to find matching method invocations. |
| `int` | argumentIndex | A zero-based index that indicates which argument will be removed from the method invocation. |

## Usage

This recipe has required configuration parameters. Recipes with required configuration parameters cannot be activated directly. To activate this recipe you must create a new recipe which fills in the required parameters. In your rewrite.yml create a new recipe with a unique name. For example: `com.yourorg.DeleteMethodArgumentExample`. Here's how you can define and customize such a recipe within your rewrite.yml:

{% code title="rewrite.yml" %}
```yaml
---
type: specs.openrewrite.org/v1beta/recipe
name: com.yourorg.DeleteMethodArgumentExample
displayName: Delete method argument example
recipeList:
  - org.openrewrite.java.DeleteMethodArgument:
      methodPattern: com.yourorg.A foo(int, int)
      argumentIndex: 0
```
{% endcode %}

Now that `com.yourorg.DeleteMethodArgumentExample` has been defined activate it in your build file:

{% tabs %}
{% tab title="Gradle" %}
{% code title="build.gradle" %}
```groovy
plugins {
    id("org.openrewrite.rewrite") version("5.4.0")
}

rewrite {
    activeRecipe("com.yourorg.DeleteMethodArgumentExample")
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
        <version>4.8.0</version>
        <configuration>
          <activeRecipes>
            <recipe>com.yourorg.DeleteMethodArgumentExample</recipe>
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

Recipes can also be activated directly from the commandline by adding the argument `-DactiveRecipe=com.yourorg.DeleteMethodArgumentExample`

