
地址：http://kotlinlang.org/docs/reference/basic-syntax.html<br />
日期：Wed May 31 08:29:36 CST 2017<br />
译者：Linky<br />

# 基本类型 （一）

**在 Kotlin 中，一切都是对象，这意味着我们可以在任何变量上调用成员函数和属性**。
一些方法是内置的，因为他们的实现被优化过，但是对于用户来说，可以把它们看作普通
的类。这一节我们描述这些类型：numbers, characters, booleans 和 arrays。

## Numbers

Kotlin 处理 numbers 的方式和 Java 很像，但不完全相同。比如 Kotlin 没有隐式
的范围扩大，和字面值表示上的一些区别。

Kotlin 提供下列的内置类型表示 Numbers（这和 Java 有点像）

| 类型   | 位数 | 
| - |:-:|
| Double | 64 |
| Float  | 32 |
| Long   | 64 |
| Int    | 32 |
| Short  | 16 |
| Byte   | 8  |

<br />
注意到，字符型（Char）在 Kotlin 中不属于 Numbers


## 字面常量

整数值有下面几种字面常量：

—— 十进制：`123`
—— Long 型用大写 `L` 标记：`123L`
  
—— 八进制：`0x0F`

—— 二进制：`0b00001011`

注意到：*不支持 八进制 的字面常量*

Kotlin 也支持浮动数的约定标记：

-- Doubles : 123.5, 123.5e10

-- Floats : 123.5f 或者 123.5F

## 从 V1.1 开始，Kotlin 支持下划线数字字面值

你可以使用 下划线 来让数字常量可读性更强：

```kotlin
val oneMillion = 1_000_000
val creditCardNumber = 1234_5678_9012_3456L
val socialSecurityNumber = 999_99_9999L
val hexBytes = 0xFF_EC_DE_5E
val bytes = 0b11010010_01101001_10010100_10010010
```

## 关于装箱

在 java 平台中，numbers 在 JVM 中以原生类型方式存储，除非我们需要一个
可为 null 的引用或者设计到泛型。在后面一种类型中，数值被装箱。

Kotlin 中，numbers 的装箱没有保持一致性 ( `===` )

```kotlin
val a: Int = 10000
print(a === a) // 打印 true
val boxedA: Int? = a
val anotherBoxedA: Int? = a
print (boxedA === anotherBoxedA) // !!! 打印 false !!!
```

另一方面，它保留了 相等性 ( `==` )
```kotlin
val a: Int = 10000
print(a == a) // 打印 true
val boxedA: Int? = a
val anotherBoxedA: Int? = a
print (boxedA == anotherBoxed) // 打印 true
```
