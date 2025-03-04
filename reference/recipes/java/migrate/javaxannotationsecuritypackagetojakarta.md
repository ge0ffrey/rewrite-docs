# Migrate deprecated `javax.annotation.security` packages to `jakarta.annotation.security`

** org.openrewrite.java.migrate.JavaxAnnotationSecurityPackageToJakarta**
_Change type of classes in the `javax.annotation.security` package to jakarta._

### Tags

* javax
* batch
* jakarta

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
    activeRecipe("org.openrewrite.java.migrate.JavaxAnnotationSecurityPackageToJakarta")
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
            <recipe>org.openrewrite.java.migrate.JavaxAnnotationSecurityPackageToJakarta</recipe>
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
  -DactiveRecipes=org.openrewrite.java.migrate.JavaxAnnotationSecurityPackageToJakarta
```
{% endcode %}
{% endtab %}
{% endtabs %}

Recipes can also be activated directly from the command line by adding the argument `-Drewrite.activeRecipes=org.openrewrite.java.migrate.JavaxAnnotationSecurityPackageToJakarta`

## Definition

{% tabs %}
{% tab title="Recipe List" %}
* [Change type](../../java/changetype.md)
  * oldFullyQualifiedTypeName: `javax.annotation.security.DeclareRoles`
  * newFullyQualifiedTypeName: `jakarta.annotation.security.DeclareRoles`
* [Change type](../../java/changetype.md)
  * oldFullyQualifiedTypeName: `javax.annotation.security.DenyAll`
  * newFullyQualifiedTypeName: `jakarta.annotation.security.DenyAll`
* [Change type](../../java/changetype.md)
  * oldFullyQualifiedTypeName: `javax.annotation.security.PermitAll`
  * newFullyQualifiedTypeName: `jakarta.annotation.security.PermitAll`
* [Change type](../../java/changetype.md)
  * oldFullyQualifiedTypeName: `javax.annotation.security.RolesAllowed`
  * newFullyQualifiedTypeName: `jakarta.annotation.security.RolesAllowed`
* [Change type](../../java/changetype.md)
  * oldFullyQualifiedTypeName: `javax.annotation.security.RunAs`
  * newFullyQualifiedTypeName: `jakarta.annotation.security.RunAs`

{% endtab %}

{% tab title="Yaml Recipe List" %}
```yaml
---
type: specs.openrewrite.org/v1beta/recipe
name: org.openrewrite.java.migrate.JavaxAnnotationSecurityPackageToJakarta
displayName: Migrate deprecated `javax.annotation.security` packages to `jakarta.annotation.security`
description: Change type of classes in the `javax.annotation.security` package to jakarta.
tags:
  - javax
  - batch
  - jakarta
recipeList:
  - org.openrewrite.java.ChangeType:
      oldFullyQualifiedTypeName: javax.annotation.security.DeclareRoles
      newFullyQualifiedTypeName: jakarta.annotation.security.DeclareRoles
  - org.openrewrite.java.ChangeType:
      oldFullyQualifiedTypeName: javax.annotation.security.DenyAll
      newFullyQualifiedTypeName: jakarta.annotation.security.DenyAll
  - org.openrewrite.java.ChangeType:
      oldFullyQualifiedTypeName: javax.annotation.security.PermitAll
      newFullyQualifiedTypeName: jakarta.annotation.security.PermitAll
  - org.openrewrite.java.ChangeType:
      oldFullyQualifiedTypeName: javax.annotation.security.RolesAllowed
      newFullyQualifiedTypeName: jakarta.annotation.security.RolesAllowed
  - org.openrewrite.java.ChangeType:
      oldFullyQualifiedTypeName: javax.annotation.security.RunAs
      newFullyQualifiedTypeName: jakarta.annotation.security.RunAs

```
{% endtab %}
{% endtabs %}
