

地址：http://kotlinlang.org/docs/reference/control-flow.html<br />
日期：2017年 06月 24日 星期六<br />
译者：Linky<br />

## 控制流

### If 表达式

在 Kotlin 中，if 是一个表达式，也就是说，它返回一个值。所以不存在三元操作符号(condition ? then : else)，
因为一个 if 语句可以实现这个功能。

```kotlin
// 传统用法
var max = a
if (a < b) max = b

// 加上 else
var max: Int
if (a > b) {
  max = a
} else {
  max = b
}

// 当 if 作为一个表达式时
val max = if (a > b) a else b
```

if 分支可以是一个块，而且最后一个表达式是这个块的值：

```kotlin
val max = if () {
  print("Choose a")
  a
} else {
  print("Choose b")
  b
}
```

如果你使用 if 是作为一个表达式，而不是一条语句，那么这个表达式被要求有一个 else 分支。

详情查看[grammar for if](http://kotlinlang.org/docs/reference/grammar.html#if)

## When 表达式

`when` 取代了 `switch` 语句，它最简单的形式像下面这样：

```kotlin
when (x) {
  1 -> print("x == 1")
  2 -> print("x == 2")
  else -> { // 注意，这是一个 块（block）
    print("x is neither 1 nor 2")
  }
}
```

`when` 会用它的参数顺序地匹配每个分支，直到有一个分支的条件满足。

`when` 既可以用作一个表达式也可以用作一个语句。当用作表达式时，满足条件的分支的值
将作为整个表达式的值。如果它用作一个语句，单条分支的值会被忽略。（就像 if 表达式，每条分支
都可以是一个块，它的值是块中最后一个表达式的值）

当其他分支都不满足时，将会走 else 分支。如果 when 被用于表达式，除非编译器可以证明，所有可能的
请求都被分支条件考虑到了，否则将走 else 分支。

如果很多情况都会用相同的方式处理，那么可以用逗号隔开分支条件：

```kotlin
  when (x) {
    0, 1 -> print("x == 0  or x == 1")
    else -> print("otherwise")
  }
```

我们可以用任意的表达式（不仅仅是常量）作为分支条件：

```kotlin
  when (x) {
    parseInt(s) -> print("s encodes x")
    else -> print("s does not encode x")
  }
```

我们也可以使用 when 来检查一个值是否在一个范围或者集合中：

```kotlin
  when (x) {
    in 1..10 -> print("x is in the range")
    in validNumbers -> print("x is valid")
    !in 10..20 -> print("x is outside the range")
    else -> print("none of the above")
  }
```

when 的另一种用法是，检查一个值是否某个特定类型。注意到，由于 [智能类型转换](http://kotlinlang.org/docs/reference/typecasts.html#smart-casts)，你可以不用其他检查就可以访问一个类的函数或属性。

```kotlin
  fun hasPrefix(x: Any) = when(x) {
    is String -> x.startsWith("prefix")
    else -> false
  }
```

when 也可以作为 `if-else-if` 的替代方式。如果没有提供参数，分支的条件就是简单的 boolean 表达式，
当该 boolean 表达式为真时，分支得到执行。

```kotlin
  when {
    x.isOdd() -> print("x is odd")
    x.isEven() -> print("x is even")
    else -> print("x is funny")
  }
```

详情查看[grammar for when](http://kotlinlang.org/docs/reference/grammar.html#when)


## For 循环

for 循环通过任何提供迭代器的对象来遍历。语法类似下面这样：

```kotlin
  for (item in collection) print(item)
```

循环体可以是一个块

```kotlin
  for (item: Int in ints) {
    // ...
  }
```

就像上面提到的，for 通过任何提供迭代器的对象来遍历，例如：

  —— 有一个成员或者扩展函数 `iterator()`，它的返回类型 既有一个成员或者一个扩展函数 `next()`，
     也有一个 返回 `Boolean`类型的 成员或者扩展函数 `hasNext()`

上面三个函数都要标记为 `operator`。

在一个数组上面的循环，将会被编译成基于索引的循环而不会创建一个迭代器对象。

如果你想通过一个数组或者列表来实现遍历，可以这样实现：

```kotlin
  for (i in array.indices) {
    print(array[i])
  }
```

注意到，通过一个范围来实现遍历的方式会被编译为最优实现，而没有额外的对象创建。

此外，你还可以使用 `withIndex` 库函数来遍历：

```kotlin
  for ((index, value) in array.withIndex()) {	// 跟 PHP 中的很像 
    println("the element at $index is $value")
  }
```

详情查看[grammar for for](http://kotlinlang.org/docs/reference/grammar.html#for)

## While 循环

`while` 和 `do..while` 的工作方式跟往常的一样

```kotlin
  while (x > 0) {
    x--
  }

  do {
    val y = retriveData()
  } while (y != null)	// 局部变量 y 在这里是可见的 
```

详情可以查看[grammar for while](http://kotlinlang.org/docs/reference/grammar.html#while)

## break 和 continue 在循环中的使用

Kotlin 支持传统的 break 和 cotinue 操作，详情查看[Returns and jumps](http://kotlinlang.org/docs/reference/returns.html)
















