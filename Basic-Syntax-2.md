
地址：http://kotlinlang.org/docs/reference/basic-syntax.html#using-a-while-loop<br />
日期：Wed May 27 CST 2017<br />
译者：Linky<br />

# 基本语法  (二)

## 使用 while 循环

```kotlin
val items = listOf("apple", "banana", "kiwi")
var index = 0
while (index < items.size) {
  println("item at $index is ${items[index]}")
  index++
}

```

详情查看[while 循环](http://kotlinlang.org/docs/reference/control-flow.html#while-loops)

## 使用 when 表达式

```kotlin
fun describe(obj: Any): String = 
when (obj) {
  1   		-> "One"
  "Hello"	-> "Greeting"
  is Long 	-> "Long"
  !is String 	-> "Not a string"
  else 		-> "Unknow"
}
```
    译者按：这个表达式很像 switch 语句，不过能处理的类型比较宽泛

详情查看[when 表达式](http://kotlinlang.org/docs/reference/control-flow.html#when-expression)

## 使用 ranges

使用 `in` 操作符来判断一个 number 是否在某个范围

```kotlin
val x = 10
val y = 9
if (x in 1..y+1) {
  println("fits in range")
}
```

检查一个数字是否超出某个范围

```kotlin
val list = listOf("a", "b", "c")

if (-1 !in 0..list.lastIndex) {
  println("-1 is out of range")
}

if (list.size !in list.indices) {
  println("list size is out of valid list indices range too")
}
```

遍历一个 范围

```kotlin
for (x in 1..5) {
  print(x)
}
```

设置遍历节奏

```kotlin
for (x in 1..10 step 2) {
  print(x)
}

for (x in 9 downTo 0 step 3) {	// 从 9 到 0，反序遍历，步长为 3 
  print(x)
}
```

详情查看[Ranges](http://kotlinlang.org/docs/reference/ranges.html)

## 使用集合

遍历一个集合

```kotlin
for (item in items) {
  println(item)
}
```

检查一个集合是否包含某个元素

```kotlin
when {
  "orange" in items -> println("juicy")
  "apple" in items -> println("apple is fine too")
}
```

使用 lambda 表达式过滤和转化集合元素

```kotlin
fruits
.filter { it.startsWith("a") }
.sortedBy { it }
.map { it.toUpperCase() }
.forEach{ println(it) }
```

详情查看[高阶函数 和 Lambda](http://kotlinlang.org/docs/reference/lambdas.html)

