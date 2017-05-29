
地址：http://kotlinlang.org/docs/reference/idioms.html<br />
日期：2017年 05月 29日 星期一<br />
译者：Linky<br />

# 编码规范

这个页面包含当前 Kotlin 语言的编程规范

## 命名风格

首先毫无疑问，默认情况下遵循 Java 的编程风格，比如：

-- 使用驼峰命名，避免下划线命名
-- 类首字母大写
-- 方法和属性首字母小写
-- 使用 4 个空格的缩进
-- public 方法应该有文档注释，这样才能出现在生成的 Kotlin Doc 中

## 冒号

**分割子类和父类的冒号前面需要要有空格**
**分割类型和对象的冒号前面不需要有空格**

```kotlin
interface Foo<out T : Any> : Bar { // T 和 Any 之间是继承关系，所以冒号前面有空格
  fun foo(a: Int): T	// a 和 Int 之间是类型和对象之间的关系，所以冒号前面不需要空格
}
```

## Lambdas

Lambda 中，花括号 {} 两边 以及 箭头 -> 两边都需要有空格

```kotlin
list.filter { it > 10 }.map { element -> element * 2 }
```

在一个短而且没有嵌套的 lambda 表达式中，一般建议使用 it 而不是自定义一个
参数。而在嵌套的 lambda 表达式中，则一般需要显式声明参数

## 类头格式

如果一个类只有很少的参数，那么可以一行写完

```kotlin
class Person(id: Int, name: String)
```

如果一个类有更长的参数，则每个参数一行，每行开头一个缩进（4 个空格），
最后一个右括号写在新的一行，如果还有继承关系的话，父类写在和右括号同一行。

```kotlin
class Person(
    id: Int,
	name: String,
	surname: String
) : Human(id, name) {
  // ...
}
```

如果有多个继承，父类的构造器应该写在第一个，然后每个接口写在新行

```kotlin
class Person(
    id: Int,
	name: String,
	surname: String
) : Human(id, name),
    KotlinMaker {
  // ...
}
```

## Unit

如果一个函数返回 Unit，返回类型可以被忽略

```kotlin
fun foo() { // ": Unit" 在这里被忽略

}
```

## 函数 VS 属性

某些情况下，没有参数的函数和只读参数是可以互换的。
虽然语义类型相似，但是在 `when` 表达式中有一些风格规范上的偏好

在底层算法中，更偏向使用 属性

-- 不会抛出异常
-- 有 O(1) 时间复杂度
-- 方便计算（在第一次运行时缓存）
-- 每次调用返回相同的结果















