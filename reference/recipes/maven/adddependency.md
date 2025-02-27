# Add Maven dependency

 **org.openrewrite.maven.AddDependency** _Add the specified Maven dependency to the pom.xml._

## Source

[Github](https://github.com/openrewrite/rewrite), [Issue Tracker](https://github.com/openrewrite/rewrite/issues), [Maven Central](https://search.maven.org/artifact/org.openrewrite/rewrite-maven/7.10.0/jar)

* groupId: org.openrewrite
* artifactId: rewrite-maven
* version: 7.10.0

## Options

| Type | Name | Description |
| :--- | :--- | :--- |
| `String` | groupId | The first part of a dependency coordinate 'com.google.guava:guava:VERSION'. |
| `String` | artifactId | The second part of a dependency coordinate 'com.google.guava:guava:VERSION'. |
| `String` | version | An exact version number, or node-style semver selector used to select the version number. |
| `String` | versionPattern | _Optional_. Allows version selection to be extended beyond the original Node Semver semantics. So for example,Setting 'version' to "25-29" can be paired with a metadata pattern of "-jre" to select Guava 29.0-jre |
| `boolean` | releasesOnly | _Optional_. Whether to exclude snapshots from consideration. |
| `String` | classifier | _Optional_. A Maven classifier to add. Most commonly used to select shaded or test variants of a library |
| `String` | scope | _Optional_. The maven dependency scope to add the dependency to. |
| `String` | type | _Optional_. The type of dependency to add. If omitted Maven defaults to assuming the type is "jar". |
| `Boolean` | optional | _Optional_. Set the value of the `<optional>` tag. No `<optional>` tag will be added when this is `null`. |
| `String` | familyPattern | _Optional_. A pattern, applied to groupIds, used to determine which other dependencies should have aligned version numbers. Accepts '\*' as a wildcard character. |
| `List` | onlyIfUsing | _Optional_. Add the dependency only if using one of the supplied types. Types should be identified by fully qualified class name or a glob expression |

## Usage

This recipe has required configuration parameters. Recipes with required configuration parameters cannot be activated directly. To activate this recipe you must create a new recipe which fills in the required parameters. In your rewrite.yml create a new recipe with a unique name. For example: `com.yourorg.AddDependencyExample`. Here's how you can define and customize such a recipe within your rewrite.yml:

{% code title="rewrite.yml" %}
```yaml
---
type: specs.openrewrite.org/v1beta/recipe
name: com.yourorg.AddDependencyExample
displayName: Add Maven dependency example
recipeList:
  - org.openrewrite.maven.AddDependency:
      groupId: com.google.guava
      artifactId: guava
      version: 29.X
      versionPattern: -jre
      releasesOnly: true
      classifier: test
      scope: compile
      type: jar
      optional: true
      familyPattern: com.fasterxml.jackson*
      onlyIfUsing: org.junit.jupiter.api.*
```
{% endcode %}

Now that `com.yourorg.AddDependencyExample` has been defined activate it in your build file:

{% tabs %}
{% tab title="Gradle" %}
{% code title="build.gradle" %}
```groovy
plugins {
    id("org.openrewrite.rewrite") version("5.4.0")
}

rewrite {
    activeRecipe("com.yourorg.AddDependencyExample")
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
            <recipe>com.yourorg.AddDependencyExample</recipe>
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

Recipes can also be activated directly from the commandline by adding the argument `-DactiveRecipe=com.yourorg.AddDependencyExample`

