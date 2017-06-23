
地址：http://kotlinlang.org/docs/reference/basic-types.html<br />
日期：Thu Jun 15 CST 2017<br />
译者：Linky<br />

# 基本类型 (二)

## 显式转换

由于不同的表示，更小的类型不是更大类型的子类型。如果这样的话，下面的排序会有麻烦

```kotlin
// 伪代码
var a: Int? = 1		// 一个 装箱 Int (java.lang.Integer)
var b: Long? = a	// 隐式转化产生一个 装箱的 Long (java.lang.Long)
print(a == b)		// 奇怪，这里输出 false
```

所以不仅是同一性，连相等性都会默默得消失

由此我们看到，更小的类型没有隐式地转化为更大的类型。所以我们不能将一个 `Byte` 类型的值
赋值给 `Int` 类型的变量，除非显式地执行转换。

```kotlin
val b: Byte = 1	// OK
val i: Int = b	// ERROR
```

我们可以将 b 显式转换为更大的值

```kotlin
val i: Int = b.toInt()
```

每个 number 类型支持下面的转换

—— `toByte(): Byte`
—— `toShort(): Short`
—— `toInt(): Int`
—— `toLong(): Long`
—— `toFloat(): Float`
—— `toDouble(): Double`
—— `toChar(): Char`

隐式转换很少被注意到，因为类型往往可以从 Context 推出，而且
数学操作符也会为转换做一些重载。例如：

```kotlin
val l = 1L + 3	// Long + Int => Long
```

## 操作符

Kotlin 支持标准的数学操作符号集合（加、减、乘、除等），它们被声明为类的成员，
编译器会优化相应指令的调用，详情查看[Operator overloading](http://kotlinlang.org/docs/reference/operator-overloading.html)

按位操作符，没有特殊的符号给他们，仅仅命名了中缀表达式，例如：

```kotlin
val x = (1 shl 2) and 0x000FF000
```

下面是完整的 按位运算 操作符（仅用于 `Int` 和 `Long` 类型）

—— `shl(bits)` - 有符号左移，类似 java 的 `<<`
—— `shr(bits)` - 有符号右移，类似 java 的 `>>`
—— `ushr(bits)` - 有符号右移，类似 java 的 `>>>`
—— `and(bits)` - 按位 与
—— `or(bits)` - 按位 或
—— `xor(bits)` -- 按位 异或
—— `inv()` - 按位 非

## 字符

字符用 `Char` 表示，它们 **不能** 被直接当作数字

```kotlin
fun check(c: Char) {
  if (c == 1) { // ERROR: incompatible，不兼容 
    // ...
  }
}
```

字符 常量用单引号，例如：`a`，特殊字符可以用 反斜杠转译。
Kotlin 支持下面的转移序列：`\t`，`\b`，`\n`，`\'`，`\"`，`\\`，`\$`，
要编码任何其他字符，可以使用 Unicode 转译语法：`'\uFF00'`

我们可以显式地将 字符 转换为 `Int` 数字：

```kotlin
fun decimalDigitValue(c: Char): Int {
  if (c !in '0'..'9')
    throw IllegalArgumentException("Out of range")
  return c.toInt() - '0'.toInt()	// 显式转换为数值
}
```

就像数值一样，当需要可以空的引用时，char 会自动装箱，装箱后，一致性不再保留。


## Booleans

类型 `Boolean` 代表 布尔值，而且有两个值：`true` 和 `false`

当需要可为空的引用时，Boolean 也会自动装箱

作用于 boolean 上的内置操作包括：

—— `||` - 一真全真
—— `&&` - 一假全假
—— `!` - 取反 

## 数组 

Kotlin 用 类 Arrays 来表示数组，这个类有 `get` 和 `set` 方法，通过运算符重载为 `[]`，
一个 size 属性和一些其他有用的成员函数：

```Kotlin
class Array<T> private constructor() {
  val size: Int
  operator fun get(index: Int): T
  operator fun set(index: Int, value: T): Unit
  operator fun iterator(): Iterator<T>
  // ... 
}
```

为了创建一个 array，我们可以使用一个库方法 `arrayOf` 然后传入值，
例如 `arrayOf(1, 2, 3)` 创建了一个数组 `array[1, 2, 3]`。
同样的 `arrayOfNulls(size)` 库函数创建了一个包含 size 个 null 元素的数组。

创建数组的另一个方法是使用一个 工厂方法，给工厂方法传入一个表示数组元素大小的 size，
以及一个接收数组索引 i 作为参数的函数即可

```Kotlin
  // 产生一个 Array<String> = ["0", "1", "4", "9", "16"]
  val asc = Array(5, { i -> (i * i).toString() })
```

就像上面所说的，`[]` 操作符表示对成员函数 `get()` 和 `set()` 的调用。

注意：Arrays 在 Kotlin 中是不可变的，也就是说你不能将 `Arrays<String>` 赋值 给
`Array<Any>`，这可以防止可能的运行时失败。不过你可以使用 `Arrays<out any>`，详情查看][Type Projections](http://kotlinlang.org/docs/reference/generics.html#type-projections)

Kotlin 也提供了特殊的类来表示没有装箱开销的原生类型的数组，`ByteArray`，`ShortArray`，`IntArray` 等等。
这些类和 `Array` 之间没有继承关系。但是他们有相同的方法和属性集合，每个都有相应的工厂方法：

```kotlin
  val x: IntArray = intArrayOf(1, 2, 3)
  x[0] = x[1] + x[2]
```

## 字符串 Strings

字符串可以用 `String` 来表示，`String` 是不可变的，其中的每个元素都是 characters，
可以通过 `s[i]` 来访问。一个 String 可以通过 for 循环来遍历：

```kotlin
  for (c in str) {
    println(c)
  }
```

## String 字面量 

Kotlin 有两种类型的 string 字面量：转译字符串（包含转译字符）和原始字符串（可以包含新行和任意文本）。
转译字符串非常类似 java 字符串：

```kotlin
val s = "Hello, world!\n"
```

一个原生字符串用一个三引号 `"""` 限定，不对转译符号进行转译，可以包括新行和任何其他字符：

```kotlin
val text = """
    for (c in "foo")
      print(c)
"""
```

可以通过 [trimMargin()](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.text/trim-margin.html) 来移除开头的空白符号

```kotlin
  val text = """
    |Tell me and I forget.
    |Teach me and I remember.
    |Involve me and I learn.
    |(Benjamin Franklin)
  """.trimMargin()
```

默认情况下，`|` 被用于间距前缀，也就是说 `trimMargin()` 相当与 `trimMargin("|")`，`|` 会被替换掉。
你也可以选择其他的字符并把它作为参数，比如：`trimMargin(">")`

## 字符串模板 

字符串可以包含模板表达式，代码段会被计算，然后将结果串联到字符串中，
一个模板表达式以 美元符 `$` 开头，要么接上一个简单的名字，例如：

```kotlin
val i = 10
val s = "i = $i"	// s 被赋值为字符串 "i = 10"
```

或者接上其他表示式，并且用花括号包围：

```kotlin
val s = "abc"
val str = "$s.length is ${s.length}" // str 被赋值为 abc.length is 3 
```

模板可以用在 原始字符串 或者 转译字符串中，如果你需要使用美元符字面值，可以使用下面的语法：

```kotlin
val price = """
  ${'$'}9.99
"""
```

