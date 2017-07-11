地址：http://kotlinlang.org/docs/reference/interfaces.html<br />
日期：2017年 07月 11日 星期二<br />
译者：Linky<br />


## 接口

Kotlin 中的接口和 Java 8 中的很像，他们可以包含抽象方法的声明以及实现。接口和抽象类的区别在于，
接口不能存储状态。他们可以有属性，但是这些属性应该是抽象的，或者提供访问器实现。

一个接口使用关键字 `interface` 来定义

```kotlin
  interface MyInterface {
    fun bar()
    fun foo() {
      // optional body
    }
  }
```

## 实现接口

一个类或对象可以实现一个或更多个接口


```kotlin
  class Child : MyInterface {
    override fun bar() {
        // body
    }
  }
```

## 接口中的属性 

接口中的属性，要么是抽象的，要么提供一个构造器实现。接口中的属性不能有向后域，
所以接口中声明的访问器不能引用他们。

```kotlin
  interface MyInterface {
    val prop: Int // abstract

    val propertyWithImplementation: String
      get() = "foo"

    fun foo() {
      print(prop)
    }
  }

  class Child : MyInterface {
    override val prop: Int = 29
  }
```

## 处理重载冲突

当我们继承了多个父类，很有可能多个父类有相同的方法名称，例如：

```kotlin
  interface A {
    fun foo() { print("A") }
    fun bar()
  }

  interface B {
    fun foo() { print("B") }
    fun bar() { print("bar") }
  }

  class C : A {
    override fun bar() { print("bar") }
  }

  class D : A, B {
    override fun foo() {
      super<A>.foo()
      super<B>.foo()
    }

    override fun bar() {
      super<B>.bar()
    }
  }

```
接口 A 和 B 都声明了方法 foo() 和 bar()。A 和 B 都实现了 foo()，但是只有 B 实现了 bar()。
现在如果我们从 A 继承一个具体类 C，很明显，我们必须重载 bar() 并且提供一个实现。

然而，如果我们同时从 A 和 B 中产生了一个 D，我们需要重载从多个接口中继承来的方法，并且提供具体的实现。
这条规则适用于只有一个实现的 bar()，也适用于有多个实现的 foo()。
