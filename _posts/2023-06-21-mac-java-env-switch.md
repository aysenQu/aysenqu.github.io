---
layout: post
title: Mac下多版本的java环境共存
categories: [MAC]
description: 小窍门：如何在Mac下切换多个版本的java sdk环境
keywords: java, mac

---

为什么会出现需要安装多个java sdk版本的情况？那是因为大家都生活在不同次元！
<br/><br/><br/>

JDK的下载：
[www.oracle.com](www.oracle.com)

Mac下Java的安装路径：`/Library/Java/JavaVirtualMachines/jdkXXXX`

多年的使用，我的电脑中存在了jdk1.8，jdk11，jdk17三个版本，那么在具体项目中切换到所需的环境呢？

<br/>
> 正文

先执行命令打开文件 `open ~/.bash_profile`


编辑如下：

```
export JAVA_8_HOME=$(/usr/libexec/java_home -v1.8)
export JAVA_11_HOME=$(/usr/libexec/java_home -v11)
export JAVA_17_HOME=$(/usr/libexec/java_home -v17)
 
alias java8='export JAVA_HOME=$JAVA_8_HOME'
alias java11='export JAVA_HOME=$JAVA_11_HOME'
alias java17='export JAVA_HOME=$JAVA_17_HOME'
 
# default to Java 11
java11
```
(按自己的真实所有进行编辑)

编辑完后，执行编辑`source ~/.bash_file`


然后每次需要改变时，编辑.bash_file最后一行，再执行一次就OK。

检查是否切换成功

`java -version`

<br/>
> 扩展

实际操作中，原本在PATH中增加了1.8的sdk路径，因此切换一直不成功。只需要删除掉PATH中所有有关java的配置。
那么如何删除PATH中的某一条呢？

简单，先`echo $PATH`打印出所有条目，然后copy出来，在文本中去掉需要删除的条目。

执行
```
export PATH=""
```
全部置空，然后再把编辑后的内容重新设置进来

<br/>
> 阅读参考：

[mac配置Java8与Java11切换](https://www.jianshu.com/p/9de5c648b2e4)