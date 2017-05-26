
地址：http://kotlinlang.org/docs/reference/basic-syntax.html<br />
日期：Wed May 26 CST 2017<br />
译者：Linky<br />

# 基本语法  (一)

地址：http://kotlinlang.org/docs/reference/basic-syntax.html

## 定义包（packages）

包的声明应该写在源文件的最上面

```kotlin
package my.demo

import java.util.*

// ...
```

源文件可以放在文件系统的任意位置，不用专门去匹配目录和包，详情查看[Packages](http://kotlinlang.org/docs/reference/packages.html)

## 定义函数

如果一个函数有两个 Int 类型的参数并且返回 Int 类型，可以这样写：
```kotlin
fun sum(a: Int, b: Int) : Int {
  return a + b
}
```

一个函数可以只有函数体，返回类型根据返回值确定：

```kotlin
fun sum(a: Int, b: Int) = a + b
```

如果一个函数没有返回值，可以如下定义：
```kotlin
fun printSum(a: Int, b: Int): Unit{
  println("sum of $a and $b is $(a + b)")
}
```
`Unit` 返回值可以被忽略

详情查看[Functions](http://kotlinlang.org/docs/reference/functions.html)

## 定义局部变量

只读局部变量，只赋值一次：val 开头
```kotlin
val a: Int = 1  // 立即赋值
val b = 2  	// 没有声明类型，但是根据 2 的类型，自动将 b 设置为 Int 类型
val c: Int 	// 如果没有在声明时初始化，需要提供类型信息
c = 3
```

可修改变量：var 开头

```
var x = 5 // 没有声明类型，但是根据 5 的类型，自动将 x 设置为 Int 类型
x += 1
```

详情查看[属性和域](http://kotlinlang.org/docs/reference/properties.html)

## 注释

就像 Java 和 JavaScript 一样，Kotlin 支持单行和多行注释

```
// 这是单行注释

/* 这是多行
   注释 */
```

和 Java 不同的是，Kotlin 中的注释可以嵌套

查看[文档化 Kotlin 代码](http://kotlinlang.org/docs/reference/kotlin-doc.html)了解文档注释语法

## 使用字符串模板
```
var a = 1
// simple name in template:
val s1 = "a is $a" 

a = 2
// arbitrary expression in template:
val s2 = "${s1.replace("is", "was")}, but now is $a"
```
详情查看[字符串模板](http://kotlinlang.org/docs/reference/basic-types.html#string-templates)


## 使用条件表达式

```
fun maxOf(a: Int, b: Int): Int {
  if (a > b) {
    return a
  } else {
    return b
  }
}
```

上述表达式可以写成 if 表达式

```
fun maxOf(a: Int, b: Int) = if (a > b) a else b
```

详情查看[if 表达式](http://kotlinlang.org/docs/reference/control-flow.html#if-expression)


## 使用 nullable 值

一个引用必须明确得声明为 `nullable` 才有可能为 null

下面的函数，如果 `str` 不是一个 int 值的字符串形式，将返回 null

```
fun parseInt(str: String): Int? {
  // ...
}
```

下面是一个返回值可为空的函数

```
fun printProduct() {
  val x = parseInt(arg1)
  val y = parseInt(arg2)

  // 直接使用 `x * y` 的话会产生 error 因为可能为 null
  if (x != null && y != null) {
    // 
    println(x * y)
  } else {
    println("either '$arg1' or '$arg2' is not a number")
  }
}
```

上面的函数也可写成

```
// ...
if (x == null) {
    println("Wrong number format in arg1: '${arg1}'")
    return
}
if (y == null) {
    println("Wrong number format in arg2: '${arg2}'")
    return
}

println(x * y)
```

详情查看[null 安全](http://kotlinlang.org/docs/reference/null-safety.html)

## 使用 类型检查 和 自动类型转换

`is` 操作符用来检查 一个表达式 是否为某个类型的对象，如果被判定为某个类型，将会自动完成转换，不用显示声明

```
fun getStringLength(obj: Any): Int? {
  if (obj is String) {
    // obj 在这个分支自动转换为 String 类型，不用显式转换
    return obj.length
  }

  // obj 仍然是 Any 类型
  return null
}
```

上面的函数也可写成

```
fun getStringLength(obj: Any): Int? {
    if (obj !is String) return null

    // obj 在这个分支自动转换为 String 类型，不用显式转换
    return obj.length
}
```

还可写成

```
fun getStringLength(obj: Any): Int? {
    // 在 && 右边的 obj 自动转换为 String 类型了
    if (obj is String && obj.length > 0) {
        return obj.length
    }

    return null
}
```

详情可查看[类](http://kotlinlang.org/docs/reference/classes.html) 和 [类型转换](http://kotlinlang.org/docs/reference/typecasts.html)


## 使用 for 循环

```
val items = listOf("apple", "banana", "kiwi")
for (item in items) {
  println(item)
}
```

或者

```
val items = listOf("apple", "banana", "kiwi")
for (index in items.indices) {
    println("item at $index is ${items[index]}")
}
```

详情查看[for 循环](http://kotlinlang.org/docs/reference/control-flow.html#for-loops)

