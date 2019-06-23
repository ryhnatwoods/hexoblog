---
title: java基础
date: 2019-06-03 06:06:14
categories:
- java基础
tags:
---
## java异常相关的理解
--------------------------
1. 如何理解异常和错误？
> 首先从java类的结构上看，异常属于Exception的分支，而错误属于Error的分支。Exception和Error都继承自Throwable这个类。
> 从异常的类型角度分析，我们可以认为Exception是checked exception，而Error是unchecked exception。虽然这么说并不严谨，因为运行时异常作为异常的一部分其实也是unchecked exception。
> 参考[checked-and-unchecked-exceptions-in-java](http://www.hacktrix.com/checked-and-unchecked-exceptions-in-java)

2. 如何理解NoClassDefFoundError和ClassNotFoundException?
> 从异常的类型看，前者是unchecked exception，因此不需要try/catch或者throws。后者是checked exception是需要try/catch或者throws，否则编译不通过。
> 从异常的导致的原因分析，两者都是由于JVM在classpath中无法定位指定的class引起的。
> + 如果你在J2EE开发中遇到NoClassDefFoundError，那么最有可能的原因就是存在多个类加载器和多个目标类，即我们常说的Jar包冲突——关于Jar包冲突，一般可以使用下面两种方法解决：
使用Maven Helper 这个插件，可以排除掉大部分jar包冲突；
根据命令mvn dependency:tree -Dverbose -Dincludes=:logback-classic
  + 调用Class.forName()、ClassLoader.findSystemClass()和ClassLoader.loadClass()等方法时可能会引起    java.lang.ClassNotFoundException
  + NoClassDefFoundError是链接错误，发生在链接阶段，当解析引用的时候找不到对应的类，就会抛出java.lang.NoClassDefFoundError；ClassNotFoundException是异常，发生在运行阶段。
  [参考文章](https://www.jianshu.com/p/93d0db07d2e3)
  [java-classnotfoundexception-and-noclassdeffounderror](https://www.baeldung.com/java-classnotfoundexception-and-noclassdeffounderror)

  3. 对于反应式编程(Reactive Stream),因为本身是异步的基于事件机制的而且代码堆栈不再是同步调用，如何处理异常？



