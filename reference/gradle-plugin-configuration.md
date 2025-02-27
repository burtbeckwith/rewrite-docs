---
description: rewrite-gradle-plugin configuration options and task descriptions
---

# Gradle Plugin Configuration

The OpenRewrite Gradle Plugin is the fastest way to apply OpenRewrite recipes to your code as part of your Gradle build. The OpenRewrite Gradle Plugin is compatible with all versions of Gradle since 4.7.

## Plugin Configuration

Apply the org.openrewrite.rewrite plugin to your build.

```groovy
plugins {
    id("java")
    id("org.openrewrite.rewrite") version("5.4.0")
}

rewrite {
    // OpenRewrite Extension Configuration
}

// Ensure a repository is declared that the rewrite core libraries can be resolved from
repositories {
    mavenCentral() 
}
```

With the plugin applied, the `rewrite` DSL is available for configuration.

### Multi-Module Gradle Projects

The rewrite gradle plugin should only be applied to the root project. Refactoring operations will affect all projects that apply Gradle's java plugin.

{% hint style="warning" %}
The rewrite gradle plugin resolves the rewrite core libraries at runtime. It will attempt to resolve them from whatever repositories are available to the root project. This can be accomplished by adding Maven Central, or a mirror of it, to your root project.
{% endhint %}

### Configuring the 'rewrite' DSL

The `rewrite` DSL exposes a few configuration options:

* `activeRecipe` - Explicitly turns on recipes by name \(the name given in the `specs.openrewrite.org/v1beta/recipe` resource\). No recipe is run unless explicitly turned on with this setting.
* `activeStyle` - Explicitly turns on a style by name \(the name given in the `specs.openrewrite.org/v1beta/style` resource\). No style is applied unless explicitly turned on with this setting.
* `configFile` - Where to look for a OpenRewrite YML configuration file somewhere in the project directory \(or really anywhere on disk\). This file is not required to exist. If not specified otherwise, the default value is `<root project directory>/rewrite.yml`.
* `failOnDryRunResults` - Boolean flag toggling whether `rewriteDryRun` should throw an exception and non-zero exit code if changes are detected. Default is `false`.

```groovy
plugins {
    id("java")
    id("org.openrewrite.rewrite") version("5.4.0")
}

repositories {
    mavenCentral()
}

rewrite {
    activeRecipe("com.yourorg.ExampleRecipe", "com.yourorg.ExampleRecipe2")
    activeStyle("com.yourorg.ExampleStyle", "com.yourorg.ExampleStyle2")

    // These are default values, shown for example. It isn't necessary to supply these values manually:
    configFile = project.getRootProject().file("rewrite.yml")
    failOnDryRunResults = false
}
```

## Activating OpenRewrite Recipes

{% hint style="info" %}
All OpenRewrite libraries and modules are published to MavenCentral. Use the `repositories` Gradle DSL to ensure that your build can resolve dependencies from there or one of its mirrors.
{% endhint %}

No recipe is ever run on your codebase without being explicitly activated in the plugin's configuration. To make pre-packaged OpenRewrite recipes available for activation, add them as `rewrite` dependencies:

```groovy
dependencies {
    rewrite("org.openrewrite.recipe:rewrite-spring:4.8.0")
}
```

Once a pre-packaged recipe has been added to the `rewrite` dependency configuration, you can tell the Gradle plugin to activate it the `rewrite` DSL. For example, here is how you would activate the `org.openrewrite.java.testing.junit5.JUnit5BestPractices` recipe that comes with `rewrite-testing-frameworks` in a single-project Gradle build:

```groovy
plugins {
    id("java")
    id("org.openrewrite.rewrite") version("5.4.0")
}

repositories {
    mavenCentral()
}

dependencies {
    testImplementation("junit:junit:4.13")
    rewrite("org.openrewrite.recipe:rewrite-testing-frameworks:1.7.1")
}

rewrite {
    activeRecipe("org.openrewrite.java.testing.junit5.JUnit5BestPractices")
}
```

## The "Run" Task

Execute `gradle rewriteRun` to run the active recipes and apply the changes. This will write changes locally to your source files on disk. Afterward, review the changes, and when you are comfortable with the changes, commit them. The `run` goal generates warnings in the build log wherever it makes changes to source files.

![Showing which files were changed and by what visitors](../.gitbook/assets/rewrite-fix-gradle-output%20%282%29%20%282%29%20%284%29%20%284%29%20%285%29%20%286%29%20%286%29%20%289%29%20%282%29%20%2811%29.png)

After the goal finishes executing, run `git diff` \(or your VCS system's equivalent\) to see what changes were made, review, and commit them.

![Example of changes made to netflix conductor by the rewriteRun task](../.gitbook/assets/rewrite-fix-git-diff-output%20%281%29%20%281%29%20%283%29%20%283%29%20%283%29%20%281%29%20%282%29.png)

## The "dryRun" Task

Execute `gradle rewriteDryRun` to dry-run the active recipes and print which visitors would make changes to which files to the build log. This does not alter your source files on disk at all. This goal can be used to preview the changes that would be made by the active recipes.

![Listing of source files that would be changed if rewriteRun were run](../.gitbook/assets/rewrite-warn-gradle-output%20%283%29%20%283%29%20%283%29%20%281%29.png)

`rewriteDryRun` can be used as a "gate" in a continuous integration environment by failing the build if `rewriteDryRun` detects changes to be made and `failOnDryRunResults` is set to `true`:

```groovy
rewrite {
    // ...
    failOnDryRunResults = true
}
```

If desired, `rewriteDryRun` can be configured so that when `check` runs, `rewriteDryRun` does too:

```groovy
tasks.named("check").configure {
    dependsOn(tasks.named("rewriteDryRun"))
}
```

## The "Discover" Task

Execute `gradle rewriteDiscover` to list the recipes available on your classpath.

![](../.gitbook/assets/image%20%281%29.png)

## Links

* [Github project](https://github.com/openrewrite/rewrite-gradle-plugin)
* [Issue Tracker](https://github.com/openrewrite/rewrite-gradle-plugin/issues)
* [Gradle Plugin Portal Listing](https://plugins.gradle.org/plugin/org.openrewrite.rewrite)

