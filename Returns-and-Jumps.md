地址：http://kotlinlang.org/docs/reference/returns.html<br />
日期：2017年 06月 24日 星期六<br />
译者：Linky<br />

## 返回和跳转

Kotlin 有三个结构化的跳转表达式：

—— return 
—— break
—— continue

所有这三个表达式都可以作为更大表达式的一部分：

```kotlin
  val s = person.name ?: return
```

这些表达式的类型是 [Nothing type](http://kotlinlang.org/docs/reference/exceptions.html#the-nothing-type)

## Break 和 Continue 标签 

Kotlin 中的任意表达式都可以标记为一个 label。Label 由一个标记符跟上 `@` 符号构成。
例如 `abc@`，`fooBar@`，为了标记一个表达式，我们只需要在它前面加一个 label 即可。

```kotlin
  loop@ for (i in 1..100) {
    // ...
  }
```

现在，我们可以使用 label 来限制一个 break 或者一个 continue 语句：

```kotlin
  loop@ for (i in 1..100) {
    for (j in 1..100) {
      if (...) break @loop
    }
  }
```

break 将跳转到循环结束后的下一行作为执行入口，continue 将继续执行这个循环的下一个迭代。

## Return Label

在 Kotlin 中，函数可以被嵌套。returns 允许我们从更外层的函数中返回。最重要的使用场景是从
一个 lambda 表达式中返回。回忆一下，当我们写这个的时候：

```kotlin
  fun foo() {
    ints.forEach {
      if (it == 0) return
      print(it)
    }
  }
```

return 表达式将从最外层函数中返回，例如 `foo`。如果我们想仅仅从 lambda 表达式中返回，我们必须
给它加上标签。

```kotlin
  fun foo() {
    ints.forEach lit@ {
      if (it == 0) return @lit
      print(it)
    }
  }
```

现在它将仅仅从 lambda 表达式中返回。同样情况下，使用 隐式标签会更方便一点，这个标签
和向 lambda 表达式传入的 函数有相同的名字。

```kotlin
  fun foo() {
    ints.forEach {
      if (it == 0) return@forEach
      print(it)
    }
  }
```

此外，我们还可以用 匿名函数 来替换 lambda 表达式，匿名函数中的 return 语句将只退出
该匿名函数。

```kotlin
  fun foo() {
    ints.forEach(fun(value: Int) {
      if (value == 0) return
      print(value)
    })
  }
```

当返回一个值时，解析器会给 return 一个引用，例如：

```kotlin
  return@a 1
```

这意味着，在 label @a 返回 1,而不是返回一个表达式 `(@a 1)`
