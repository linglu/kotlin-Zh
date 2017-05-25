
地址：http://kotlinlang.org/docs/tutorials/command-line.html<br />
日期：Wed May 25 CST 2017<br />
作者：Linky<br />

# 使用命令行编译运行 Kotlin

这个教程将带领大家使用命令行创建 Hello World 应用程序

## 下载编译器

每个 release 都有一个独立的编译器版本，我们可以在[GitHub Releases](https://github.com/JetBrains/kotlin/releases/tag/v1.1.2-2)下载<br />
当前最新版本是 1.1.2-2

### **手动安装**

解压下载好的到指定目录，然后你可以选择把 `bin` 目录放到系统环境变量。`bin` 目录包含编译和运行 Kotlin 所需的脚本。

### **SDKMAN!**

在基于 UNIX 的操作系统下，例如 OS X、Linux、Cygwin、FreeBSD 和 Solaris，一个更简单的安装方法是使用 [SDKMAN!](sdkman.io)。简单运行下面的命令：

```
 $ curl -s https://get.sdkman.io | bash
```

然后打开新的 终端(terminal)，输入如下命令安装：

```
$ sdk install kotlin
```

### **Homebrew**

在 OS X 下，你可以使用 [Homebrew](https://brew.sh/) 安装：

```
 $ brew update
 $ brew install kotlin
```

### **MacPorts**

如果你是 [MacPorts](https://www.macports.org/) 用户，可以如下安装

```
$ sudo port install kotlin
```

## 创建和运行第一个程序

 1、用你喜欢的编辑器，创建一个新文件，命名为 hello.kt，输入如下代码：

```
fun main(args: Array<String>) {
    println("Hello, World!")
}
```

 2、使用 Kotlin 编译器编译应用

```
$ kotlinc hello.kt -include-runtime -d hello.jar
```

**`-d`** 选项意味着我们希望编译器的输出如何命名，可以是目录，用来存放 class 文件，也可以是 .jar 文件。
**`-include-runtime`** 选项可以让 .jar 文件包含 Kotlin 运行时库从而可以直接运行。
	如果你想看所有的可用选项，运行

```
$ kotlinc -help
```

 3、运行应用
```
$ java -jar hello.jar
```

## 编译成库

如果你正在开发其他 Kotlin 应用需要使用的库，你可以生成一个不带 Kotlin 运行时的 .jar 文件

```
$ kotlinc hello.kt -d hello.jar

```
由于这样生成的 .jar 文件不包含 Kotlin 运行时，所以你应该确保当它被使用时，运行时在你的 classpath 上

你也可以使用 kotlin 命令来运行 Kotlin 编译器生成的 .jar 文件

```
$ kotlin -classpath hello.jar HelloKt
```

`HelloKt` 是 Kotlin 编译器为 `hello.kt` 生成的 主类名

## 运行 REPL（交互式解释器）

我们可以运行如下命令得到一个可交互的 shell，然后输入任何有效的 Kotlin 代码，并立即看到结果<br />

![kotlin_shell](http://kotlinlang.org/assets/images/tutorials/command-line/kotlin_shell.png)


## 使用命令行运行脚本

Kotlin 也可以作为一个脚本语言使用，一个脚本是一个 .kts 文件。
例如我们创建一个文件，命名为 `list_folders.kts`，写入如下内容：

```
   import java.io.File

   val folders = File(args[0]).listFiles { file -> file.isDirectory() }
   folders?.forEach { folder -> println(folder) }
```

执行时，给 编译器加入 `-script` 选项 和需要查看的目录地址

```
$ kotlinc -script list_folders.kts <path_to_folder>
```
其中 `<path_to_folder>`是一个目录地址， 作为参数传递给 args[0]。















