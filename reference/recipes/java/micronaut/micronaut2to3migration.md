# Migrate from Micronaut 2.x to 3.x

 **org.openrewrite.java.micronaut.Micronaut2to3Migration** _This recipe will apply changes required for migrating from Micronaut 2 to Micronaut 3._

## Source

[Github](https://github.com/openrewrite/rewrite-micronaut), [Issue Tracker](https://github.com/openrewrite/rewrite-micronaut/issues), [Maven Central](https://search.maven.org/artifact/org.openrewrite.recipe/rewrite-micronaut/0.2.0/jar)

* groupId: org.openrewrite.recipe
* artifactId: rewrite-micronaut
* version: 0.2.0

## Usage

This recipe has no required configuration options and can be activated directly after taking a dependency on org.openrewrite.recipe:rewrite-micronaut:0.2.0 in your build file:

{% tabs %}
{% tab title="Gradle" %}
{% code title="build.gradle" %}
```groovy
plugins {
    id("org.openrewrite.rewrite") version("5.4.0")
}

rewrite {
    activeRecipe("org.openrewrite.java.micronaut.Micronaut2to3Migration")
}

repositories {
    mavenCentral()
}

dependencies {
    rewrite("org.openrewrite.recipe:rewrite-micronaut:0.2.0")
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
            <recipe>org.openrewrite.java.micronaut.Micronaut2to3Migration</recipe>
          </activeRecipes>
        </configuration>
        <dependencies>
          <dependency>
            <groupId>org.openrewrite.recipe</groupId>
            <artifactId>rewrite-micronaut</artifactId>
            <version>0.2.0</version>
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

Recipes can also be activated directly from the command line by adding the argument `-DactiveRecipe=org.openrewrite.java.micronaut.Micronaut2to3Migration`

## Definition

{% tabs %}
{% tab title="Recipe List" %}
* [Upgrade Maven parent project version](../../maven/upgradeparentversion.md)
  * groupId: `io.micronaut`
  * artifactId: `micronaut-parent`
  * newVersion: `3.0.0-M2`
* [Upgrade Maven dependency version](../../maven/upgradedependencyversion.md)
  * groupId: `io.micronaut`
  * artifactId: `micronaut-bom`
  * newVersion: `3.0.0-M2`
  * trustParent: `true`
* [Rename package name](../changepackage.md)
  * oldPackageName: `io.micronaut.configuration.cassandra`
  * newPackageName: `io.micronaut.cassandra`
* [Change method name](../changemethodname.md)
  * methodPattern: `io.micronaut.context.ApplicationContext build(..)`
  * newMethodName: `builder`
* [Change type](../changetype.md)
  * oldFullyQualifiedTypeName: `io.micronaut.core.async.SupplierUtil`
  * newFullyQualifiedTypeName: `io.micronaut.core.util.SupplierUtil`
* [Change method name](../changemethodname.md)
  * methodPattern: `io.micronaut.http.netty.stream.DelegateHttpRequest getMethod()`
  * newMethodName: `method`
* [Change method name](../changemethodname.md)
  * methodPattern: `io.micronaut.http.netty.stream.DelegateHttpResponse getStatus()`
  * newMethodName: `status`
* [Change method name](../changemethodname.md)
  * methodPattern: `io.micronaut.http.server.netty.DelegateHttpResponse getStatus()`
  * newMethodName: `status`
* [Change method name](../changemethodname.md)
  * methodPattern: `io.micronaut.http.netty.stream.DelegateHttpRequest getUri()`
  * newMethodName: `uri`
* [Change method name](../changemethodname.md)
  * methodPattern: `io.micronaut.http.netty.stream.DelegateHttpMessage getDecoderResult()`
  * newMethodName: `decoderResult`
* [Change method name](../changemethodname.md)
  * methodPattern: `io.micronaut.http.netty.stream.DelegateHttpMessage getProtocolVersion()`
  * newMethodName: `protocolVersion`
* [Change type](../changetype.md)
  * oldFullyQualifiedTypeName: `io.micronaut.management.endpoint.beans.impl.RxJavaBeanDefinitionDataCollector`
  * newFullyQualifiedTypeName: `io.micronaut.management.endpoint.beans.impl.DefaultBeanDefinitionDataCollector`
* [Change type](../changetype.md)
  * oldFullyQualifiedTypeName: `io.micronaut.management.endpoint.routes.impl.RxJavaRouteDataCollector`
  * newFullyQualifiedTypeName: `io.micronaut.management.endpoint.routes.impl.DefaultRouteDataCollector`
* [Change type](../changetype.md)
  * oldFullyQualifiedTypeName: `io.micronaut.management.health.aggregator.RxJavaHealthAggregator`
  * newFullyQualifiedTypeName: `io.micronaut.management.health.aggregator.DefaultHealthAggregator`
* [Change type](../changetype.md)
  * oldFullyQualifiedTypeName: `io.micronaut.messaging.annotation.Body`
  * newFullyQualifiedTypeName: `io.micronaut.messaging.annotation.MessageBody`
* [Change type](../changetype.md)
  * oldFullyQualifiedTypeName: `io.micronaut.messaging.annotation.Headers`
  * newFullyQualifiedTypeName: `io.micronaut.messaging.annotation.MessageHeaders`
* [Change method name](../changemethodname.md)
  * methodPattern: `io.micronaut.rss.itunespodcast.ItunesPodcast isExplict()`
  * newMethodName: `isExplicit`
* [Change method name](../changemethodname.md)
  * methodPattern: `io.micronaut.rss.itunespodcast.ItunesPodcast setExplict(boolean)`
  * newMethodName: `setExplicit`
* [Change method name](../changemethodname.md)
  * methodPattern: `io.micronaut.rss.itunespodcast.ItunesPodcast explict(boolean)`
  * newMethodName: `setExplicit`
* [Change type](../changetype.md)
  * oldFullyQualifiedTypeName: `io.micronaut.runtime.server.EmbeddedServerInstance`
  * newFullyQualifiedTypeName: `io.micronaut.discovery.EmbeddedServerInstance`
* [Change method name](../changemethodname.md)
  * methodPattern: `io.micronaut.web.router accept(io.micronaut.http.MediaType)`
  * newMethodName: `doesConsume`
* [Change method name](../changemethodname.md)
  * methodPattern: `io.micronaut.web.router.Route acceptAll()`
  * newMethodName: `consumesAll`
* [Change method name](../changemethodname.md)
  * methodPattern: `io.micronaut.web.router.RouteMatch accept(io.micronaut.http.MediaType)`
  * newMethodName: `doesConsume`
* [Change method name](../changemethodname.md)
  * methodPattern: `io.micronaut.web.router.RouteMatch explicitAccept(io.micronaut.http.MediaType)`
  * newMethodName: `explicitlyConsumes`
* [De-capitalize `BeanIntrospection` `getProperty(..)` and `getRequiredProperty(..)` name arguments](beanpropertycapitalizationstrategy.md)
* [Copy non-inherited annotations from super class](copynoninheritedannotationsfromsuperclass.md)
* [Add typed bean annotation to beans produced by factories](factorybeansaretyped.md)
* [Convert `OncePerRequestServerFilter` extensions to `HttpServerFilter`](onceperrequesthttpserverfiltertohttpserverfilter.md)
* [`Provider` implementation beans to Micronaut `@Factory`](providerimplementationstomicronautfactories.md)
* [Add `@Introspected` to classes requiring a map representation](typerequiresintrospection.md)
{% endtab %}

{% tab title="Yaml Recipe List" %}
```yaml
---
type: specs.openrewrite.org/v1beta/recipe
name: org.openrewrite.java.micronaut.Micronaut2to3Migration
displayName: Migrate from Micronaut 2.x to 3.x
description: This recipe will apply changes required for migrating from Micronaut 2 to Micronaut 3.
recipeList:
  - org.openrewrite.maven.UpgradeParentVersion:
      groupId: io.micronaut
      artifactId: micronaut-parent
      newVersion: 3.0.0-M2
  - org.openrewrite.maven.UpgradeDependencyVersion:
      groupId: io.micronaut
      artifactId: micronaut-bom
      newVersion: 3.0.0-M2
      trustParent: true
  - org.openrewrite.java.ChangePackage:
      oldPackageName: io.micronaut.configuration.cassandra
      newPackageName: io.micronaut.cassandra
  - org.openrewrite.java.ChangeMethodName:
      methodPattern: io.micronaut.context.ApplicationContext build(..)
      newMethodName: builder
  - org.openrewrite.java.ChangeType:
      oldFullyQualifiedTypeName: io.micronaut.core.async.SupplierUtil
      newFullyQualifiedTypeName: io.micronaut.core.util.SupplierUtil
  - org.openrewrite.java.ChangeMethodName:
      methodPattern: io.micronaut.http.netty.stream.DelegateHttpRequest getMethod()
      newMethodName: method
  - org.openrewrite.java.ChangeMethodName:
      methodPattern: io.micronaut.http.netty.stream.DelegateHttpResponse getStatus()
      newMethodName: status
  - org.openrewrite.java.ChangeMethodName:
      methodPattern: io.micronaut.http.server.netty.DelegateHttpResponse getStatus()
      newMethodName: status
  - org.openrewrite.java.ChangeMethodName:
      methodPattern: io.micronaut.http.netty.stream.DelegateHttpRequest getUri()
      newMethodName: uri
  - org.openrewrite.java.ChangeMethodName:
      methodPattern: io.micronaut.http.netty.stream.DelegateHttpMessage getDecoderResult()
      newMethodName: decoderResult
  - org.openrewrite.java.ChangeMethodName:
      methodPattern: io.micronaut.http.netty.stream.DelegateHttpMessage getProtocolVersion()
      newMethodName: protocolVersion
  - org.openrewrite.java.ChangeType:
      oldFullyQualifiedTypeName: io.micronaut.management.endpoint.beans.impl.RxJavaBeanDefinitionDataCollector
      newFullyQualifiedTypeName: io.micronaut.management.endpoint.beans.impl.DefaultBeanDefinitionDataCollector
  - org.openrewrite.java.ChangeType:
      oldFullyQualifiedTypeName: io.micronaut.management.endpoint.routes.impl.RxJavaRouteDataCollector
      newFullyQualifiedTypeName: io.micronaut.management.endpoint.routes.impl.DefaultRouteDataCollector
  - org.openrewrite.java.ChangeType:
      oldFullyQualifiedTypeName: io.micronaut.management.health.aggregator.RxJavaHealthAggregator
      newFullyQualifiedTypeName: io.micronaut.management.health.aggregator.DefaultHealthAggregator
  - org.openrewrite.java.ChangeType:
      oldFullyQualifiedTypeName: io.micronaut.messaging.annotation.Body
      newFullyQualifiedTypeName: io.micronaut.messaging.annotation.MessageBody
  - org.openrewrite.java.ChangeType:
      oldFullyQualifiedTypeName: io.micronaut.messaging.annotation.Headers
      newFullyQualifiedTypeName: io.micronaut.messaging.annotation.MessageHeaders
  - org.openrewrite.java.ChangeMethodName:
      methodPattern: io.micronaut.rss.itunespodcast.ItunesPodcast isExplict()
      newMethodName: isExplicit
  - org.openrewrite.java.ChangeMethodName:
      methodPattern: io.micronaut.rss.itunespodcast.ItunesPodcast setExplict(boolean)
      newMethodName: setExplicit
  - org.openrewrite.java.ChangeMethodName:
      methodPattern: io.micronaut.rss.itunespodcast.ItunesPodcast explict(boolean)
      newMethodName: setExplicit
  - org.openrewrite.java.ChangeType:
      oldFullyQualifiedTypeName: io.micronaut.runtime.server.EmbeddedServerInstance
      newFullyQualifiedTypeName: io.micronaut.discovery.EmbeddedServerInstance
  - org.openrewrite.java.ChangeMethodName:
      methodPattern: io.micronaut.web.router accept(io.micronaut.http.MediaType)
      newMethodName: doesConsume
  - org.openrewrite.java.ChangeMethodName:
      methodPattern: io.micronaut.web.router.Route acceptAll()
      newMethodName: consumesAll
  - org.openrewrite.java.ChangeMethodName:
      methodPattern: io.micronaut.web.router.RouteMatch accept(io.micronaut.http.MediaType)
      newMethodName: doesConsume
  - org.openrewrite.java.ChangeMethodName:
      methodPattern: io.micronaut.web.router.RouteMatch explicitAccept(io.micronaut.http.MediaType)
      newMethodName: explicitlyConsumes
  - org.openrewrite.java.micronaut.BeanPropertyCapitalizationStrategy
  - org.openrewrite.java.micronaut.CopyNonInheritedAnnotationsFromSuperClass
  - org.openrewrite.java.micronaut.FactoryBeansAreTyped
  - org.openrewrite.java.micronaut.OncePerRequestHttpServerFilterToHttpServerFilter
  - org.openrewrite.java.micronaut.ProviderImplementationsToMicronautFactories
  - org.openrewrite.java.micronaut.TypeRequiresIntrospection
```
{% endtab %}
{% endtabs %}

