
地址：http://kotlinlang.org/docs/tutorials/getting-started.html<br />
日期：Wed May 24 CST 2017<br />
作者：Linky<br />

# 用 IntelliJ IDEA 运行 Kotlin

## 配置环境

&ensp;&ensp;&ensp;&ensp;这个教程我们将讲解使用 IDEA 运行 Kotlin，如果想了解如何用命令行编译和运行 Kotlin 应用，可以移步：[命令行运行 Kotlin](http://kotlinlang.org/docs/tutorials/command-line.html)

&ensp;&ensp;&ensp;&ensp;如果你对 JVM 和 Java 也感到陌生，可以移步[JVM 生存指南](http://hadihariri.com/2013/12/29/jvm-minimal-survival-guide-for-the-dotnet-developer/)。如果你对 IntelliJ IDEA 感到陌生，可以移步[IntelliJ IDEA 生存指南](http://hadihariri.com/2014/01/06/intellij-idea-minimal-survival-guide/)

下面开始进入正题

1. **安装最新版本的 IntelliJ IDEA**。可运行 Kotlin 的最小 IntelliJ IDEA 版本是 15，你可以从 [JetBrains](https://www.jetbrains.com/) 下载免费的[社区版本](https://www.jetbrains.com/idea/download/index.html)

2. 创建一个新项目。我们选择 Java Module 和 选择 Project SDK。Kotlin 的运行的最小 JDK 版本是 1.6，然后选中 Kotlin(java) <br />
  ![new_project_step1](http://kotlinlang.org/assets/images/tutorials/getting-started/new_project_step1.png)

3. 下一步写入你的项目名称<br />
  ![project_name](http://kotlinlang.org/assets/images/tutorials/getting-started/project_name.png)

4. 现在你应该有如下的项目结构<br />
  ![folders](http://kotlinlang.org/assets/images/tutorials/getting-started/folders.png)

5. 然后在 源文件目录下创建一个新的 Kotlin 文件，命名为 app.kt，当然也可以取其他名称<br />
  ![new_file](http://kotlinlang.org/assets/images/tutorials/getting-started/new_file.png)

6. 然后我们需要写 main 方法，这是 Kotlin 应用的入口。IntelliJ IDEA 提供了这个模板，只需要输入 main，然后按 tab 键即可<br />
  ![main](http://kotlinlang.org/assets/images/tutorials/getting-started/main.png)

7. 现在添加一行 Hello World 代码<br />
  ![hello_world](http://kotlinlang.org/assets/images/tutorials/getting-started/hello_world.png)

8. 现在我们可以运行 Kotlin 应用，最简单的方法是点击左边 gutter 的 Kotlin 图标，然后选择运行 *Appkt*<br />
  ![run_default](http://kotlinlang.org/assets/images/tutorials/getting-started/run_default.png)

9. 如果一切顺利，我们应该可以在 **Run** 工具窗口看到结果<br />
  ![run_window](http://kotlinlang.org/assets/images/tutorials/getting-started/run_window.png)







