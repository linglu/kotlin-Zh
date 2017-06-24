
地址：http://kotlinlang.org/docs/reference/packages.html<br />
日期：2017年 06月 24日 星期六<br />
译者：Linky<br />

## Packages

一个源文件始于一个包声明：

```kotlin
  package foo.bar
  
  fun baz() {}
  class Goo {}
```

源文件中的所有内容（例如类和方法）都被包含在包声明中。所以在上面的例子中，
`baz()` 的完整形式是 `foo.bar.baz`，`Goo` 的完整形式是 `foo.bar.Goo`。

如果没有声明包，那么里面的内容将属于 default 包，不用加包名路径前缀。


## 默认导入的包

下面这些包是默认导入到每个 Kotlin 文件中的：

—— kotlin.*
—— kotlin.annotation.*
—— kotlin.collections.*
—— kotlin.comparisons.*( 从 1.1 开始)
—— kotlin.io.*
—— kotlin.ranges.*
—— Kotlin.sequences.*
—— kotlin.text.*

下面的包是否导入取决于目标平台：

—— JVM:

  —— java.lang.*
  —— kotlin.jvm.*

—— JS:

  —— kotlin.js.*

## 导入 

  除了默认导入的包，每个文件也许包含它自己的导入指令。导入的语法可以在[这里](http://kotlinlang.org/docs/reference/grammar.html#import)查看

我们可以导入单个名称，例如：

```kotlin
  import foo.Bar
```

或者导入某个域下的所有内容（包、类、对象等）：

```kotlin
import foo.* // foo 下的所有都可以访问到
```

如果存在命名冲突，可以通过 as 关键字重命名本地冲突实体来消除歧义

```kotlin
  import foo.Bar  // Bar 是可以访问到的 
  import bar.Bar as bBar // bBar 表示 bar.Bar 
```


`import` 不仅可以导入类，也可以导入其他声明：

—— 最外层函数和属性；
—— 在 [object declarations](http://kotlinlang.org/docs/reference/object-declarations.html#object-declarations)中声明的函数和属性；
—— [enum constants](http://kotlinlang.org/docs/reference/enum-classes.html)


不像 java，Kotlin 没有 `import static` 语法，所有导入都要
通过使用 `import` 关键字。


## 最上层声明的可见性

  如果一个声明用 `private` 标记了，那么这个声明仅对该文件
可见，详情查看[Visibility Modifiers](kotlinlang.org/docs/reference/visibility-modifiers.html)






































