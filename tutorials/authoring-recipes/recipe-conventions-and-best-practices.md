---
description: Conventions to follow, pitfalls to avoid
---

# Recipe Conventions and Best Practices

[Recipes](../../v1beta/recipes.md) use [Visitors](../../v1beta/visitors.md) to operate on diverse and unexpected [ASTs](../../v1beta/abstract-syntax-trees.md). This document describes an assortment of conventions, best practices, and pitfalls to avoid to create reliable, scalable recipes.

### Do No Harm

If your Recipe cannot determine that a change is safe to make, such as when a type you're looking for is unavailable, it is always preferable to make no change than to make the wrong change. Relatedly, when making changes always strive to make the most minimal, least invasive version of that change. Keeping changes minimal makes for easy to review diffs and higher rates of pull request acceptance. A change which unnecessarily clobbers formatting or is otherwise overly broad will burden code reviewers and drastically reduce the rate at which they accept changes.&#x20;

{% hint style="success" %}
RewriteTest helps you to verify that your recipe does not make unnecessary changes by running your recipe in a loop. If you see your change being made many times it is likely your visitor fails to avoid making unnecessary changes.&#x20;
{% endhint %}

{% hint style="info" %}
When authoring your tests always remember to test that changes aren't made when they shouldn't be.
{% endhint %}

### Naming conventions

Recipe names, descriptions, and parameters should follow our [recipe naming conventions](https://github.com/openrewrite/rewrite/blob/main/doc/adr/0002-recipe-naming.md).&#x20;

### If it can be declarative, it should be declarative

If your Recipe exists only to aggregate other recipes together in a unit, it is preferable to include it as a [declarative YAML recipe](../../reference/yaml-format-reference.md) rather than as code.

### Recipes must be configurable with simple, JRE-provided types

Recipes may be configured in code, from yaml, or from a web interface. If your recipe is configured with complex types this becomes untenable and your recipe's interoperability and utility will be reduced. If the implementation of a visitor is simplified by using complex types, then it is the job of the recipe to assemble those more complex types out of the simple types it is configured with.

{% hint style="warning" %}
Recipe options which are configured with `String` parameters should generally treat the empty string and `null` similarly. Depending on the frontend which configures the recipe either value may be used to represent omitted configuration.
{% endhint %}

### Be deliberate about AST traversal

As the author of a visitor the traversal of the AST is in your hands. Calling`super.visitSomeAstElement()` is what causes the traversal of sub-elements of the current element to happen. So if you know that no traversal of sub-elements will be necessary, you can skip this call entirely to improve the performance of your recipe. Usually it is most convenient to call at the beginning of each visit method you implement.

### Use Applicability Tests

Most recipes are not universally applicable to every source file. Often you can know ahead of time that your recipe will not need to modify source files where a particular type is not present. The visitor returned from  `Recipe.getSingleSourceApplicableTest()` making any change to the AST is interpreted as an "affirmative" result that the Recipe is applicable to the AST. Use `Applicability.and()`, `Applicability.or()`, and `Applicability.not()` to create more complex applicability criteria from simple building blocks.&#x20;

Using applicability tests can simplify implementation of your recipe by separating the code which detects "should a change be made" from the code which enacts "making the change". This enhances readability, simplifying debugging and maintenance.

{% hint style="info" %}
Applicability tests are most worthwhile when they can cheaply prevent a visitor from running unnecessarily.
{% endhint %}

{% hint style="warning" %}
`Recipe.getApplicableTest()` returning an affirmative result for _any_ source file marks the recipe as applicable to _all_ source files. For most recipes `Recipe.getSingleSourceApplicableTest()` is the appropriate method to overload.
{% endhint %}

### Recipe and AST immutability

Recipes must have no mutable state. `Recipe.getVisitor()` must always return a brand new visitor instance. During recipe execution the same recipe may be invoked multiple times, possibly on sources it has seen before, so any mutable state is an opportunity for bugs. During test execution recipe execution is single threaded for simplicity, but outside of tests recipe execution is paralellized. Following this rule is essential for OpenRewrite to operate reliabliy and correctly.

{% hint style="warning" %}
All AST fields should be treated as immutable, even in certain circumstances where mutation is _technically_ possible it is always a bug for a recipe to mutate those fields.&#x20;
{% endhint %}

OpenRewrite detects that a visitor/recipe has made a change based on referential equality. Mutating an AST foils this detection, and can potentially cause incorrect diffs to be created.&#x20;

### Use ListUtils for collections manipulation

Since referential equality is so important for OpenRewrite to detect changes, typical collection creation and manipulation patterns like newing up your own collection or using Java streams are usually a mistake. Instead we provide the `ListUtils` class which provides referential-equality conscious data access and manipulation faculties which avoid unnecessary memory allocations.

### Nullability matters

Throughout our ASTs and other APIs we have been careful to use Java's nullability annotations to indicate whether a field is nullable or not. If a field is nullable then there _will_ be ASTs where that field is null. To operate correctly on the wildly diverse code which exists throughout the world Recipe/Visitors must decline to make changes when a field they need to make changes is null.

### Avoid constructing AST elements by hand

Even very simple pieces of code have complex AST representations which are tedious and error-prone to construct by hand. With your visitor, prefer faculties like [JavaTemplate](../../v1beta/javatemplate.md) to turn code snippets into AST elements. In data formats like XML or Json it is usually most convenient to use the format's parser to turn a snippet of text into usable AST elements.
