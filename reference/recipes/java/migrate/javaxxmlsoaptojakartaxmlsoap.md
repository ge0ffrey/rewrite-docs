# Migrate deprecated `javax.soap` packages to `jakarta.soap`

** org.openrewrite.java.migrate.JavaxXmlSoapToJakartaXmlSoap**
_Java EE has been rebranded to Jakarta EE, necessitating a package relocation._

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
    activeRecipe("org.openrewrite.java.migrate.JavaxXmlSoapToJakartaXmlSoap")
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
            <recipe>org.openrewrite.java.migrate.JavaxXmlSoapToJakartaXmlSoap</recipe>
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
  -DactiveRecipes=org.openrewrite.java.migrate.JavaxXmlSoapToJakartaXmlSoap
```
{% endcode %}
{% endtab %}
{% endtabs %}

Recipes can also be activated directly from the command line by adding the argument `-Drewrite.activeRecipes=org.openrewrite.java.migrate.JavaxXmlSoapToJakartaXmlSoap`

## Definition

{% tabs %}
{% tab title="Recipe List" %}
* [Add Maven dependency](../../maven/adddependency.md)
  * groupId: `jakarta.xml.soap`
  * artifactId: `jakarta.xml.soap-api`
  * version: `2.x`
  * onlyIfUsing: `javax.xml.soap.*`
* [Upgrade Maven dependency version](../../maven/upgradedependencyversion.md)
  * groupId: `jakarta.xml.soap`
  * artifactId: `jakarta.xml.soap-api`
  * newVersion: `2.x`
* [Rename package name](../../java/changepackage.md)
  * oldPackageName: `javax.xml.soap`
  * newPackageName: `jakarta.xml.soap`
  * recursive: `true`
* [Remove Maven dependency](../../maven/removedependency.md)
  * groupId: `javax.xml.soap`
  * artifactId: `javax.xml.soap-api`

{% endtab %}

{% tab title="Yaml Recipe List" %}
```yaml
---
type: specs.openrewrite.org/v1beta/recipe
name: org.openrewrite.java.migrate.JavaxXmlSoapToJakartaXmlSoap
displayName: Migrate deprecated `javax.soap` packages to `jakarta.soap`
description: Java EE has been rebranded to Jakarta EE, necessitating a package relocation.
recipeList:
  - org.openrewrite.maven.AddDependency:
      groupId: jakarta.xml.soap
      artifactId: jakarta.xml.soap-api
      version: 2.x
      onlyIfUsing: javax.xml.soap.*
  - org.openrewrite.maven.UpgradeDependencyVersion:
      groupId: jakarta.xml.soap
      artifactId: jakarta.xml.soap-api
      newVersion: 2.x
  - org.openrewrite.java.ChangePackage:
      oldPackageName: javax.xml.soap
      newPackageName: jakarta.xml.soap
      recursive: true
  - org.openrewrite.maven.RemoveDependency:
      groupId: javax.xml.soap
      artifactId: javax.xml.soap-api

```
{% endtab %}
{% endtabs %}
