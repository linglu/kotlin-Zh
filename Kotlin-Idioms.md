
地址：http://kotlinlang.org/docs/reference/idioms.html<br />
日期：2017年 05月 28日 星期日<br />
译者：Linky<br />

# 习语（Idioms）

这篇文章是 Kotlin 中经常使用的 习语 的集合。如果你有更喜欢的，可以通过 [Pull request](https://github.com/JetBrains/kotlin-web-site/edit/master/pages/docs/reference/idioms.md) 分享

## 创建 DTOs(POJOs/POCOs)

```kotlin
data class Customer(val name: String, val email: String)
```

这条语句创建了一个有如下特性的 `Customer` 类

-- 为所有属性创建 getters，如果 该属性是 var 的话，也创建 setters 属性
-- `equals()`
-- `hashCode()`
-- `toString()`
-- `copy()`
-- 为所有属性创建 `component1()`, `component2()`，...，详情查看[Data classes](http://kotlinlang.org/docs/reference/data-classes.html)

## 为函数参数定义默认值

```kotlin
fun foo(a: Int = 0, b: String = "") {...}
```

## 过滤一个列表

```kotlin
val positives = list.filter {x -> x > 0 }
```

或者更简单

```kotlin
val positives = list.filter { it > 0 }
```

## 数据插入

```kotlin
println("Name $name")
```

## 对象检查

```kotlin
when (x) {
  is Foo -> ...
  is Bar -> ...
  else   -> ...
}
```

## 遍历一个 Map

```kotlin
for ((k, v) in map) {
  println("$k -> $v")
}
```

## 范围使用

```kotlin
for (i in 1..100) {...} // 闭区间，包括 100
for (i in 1 until 100) {...} // 半开区间，不包括 100
for (x in 2..10 step 2) {...}
for (x in 10 downTo 1) {...}
if (x in 1..10) {...}
```

## 定义一个只读列表
```kotlin
val list = listOf("a", "b", "c")
```

## 定义一个只读 Map

```kotlin
val map = mapOf("a" to 1, "b" to 2, "c" to 3)
```

## 访问一个 Map

```kotlin
println(map["key"])
map["key"] = value
```

## 懒加载

```kotin
val p: String by lazy {
  // 计算 string 
}
```

## 扩展一个方法

```kotlin
fun String.spaceToCamelCase() { ... }

"Convert this to camelcase".spaceToCamelCase();
```

## 创建一个 单例

```kotlin
object Resource {
  val name = "Name"
}
```

## 非空检测 的简写

```kotlin
val files = File("Test").listFiles()
println(files?.size)
```

## 如果非空，否则 的简写

```kotlin
val files = File("Test").listFiles()
println(files?.size ?: "empty")
```

## 若为空，则执行一条语句，比如：抛出异常

```kotlin
val data = ...
val email = data["email"] ?: throw IllegalStateException("Email is missing!")
```

## 若不为空，则执行一条语句

```kotlin
val data = ...
data?.let {
  ... // 若 data 不为 null，则执行这个代码块
}
```

## return 一个 when 语句

```kotlin
fun transform(color: String): Int {
  return when (color) {
    "Red" -> 0
    "Green" -> 1
    "Blue" -> 2
    else -> throw IllegalArgumentExcetion("Invalid color param value")
  }
}
```

## 'try/catch' 表达式

```kotlin
fun test() {
  val result = try {
    count()
  } catch (e: ArithmeticException) {
    throw IllegalStateException(e)
  }

  // 操作 result 
}
```

## 'if' 表达式

```kotlin
fun foo(param: Int) {
  val result = if (param == 1) {
    "one"
  } else if (param == 2) {
    "two"
  } else {
    "three"
  }
}
```

## Builder 风格的函数

```kotlin
fun arrayOfMinusOnes(size: Int): IntArray {
  return IntArray(size).apply { fill(-1) }
}
```

## 单表达式 函数

```kotlin
fun theAnswer() = 42
```

这个等价于

```kotlin
fun theAnswer(): Int {
  return 42
}
```

这可以更高效地和其他习语一起使用，写出更简洁的代码。比如 和 when 表达式一起使用

```kotlin
fun transform(color: String): Int = when (color) {
  "Red" -> 0
  "Green" -> 1
  "Blue" -> 2
  else -> throw IllegalArgumentException("Invalid color param value")
}
```

## 在一个对象实例中调用多个方法 - 使用 with 语句

```kotlin
class Turtle {
  fun penDown()
  fun penUp()
  fun turn(degrees: Double)
  fun forward(pixels: Double)
}

val myTurtle = Turtle()
with(myTurtle) {	// 画一个 100 像素的正方形
  penDown()
  for (i in 1..4) {
    forward(100.0)
    turn(90.0)
  }
  penUp()
}
```

## 读取一个文件内容

```kotlin
val stream = Files.newInputStream(Paths.get("/some/file.txt"))
stream.buffered().reader().use { reader -> 
  println(reader.readText())
}
```

## 泛型方法的简便形式

```kotlin
// Java 的定义
// public final class Gson {
//  ...
// public <T> T fromJson(JsonElement json, Class<T> classOfT) throws 
// JsonSyntaxException {
// ...

inline fun <reifield T: Any> Gson.fromJson(): T = this.fromJson(json, T::class.java)

```

## 消费一个 nullable Boolean

```kotlin
val b: Boolean? = ...
if (b == true) {

} else {
    // b 为 空 或者 false 时执行这个分支
}
```















