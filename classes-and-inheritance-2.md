地址：http://kotlinlang.org/docs/reference/classes.html<br />
日期：2017年 06月 28日 星期二<br />
译者：Linky<br />

# 类 和 继承 (二) 

## 重载属性 

重载属性和重载方法相似：在父类中声明的属性如果在子类中再次声明，必须加上 `override` 前缀，
而且他们必须有一个兼容的类型。每个声明的属性可以通过一个带初始化器的属性或者通过一个属性的
getter 方法来重载。

```kotlin
  open class Foo {
    open val x: Int get { ... }
  }

  class Bar1 : Foo() {
    override val x: Int = ...
  }
```

你可以用一个 `var` 类型的属性重载 `val` 类型的属性，但是不能反过来。
`var` 类型重载 `val` 类型是允许的，因为 `val` 类型默认有一个 getter 方法，
而重载它的 `var` 则额外声明了一个 setter 方法

注意到，我们可以使用 `override` 关键字作为 主要构造器 中的属性声明的一部分。

```kotlin

  interface Foo {
    val count: Int
  }

  class Bar1(override val count: Int) : Foo 

  class Bar2 : Foo {
    override var count: Int = 0
  }
```

## 重载规则 

在 kotlin 中，继承需要遵循以下规则：如果一个类从它的多个直接父类中继承了 
相同的成员，那么它必须重载这个成员并且提供自己的一套实现。为了表示使用了
父类，我们使用 `super` 和尖括号组合父类表示，例如：`super<Base>` 


```kotlin
  open class A {
    open fun f() { print("A") }
    fun a() { print("a") }
  }

  interface B {
    fun f() {} // 接口中的 成员 是 默认 open 的 
    fun b() {}
  }

  class C() : A(), B {
    // 编译器要求 f() 函数必须被重写，
    override fun f() {
      super<A>.f()  // 调用到 A.f()
      super<B>.f()  // 调用到 B.f() 
    }
  }
```

同时继承 `A` 和 `B` 是没问题的，而且方法 `a()` 和 `b()` 由于只有一种实现，
所以 C 直接继承它们也没问题。但是对于 `f()` 方法，由于 `A` 和 `B` 都有一套
实现，所以 `C` 必须提供一套自己的实现，才能消除含糊不清。

## 抽象类

类和成员可以用 `abstract` 关键字修饰。我们不用使用 `open` 来修饰一个类或者成员，
毕竟这不言而喻。

我们可以在一个抽象类中，重载一个非抽象类的 open 成员：


```kotlin
  open class Base {
    open fun f() {}
  }

  abstract class Derived : Base() {
    override abstract fun f()
  }
```

## 同伴对象 

在 kotlin 中，没有像 Java 或者 C# 那样的 static 方法，而是使用包级别的函数。

如果你需要写一个不用 实例化对象 但是需要访问 类内部的方法（例如：一个工厂方法），
你可以将这个函数作为类内部的 [对象声明](http://kotlinlang.org/docs/reference/object-declarations.html)的成员。

更进一步，如果你在类内部声明了一个 [companion 对象](http://kotlinlang.org/docs/reference/object-declarations.html#companion-objects)，你就能够像在 Java 或者 C# 中
使用 static 方法一样调用这个成员。























