# Use `Set.of(..)` in Java 9 or higher

** org.openrewrite.java.migrate.guava.NoGuavaImmutableSetOf**
_Replaces `ImmutableSet.of(..)` if the returned type is immediately down-cast.
  Java 9 introduced `List#of(..)`, `Map#of(..)`, `Set#of(..)` which is similar to `ImmutableList#of(..)`, `ImmutableMap#of(..)`, `ImmutableSet#of(..)`, but has a subtle difference.
  As per the Java 9 documentation, [`Set.of` provides an unspecified iteration order on the set of elements and is subject to change](https://docs.oracle.com/javase/9/docs/api/java/util/Set.html), whereas [Guava `ImmutableSet` preserves the order from construction time](https://github.com/google/guava/wiki/ImmutableCollectionsExplained#how).
  This is worth pointing out in case your usage calls for iteration order being important._

### Tags

* RSPEC-4738

## Source

[Github](https://github.com/openrewrite/rewrite-migrate-java), [Issue Tracker](https://github.com/openrewrite/rewrite-migrate-java/issues), [Maven Central](https://search.maven.org/artifact/org.openrewrite.recipe/rewrite-migrate-java/1.13.0/jar)

* groupId: org.openrewrite.recipe
* artifactId: rewrite-migrate-java
* version: 1.13.0


## Usage

This recipe has no required configuration options and can be activated directly after taking a dependency on org.openrewrite.recipe:rewrite-migrate-java:1.13.0 in your build file:

{% tabs %}
{% tab title="Gradle" %}
{% code title="build.gradle" %}
```groovy
plugins {
    id("org.openrewrite.rewrite") version("5.31.0")
}

rewrite {
    activeRecipe("org.openrewrite.java.migrate.guava.NoGuavaImmutableSetOf")
}

repositories {
    mavenCentral()
}

dependencies {
    rewrite("org.openrewrite.recipe:rewrite-migrate-java:1.13.0")
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
        <version>4.36.0</version>
        <configuration>
          <activeRecipes>
            <recipe>org.openrewrite.java.migrate.guava.NoGuavaImmutableSetOf</recipe>
          </activeRecipes>
        </configuration>
        <dependencies>
          <dependency>
            <groupId>org.openrewrite.recipe</groupId>
            <artifactId>rewrite-migrate-java</artifactId>
            <version>1.13.0</version>
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
```shell
mvn org.openrewrite.maven:rewrite-maven-plugin:4.36.0:run \
  -Drewrite.recipeArtifactCoordinates=org.openrewrite.recipe:rewrite-migrate-java:1.13.0 \
  -DactiveRecipes=org.openrewrite.java.migrate.guava.NoGuavaImmutableSetOf
```
{% endcode %}
{% endtab %}
{% endtabs %}

Recipes can also be activated directly from the command line by adding the argument `-Drewrite.activeRecipes=org.openrewrite.java.migrate.guava.NoGuavaImmutableSetOf`
