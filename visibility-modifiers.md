
地址：http://kotlinlang.org/docs/reference/visibility-modifiers.html<br />
日期：2017-07-11<br />
译者：Linky<br />

## 可见性修饰符 

类、对象、接口、构造器、函数、属性和他们的 `setters` 方法都可以用 可见性修饰符 修饰（Getters 通常
都和属性的可见性相同）。Kotlin 中有四个可见性修饰符：`private`、`protected`、`internal` 和 `public`。
如果没有显式添加，则默认为 `public`。

## 包

函数、属性 和 类、对象以及接口都可以在 顶层 声明，例如，直接在包中声明

```kotlin
  package foo

  fun baz() {}
  class Bar {}
```

—— 如果不指定可见性，默认是 public，也就是说你的声明可以在任何地方可见；
—— 如果用 private 修饰一个属性，那么该属性只能在包含该声明的文件内部可见；
—— 如果用 internal 修饰一个属性，那么该属性在相同的 module 中可见；
—— 在 顶层声明中，不能用 protected 修饰；

例如：

```kotlin
  package foo

  private fun foo() {}	// visible inside example.kt 

  public var bar: Int = 5  // property is visible everywhere 
    private set		   // setter is visible only in example.kt 

  internal val baz = 6	   // visible inside the same module 
```

## 类 和 接口 

对于声明在 类 中的成员

—— private 意味着 只在类内可见 
—— protected 意味着 类内 + 子类中可见 
—— internal 在 module 内部的任意 client，如果可访问声明的 类，那么也可以访问该类的 internal 成员
—— public 任意 client，如果可访问声明的类，那么也可见它的 public 成员 

注意：对于 Java 用户来说，外部类不能访问 Kotlin 内部类的私有成员。

如果你继承了一个 protected 成员，同时没有指定它的可见性，那么默认重载的成员也有 protected 的可见性

```kotlin
  open class Outer {
    private val a = 1
    protected open val b = 2
    internal val c = 3
    val d = 4	// 默认为 public 

    protected class Nested {
      public val e: Int = 5
    }
  }

  class Subclass : Outer() {
    // a 不可见
    // b，c 和 d 是可见的
    // Nested类 和 e 是可见的

    override val b = 5	// 'b' is protected 
  }

  class Unrelated(o: Outer) {
    // o.a, o.b 是不可见的
    // o.c 和 o.d 是可见的（相同的 module）
    // Outer.Nested 不可见，Nested::e 也不可见 
  }

```

## 构造器 

为了声明一个类的基本构造器的可见性，使用下面的语法：（需要显式地使用 constructor 关键字）

```kotlin
  class C private constructor(a: Int) { ... }
```

在这里，构造器是 private 的。默认情况下，所有的构造器都是 public 的，
internal 声明的 class 只在相同的 module 中可见。

###局部声明

局部变量，函数和类不能有 可见性修饰符

## 模块

internal 可见性修饰符意味着相同 module 中的成员可见。具体来说，
一个 module 就是一组 Kotlin 文件编译在了一起。

—— 一个 Intellij IDEA 模块；
—— 一个 Maven 项目；
—— 一个 Gradle 文件集合；
—— 一组被 Ant 任务编译的文件；
