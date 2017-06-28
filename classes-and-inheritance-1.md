地址：http://kotlinlang.org/docs/reference/classes.html<br />
日期：2017年 06月 24日 星期六<br />
译者：Linky<br />

# 类 和 继承 (一) 

## 类 

在 Kotlin 中，类 使用关键字 class 声明：

```kotlin
  class Invoice {
  }
```

类的声明由类名，类头（确定它的类型参数、私有构造函数等）和类体组成，类头 和 类体 是可选的。
如果一个类没有体，花括号可以省略。

```kotlin
  class Empty
```

### 构造函数 

Kotlin 中，一个类可以有一个主要构造器和一个或多个次要构造器。主要构造器是类头的一部分，
跟在类名之后，类型参数 是可选的。

```kotlin
  class Person constructor(firstName: String) {
  }
```

如果主要构造器没有任何注解或者可见的修饰符，关键字 `constructor` 可以省略

```kotlin
class Person(firstName: String) {
}
```

注意：构造函数里面不能包含任何代码，初始化代码可以放在初始块中，初始块以 `init` 关键字为前缀：

```kotlin
  class Customer(name: String) {
    init {
      logger.info("Customer initialized with value ${name}")
    }
  }
```

注意到，主要构造器的参数可以在 初始块中引用，它们也可以在属性初始化声明中使用：

```kotlin
  class Customer(name: String) {
    val customerKey = name.toUpperCase()
  }
```

声明和初始化属性，Kotlin 有一个更简单的语法：(PS : 多个了 val 或者 var 关键字)

```kotlin
  class Person(val firstName: String, val lastName: String, var age: Int) {
    // ... 
  }
```

如果构造函数有注解或者可见的修饰符，那么 `constructor` 关键字是需要的，修饰符写在它
的前面：

```kotlin
  class Customer public @Inject constructor(name: String) { ... }
```

更多详情查看[Visibility Modifiers](http://kotlinlang.org/docs/reference/visibility-modifiers.html#constructors)

### 次要构造器 

一个类也可以声明次要构造器，以 constructor 为前缀：

```kotlin
  class Person {
    constructor(parent: Person) {
      parent.children.add(this)
    }
  }
```

如果一个类有主要构造器，那么每个次要构造器都需要委托主要构造器（直接或间接）。
委托另一个构造器可以使用 this 关键字：

```kotlin
  class Person(val name: String) {
    constructor(name: String, parent: Person) : this(name) {
      parent.children.add(this)
    }
  }
```

如果一个非抽象类没有声明任何构造器（主要或次要），默认会有一个不带参数的主要构造器，
可见性为 public。如果你不想你的类有一个 public 的构造器，则需要你手动声明：

```kotlin
class DontCreateMe private constructor () {
}
```


注意：在 JVM 中，如果 主要构造器 的所有参数都有默认值，编译器将会构造一个额外的没有参数的
构造器，并且使用默认值。这个特性使得 Kotlin 在使用 jackson 或者 JPA 等通过无参构造器实例化
类对象的第三方库时变得非常容易。

```kotlin
  class Customer(val customerName: String = "")
```

### 创建类对象

创建类对象时，直接调用类的构造器，就像它是一个标准的函数一样：

```kotlin
val invoice = Invoice()
val customer = Customer("Joe Smith")
```

注意到，Kotlin 没有使用 `new` 关键字

创建嵌套的实例，内部和匿名内部类，可以查看[Nested classes](http://kotlinlang.org/docs/reference/nested-classes.html)

### 类成员

类可以包含

—— 构造器 和 初始化块
—— [函数](http://kotlinlang.org/docs/reference/functions.html)
—— [属性](http://kotlinlang.org/docs/reference/properties.html)
—— [嵌套或者内部类](http://kotlinlang.org/docs/reference/nested-classes.html)
—— [对象声明](http://kotlinlang.org/docs/reference/object-declarations.html)

## 继承 

Kotlin 中的所有类都有一个共同的父类 `Any` 

```kotlin
  class Example // 隐式继承 Any 
```

`Any` 不是 `java.lang.Object`，具体来说，它只有 `equals()`, `hashCode()` 和 `toString()` 方法，
而没有其他任何成员。你可以查看 [Java interoperability](http://kotlinlang.org/docs/reference/java-interop.html#object-methods)获得更多细节。

为了显式地声明一个父类，我们在类头中加个冒号和父类型即可：

```kotlin
  open class Base(p: Int)
  class Derived(p: Int) : Base(p)
```

如果类有一个主要构造器，基类必须在那里初始化。

如果类没有主要构造器，那么每个次要构造器必须初始化基类，使用 `super` 关键字，或者委托
其他构造器这么做。注意到，这种情况下，不同的次要构造器可以调用不同的基类构造器。

```kotlin
  class MyView : View {
    constructor(ctx: Context) : super(ctx)
    constructor(ctx: Context, attrs: AttributeSet) : super(ctx, attrs)
  }
```

`open` 注解和 java 中的 `final` 相反：它允许其他类从这个类继承。默认情况下，Kotlin 
中的所有类都是 `final` 的，这主要是借鉴了 [Effective java](http://www.oracle.com/technetwork/java/effectivejava-136174.html)17 章的内容：要么为继承设计好，要么禁止它

### 重载方法

就像上面说的，我们争取在 Kotlin 中一切都是那么清晰，不像 java， Kotlin 要求对
可重写的成员进行明确的注解（使用 *open*）：

```kotlin
  open class Base {
    open fun v() {}
    fun nv() {}
  }

  class Derived() : Base() {
    override fun v() {}
  }
```

`Derived.v()` 需要用 `override` 注解，否则编译器会报错。如果父类中的方法 `Base.nv()`
没有声明 `open` 注解，在子类中定义相同的方法，无论是否有 `override` 都是不允许的。
在一个 `final` 类中（没有 `open` 注解的类），用 open 修饰成员是不被允许的。

一个用 `override` 标记的成员本身是 open 的。在子类中可以被重写，如果你想禁止再次重写，
可以使用 `final`：

```kotlin
open class AnotherDerived() : Base() {
  final override fun v() {}
}
```






















































