---
title: Java编译小坑
date: 2021-10-24 14:23:26
tags: 编程,入门
---

​	最近在帮助同学们解答Java问题的时候，发现了win10上使用命令行编译会出现GBK编码问题。以下就来讲讲这个问题是如何出现的，以及如何去修复这个问题。

<!--more-->

#### 问题现象

```java
public class Main{
    public static void main(String[] args) {
        System.out.println("你好！");
    }
}
```

上方是经典的第一个程序的源代码。 当我们编译的时候会出现

![image-20211024142838520](/photos/image-20211024142838520.png)

提示编码的GBK不可映射字符。

如果我们去掉那个"!"，变成

```java
public class Main{
    public static void main(String[] args) {
        System.out.println("你好");
    }
}
```

运行它

![image-20211024143105336](/photos/image-20211024143105336.png)

我们发现又可以编译了。

但是当我将其放在intellij idea内运行时

![image-20211024143334891](/photos/image-20211024143334891.png)

即使使用了第一次的代码也不会报错

#### 问题分析

出现此问题可能是输出语句中包含了中文符号，但是当我仔细研究了终端的编码时，我才发现。

![image-20211024143443974](/photos/image-20211024143443974.png)

我们的终端使用的时GBK文字编码，但是在记事本中

![image-20211024143527829](/photos/image-20211024143527829.png)

他却是UTF-8编码的。

因此我认为是文件的编码与终端运行的编码不一致出现的输出错误。

#### 解决问题

解决问题的最好方式就是不使用终端，转用更为方便的ide。例如

> Visual Studio	无需配置，环境一步到位
>
> Visual Studio Code	需要配置，并且没有方便的代码提示
>
> Jetbrain  IntelliJ IDEA	无需配置，我比较推荐这个选择

还有一种办法，将文件转码为GBK文件，但是我们需要借助一些工具，比如notepad++、Visual Studio Code等，下面我以Visual Studio Code（以下简称vsc）为例来讲述如何转码。

在vsc中打开你所写的java源文件，蓝色标记处显示了你的文件的编码。

![image-20211024144220753](/photos/image-20211024144220753.png)

点击它，选择“通过编码保存”

![image-20211024144345053](/photos/image-20211024144345053.png)

在输入框中输入"GBK"，用鼠标点击第一个结果。

![image-20211024144419456](/photos/image-20211024144419456.png)

我们发现，原来蓝色标记的是UTF-8变成了GBK，然后“保存”。

#### 查看问题是否解决

![image-20211024144605138](/photos/image-20211024144605138.png)

问题成功解决。
