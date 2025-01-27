---
title: Sound null safety
title: 健全的空安全
description: Information about Dart's null safety feature
description: Dart 空安全的有关内容
---

The Dart language now supports sound null safety!

Dart 语言已支持健全的空安全机制！

When you opt into null safety,
types in your code are non-nullable by default, meaning that
variables can’t contain `null` _unless you say they can._
With null safety, your **runtime** null-dereference errors
turn into **edit-time** analysis errors.

当你选择使用空安全时，代码中的类型将默认是非空的，
意味着 **除非你声明它们可空**，它们的值都不能为空。
有了空安全，原本处于你的 **运行时** 的空值引用错误
将变为 **编辑时** 的分析错误。

With null safety,
all of the variables in the following code are non-nullable:

有了空安全，下面代码中所有的变量都是非空的：

```dart
// In null-safe Dart, none of these can ever be null.
var i = 42; // Inferred to be an int.
String name = getFileName();
final b = Foo();
```

<a id="creating-variables"></a>
To indicate that a variable might have the value `null`,
just add `?` to its type declaration:

若你想让变量可以为 `null`，只需要在类型声明后加上 `?`。

```dart
int? aNullableInt = null;
```

You can
[use null safety](#enable-null-safety) in your normal development environment,
[migrate existing code][migration guide] to use null safety,
or try null safety in [DartPad]({{site.dartpad}}).

你可以在你的普通开发环境中 [使用空安全](#enable-null-safety)，
也建议 [迁移你项目中的代码][migration guide] 至空安全，
或者通过 [支持空安全的 DartPad]({{site.dartpad}}) 进行空安全特性实验。

For an interactive, example-driven introduction to null safety language features,
see the [null safety codelab][Null safety codelab].
For an in-depth discussion, see
[Understanding null safety](/null-safety/understanding-null-safety).

若你想通过一个交互示例快速了解空安全，可以查看 [空安全 Codelab][Null safety codelab]。
更深入的探讨，可以阅读 [深入理解空安全](/null-safety/understanding-null-safety)。

## Null safety principles

## 空安全的原则

Dart null safety support is based on the following three core design principles:

Dart 的空安全支持基于以下三条核心原则：

* **Non-nullable by default**. Unless you explicitly tell Dart that a variable
   can be null, it's considered non-nullable. This default was chosen
   after research found that non-null was by far the most common choice in APIs.

   **默认不可空**。除非你将变量显式声明为可空，否则它一定是非空的类型。
   我们在研究后发现，非空是目前的 API 中最常见的选择，所以选择了非空作为默认值。

* **Incrementally adoptable**. You choose _what_ to migrate to null safety, and _when_.
  You can migrate incrementally, mixing null-safe and
  non-null-safe code in the same project. We provide tools to help you
  with the migration.

  **渐进迁移**。你可以自由地选择何时进行迁移，多少代码会进行迁移。
  你可以使用混合模式的空安全，在一个项目中同时使用空安全和非空安全的代码。
  我们也提供了帮助你进行迁移的工具。

* **Fully sound**. Dart’s null safety is sound, which enables compiler optimizations.
  If the type system determines that something isn’t null, then that thing can _never_ be
  null. Once you migrate your whole project
  and its dependencies to null safety, 
  you reap the full benefits of soundness—not only 
  fewer bugs, but smaller binaries and faster execution.

  **完全可靠**。Dart 的空安全是非常可靠的，意味着编译期间包含了很多优化。
  如果类型系统推断出某个变量不为空，那么它 **永远** 不为空。
  当你将整个项目和其依赖完全迁移至空安全后，
  你会享有健全性带来的所有优势&mdash;&mdash;
  更少的 BUG、更小的二进制文件以及更快的执行速度。

## Enabling null safety {#enable-null-safety}

## 启用空安全 {#enable-null-safety}

Sound null safety is available in Dart 2.12 and Flutter 2.

健全的空安全已在 Dart 2.12 和 Flutter 2 中可用。

### Migrating an existing package or app {#migrate}

### 迁移已有 package 或应用 {#migrate}

For instructions on how to migrate your code to null safety,
see the [migration guide][].

若你需要代码迁移的指导，请查看 [迁移至空安全][migration guide]。

{{site.alert.version-note}}

  Before Dart 2.13, the templates used by the [`dart create`][] command
  and IDEs aren't null safe, so you need to migrate the code they create.
  For example:

  使用 Dart 2.13 以前版本的 [`dart create`][] 命令或 IDE 创建的模板，
  尚未迁移至空安全。在创建后你还需要对它们进行迁移。举个例子：

  ```terminal
  $ dart create -t console my_cli
  $ cd my_cli
  $ dart migrate --apply-changes
  ```
{{site.alert.end}}

### Behind the scenes: SDK constraints {#constraints}

### 幕后工作：SDK 限制 {#constraints}

To make Dart treat your code as null safe,
the [SDK constraints](/tools/pub/pubspec#sdk-constraints)
must require a [language version][] that has null safety support.
For example, your `pubspec.yaml` file might have the following constraints:

将 [SDK 版本约束](/tools/pub/pubspec#sdk-constraints)
设定为一个支持空安全的 SDK 版本。
例如，你的 `pubspec.yaml` 可以设置为如下的限制：

```yaml
environment:
  sdk: '>=2.12.0 <3.0.0'
```

[language version]: /guides/language/evolution#language-versioning

## Where to learn more

## 学习更多

For more information about null safety, see the following resources:

想了解关于空安全的更多内容，可查看以下的资源内容：

* [Null safety codelab][]

  [空安全 Codelab][Null safety codelab]

* [Understanding null safety][]

  [深入理解空安全][Understanding null safety]

* [Migration guide for existing code][migration guide]

  [现有代码的迁移指南][migration guide]

* [Null safety FAQ][]

  [空安全常见问题和解答][Null safety FAQ]
  
* [DartPad with null safety]({{site.dartpad}})

  [支持空声明的 DartPad (DartPad with null safety)]({{site.dartpad}})

* [Null safety sample code][calculate_lix]

  [空安全示例代码 (Null safety sample code)][calculate_lix]

* [Null safety tracking issue][110]

  [空安全的问题跟踪 (Null safety tracking issue)][110]

* [Dart blog][]

  [Dart 官方博客][Dart blog]

[110]: https://github.com/dart-lang/language/issues/110
[calculate_lix]: https://github.com/dart-lang/samples/tree/master/null_safety/calculate_lix
[`dart create`]: /tools/dart-create
[Dart blog]: https://medium.com/dartlang
[migration guide]: /null-safety/migration-guide
[Null safety FAQ]: /null-safety/faq
[Null safety codelab]: /codelabs/null-safety
[Understanding null safety]: /null-safety/understanding-null-safety

