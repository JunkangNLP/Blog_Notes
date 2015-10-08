title: Mac开发环境
date: 2014-12-15
tags: [工具]
categories: 工程
---
### <font color="#32CD99"> IDE的选择 </font>

#### 1)  PyCharm

  PyCharm 不用多说，覆盖了Sublime的插件功能，在重构、调试方面也是非常顺手，IDE的使用的确可以大大增加效率的。
平时写Python，可以分为两个场景，写一些简单的代码，Sublime上就行了，启动块，占内存小。但涉及大型一点的工程，或者想改代码，重构某个模块，PyCharm是更为合适的选择。

#### 2） Sublime文本编辑器

  Sublime3挺好用的，虽然会跳出购买的框，但没关系，还是OK的。Python很大一部分可以用Sublime来代替，但是C++折腾了蛮久还是没有发现可以代替，所以sublime只能在学习C++写些代码可以用，其他还是使用Appcode来用。其他还有好多插件，目前用不上, VIM模式也可以节省记忆少去记一些文本操作键。
Sublime做一些设置可以在工作环境中写一些代码，这个完全可以做到。  
1)    JEDI 补全插件.
2)    brogrammer主题不错。
3)    sublimelinter 
4)    sublimelinter-pep8, sulimelinter-pyflakes
4)    sublimelinter-sqlint

#### 3) IDEA 
  作为 Scala 和 Spark 的开发IDE。用Sublime文本编辑。

#### 4) Eclipse
  身不由己

### <font color="#32CD99"> Python相关 </font>

#### 1) Python的版本问题

  Python由于存在两个版本的原因，虽然大部分库已经有了对Python3的支持，但是有备无患，用Pyenv做版本管理，用miniconda做库管理，非常方便。而且不论是IDE还是使用Python补全插件，都可以指定解释器的位置，就算不装Pyenv也是OK的。

#### 2) Python 库

*  numpy
*  scipy
*  pandas
*  pymc
*  jieba(分词)
*  scikit-learn(机器学习)

### <font color="#32CD99"> Java 相关 </font>

  Mac 下的 java6 是 Apple 自己提供的版本，有时候需要用到更高的java版本，本来以为 jenv 和 pyenv 一样好用，实际上有些问题。所以通过更改环境变量可以随时更改版本。

    # Mac默认 JDK 6（Mac默认自带了一个jdk6版本）  
    export JAVA_6_HOME=`/usr/libexec/java_home -v 1.6`  
    # 设置 JDK 7  
    export JAVA_7_HOME=`/usr/libexec/java_home -v 1.7`  
    # 设置 JDK 8  
    export JAVA_8_HOME=`/usr/libexec/java_home -v 1.8`  
      
    #默认JDK 6  
    export JAVA_HOME=$JAVA_6_HOME  
      
    #alias命令动态切换JDK版本  
    alias jdk6="export JAVA_HOME=$JAVA_6_HOME"  
    alias jdk7="export JAVA_HOME=$JAVA_7_HOME"  
    alias jdk8="export JAVA_HOME=$JAVA_8_HOME"  

### <font color="#32CD99"> Scala & Spark </font>

待续。

参考资料：
*    [Setting Up Sublime Text 3 for Full Stack Python Development](https://realpython.com/blog/python/setting-up-sublime-text-3-for-full-stack-python-development/)
*    [MAC下安装多版本JDK和切换几种方式](http://chessman-126-com.iteye.com/blog/2162466)
