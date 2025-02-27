# Add explicit JAX-WS dependencies

 **org.openrewrite.java.migrate.javax.AddJaxwsDependencies** _This recipe will add the necessary JAX-WS dependencies for those projects migrating to Java 11._

### Tags

* glassfish
* javax
* java11
* jaxws
* jakarta

## Source

[Github](https://github.com/openrewrite/rewrite-migrate-java), [Issue Tracker](https://github.com/openrewrite/rewrite-migrate-java/issues), [Maven Central](https://search.maven.org/artifact/org.openrewrite.recipe/rewrite-migrate-java/0.5.0/jar)

* groupId: org.openrewrite.recipe
* artifactId: rewrite-migrate-java
* version: 0.5.0

## Usage

This recipe has no required configuration options and can be activated directly after taking a dependency on org.openrewrite.recipe:rewrite-migrate-java:0.5.0 in your build file:

{% tabs %}
{% tab title="Gradle" %}
{% code title="build.gradle" %}
```groovy
plugins {
    id("org.openrewrite.rewrite") version("5.4.0")
}

rewrite {
    activeRecipe("org.openrewrite.java.migrate.javax.AddJaxwsDependencies")
}

repositories {
    mavenCentral()
}

dependencies {
    rewrite("org.openrewrite.recipe:rewrite-migrate-java:0.5.0")
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
            <recipe>org.openrewrite.java.migrate.javax.AddJaxwsDependencies</recipe>
          </activeRecipes>
        </configuration>
        <dependencies>
          <dependency>
            <groupId>org.openrewrite.recipe</groupId>
            <artifactId>rewrite-migrate-java</artifactId>
            <version>0.5.0</version>
          </dependency>
        </dependencies>
      </plugin>
    </plugins>
  </build>
</project>
```
{% endcode %}
{% endtab %}
{% endtabs %}

Recipes can also be activated directly from the command line by adding the argument `-DactiveRecipe=org.openrewrite.java.migrate.javax.AddJaxwsDependencies`

## Definition

{% tabs %}
{% tab title="Recipe List" %}
* [Add Maven dependency](../../../maven/adddependency.md)
  * groupId: `jakarta.xml.ws`
  * artifactId: `jakarta.xml.ws-api`
  * version: `2.3.x`
  * releasesOnly: `false`
  * onlyIfUsing: `[javax.jws.*]`
* [Upgrade Maven dependency version](../../../maven/upgradedependencyversion.md)
  * groupId: `jakarta.xml.ws`
  * artifactId: `jakarta.xml.ws-api`
  * newVersion: `2.3.x`
* [Add Maven dependency](../../../maven/adddependency.md)
  * groupId: `com.sun.xml.ws`
  * artifactId: `jaxws-rt`
  * version: `2.3.x`
  * releasesOnly: `false`
  * scope: `runtime`
  * onlyIfUsing: `[javax.jws.*]`
* [Upgrade Maven dependency version](../../../maven/upgradedependencyversion.md)
  * groupId: `com.sun.xml.ws`
  * artifactId: `jaxws-rt`
  * newVersion: `2.3.x`
* [Remove Maven dependency](../../../maven/removedependency.md)
  * groupId: `javax.xml.ws`
  * artifactId: `jaxws-api`
{% endtab %}

{% tab title="Yaml Recipe List" %}
```yaml
---
type: specs.openrewrite.org/v1beta/recipe
name: org.openrewrite.java.migrate.javax.AddJaxwsDependencies
displayName: Add explicit JAX-WS dependencies
description: This recipe will add the necessary JAX-WS dependencies for those projects migrating to Java 11.
tags:
  - glassfish
  - javax
  - java11
  - jaxws
  - jakarta
recipeList:
  - org.openrewrite.maven.AddDependency:
      groupId: jakarta.xml.ws
      artifactId: jakarta.xml.ws-api
      version: 2.3.x
      releasesOnly: false
      onlyIfUsing: [javax.jws.*]
  - org.openrewrite.maven.UpgradeDependencyVersion:
      groupId: jakarta.xml.ws
      artifactId: jakarta.xml.ws-api
      newVersion: 2.3.x
  - org.openrewrite.maven.AddDependency:
      groupId: com.sun.xml.ws
      artifactId: jaxws-rt
      version: 2.3.x
      releasesOnly: false
      scope: runtime
      onlyIfUsing: [javax.jws.*]
  - org.openrewrite.maven.UpgradeDependencyVersion:
      groupId: com.sun.xml.ws
      artifactId: jaxws-rt
      newVersion: 2.3.x
  - org.openrewrite.maven.RemoveDependency:
      groupId: javax.xml.ws
      artifactId: jaxws-api
```
{% endtab %}
{% endtabs %}

