
地址：http://kotlinlang.org/docs/reference/properties.html<br />
日期：Fri Jun 30 2017<br />
译者：Linky<br />

## 属性和域

  类可以声明属性，可变化的属性，使用 `var` 关键字声明，只读的属性，使用 `val` 关键字

```kotlin
  class Address {
    var name: String = ...
    var street: String = ...
    var city: String = ...
    var state: String = ...
    var zip: String = ... 
  }
```

使用时，我们只需要使用 变量名 来引用它即可，就像在 Java 中的一样

```kotlin
  fun copyAddress(address: Address): Address {
    val result = Address()
    result.name = address.name
    result.street = address.street
    // ...
    return result
  }
```

### Get 函数和 Set 函数

声明一个属性的完整语法如下：

```kotlin
  var <属性名称>[: <属性类型>] [= <属性初始化器>]
  [<getter>]
  [<setter>]
```

属性初始化器、getter 和 setter 是可选的。如果可以从  属性初始化器 推断出它的类型的话、或者从 getter 方法的返回值可以看出来的话，那么属性类型也可以忽略，就像下面这样：

```kotlin
   var initialized = 1 // 这个 属性有 Int 类型，默认 getter 和 setter 方法 
```

只读属性的声明和可变属性的声明有两点不同：1、只读属性以 `val` 开头；2、没有 setter 方法：

```kotlin
  val simple: Int      // Int 类型，一个默认的 getter 方法，必须在构造器在哦和那个初始化
  val interredType = 1 // 类型为 Int，还有一个默认的 getter 方法
```

>* *译者按：Kotlin 中的属性也有类型的概念，只是如果 属性的类型可以从其他地方推断出来时，可以不显式得写出来而已*

我们可以自定义一个 属性访问器，跟普通的函数一样：

```kotlin
  val isEmpty: Boolean
    get() = this.size == 0
```

一个自定义的 setter 函数看起来像这样：
```kotlin
  var stringRepresentation: String
    get() = this.toString()
    set(value) {
      setDataFromString(value) // 解析 string，然后赋值给其他属性 
    }
```

按照惯例，setter 函数的参数名一般为 `value`，不过你也可以选择其他名称。

从 Kotlin1.1 开始，如果可以从 属性的 getter 函数中推断出属性的类型，可以忽略属性的类型：


```kotlin
  val isEmpty get() = this.size == 0 // Boolean 类型 
```

如果你需要改变访问器的可见性或者给它加个注解，但是不改变默认实现，你可以只声明访问器而不改变它的实现：

```kotlin

  var setterVisibility: String = "abc"
    private set // setter 是 private 的，并且有默认的实现

  var setterWithAnnotation: Any? = null
    @Inject set // 用 Inject 给 setter 添加注解 
```

## 向后域

Kotlin 中，类不能有 域。然而，有时候在使用自定义访问器时，需要有一个 向后域。为了这个目的，
Kotlin 提供了一个使用 `field` 标志符的自动的 向后域：


```kotlin
  var counter = 0
    set(value) {
      if (value >= 0) field = value
    }
```

`field` 只能在属性的访问器中使用。

如果类属性至少使用了一个默认的访问器，那么该属性的 向后域 会自动产生。
如果类属性的自定义的访问器使用了 `field` 标志符，那么该属性的 向后域 也会自动产生。

例如，在下面这种情况下，将没有 向后域：

```kotlin
  val isEmpty: Boolean
    get() = this.size == 0 
```

### 向后属性 

如果你想做一些不符合这种 隐式向后域 模式的事情，可以考虑使用 向后属性：

```kotlin
  private var _table: Map<String, Int>? = null
  public val table: Map<String, Int>
    get() {
      if (_table == null) {
        _table = HashMap()
      }
      return _table ?: throw AssertionError("Set to null by another thread")
    }
```

使用默认的 setters 和 getters 对私有属性进行访问都是最优化的，因为这样没有引入额外的函数调用开销。


### 编译时常量 

如果一个属性的值可以在编译时得知，那么可以使用 `const` 修饰符将其标记为 **运行时常量** 
这个属性需要满足以下要求：

—— 最外层 或者 是一个对象的成员
—— 用 String 类型 或者 原生类型的值初始化
—— 没有自定义 `getter` 方法

这个属性可以在注解中使用：

```kotlin
  const val SUBSYSTEM_DEPRECATED: String = "This subsystem is deprecated"
  @Deprecated(SUBSYSTEM_DEPRECATED) fun foo() { ... }
```

### 后期初始化 属性

一般情况下，非空类型的属性都必须在构造器中初始化。但是很多时候这样不太方便。例如要通过依赖注入来初始化，
或者在单元测试的 setup 方法中初始化。在这种情况下，你不能在构造器中提供一个非空初始化器，但是你仍然想
在一个类体中避免空值检查。为了处理这种情况，你可以用 `lateinit` 修饰符来标识属性。


```kotlin
  public class MyTest {
    lateinit var subject: TestSubject

    @SetUp fun setup() {
      subject = TestSubject()
    }

    @Test fun test() {
      subject.method() 
    }
  }
```

这个修饰符只能用在类体中的 var 属性，不能用在 主要构造器 中，而且该属性没有自定义的 getter 或者 setter。
属性的类型必须是非空的，而且不能为原生类型。

如果一个 `lateinit` 属性在初始化之前就被访问，将抛出一个异常。

### 重载属性

详情查看[Overriding Properties](http://kotlinlang.org/docs/reference/classes.html#overriding-properties)

