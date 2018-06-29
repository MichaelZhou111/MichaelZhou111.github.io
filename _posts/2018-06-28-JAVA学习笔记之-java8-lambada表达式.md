---
layout: post
title: 这些概念你不懂的话，你好意思说你懂java?
date:  2018-06-29 11:15:06
tags: JAVA笔记    lambada    函数式编程    闭包

---

## lambada
### 1. Define: 什么是lambada表达式？


## 函数式接口
### 1、Define: 什么是函数式接口？
函数式接口(Functional Interface)是Java 8对一类特殊类型的接口的称呼。 这类接口只定义了唯一的抽象方法的接口（除了隐含的Object对象的公共方法），
 因此最开始也就做SAM类型的接口（Single Abstract Method）。
 
 首次看到这个概念的时候，有些迷茫。因为接口中的方法都是public abstract 的（即便省略掉这两个关键字也是ok的，接口中每一个方法也是隐式抽象的,接口中的方法会被隐式的指定为 public abstract（只能是 public abstract，其他修饰符都会报错）），那么上面的定义就变成了：只有一个方法声明的接口就是函数式接口。
 但是实际上在代码中看到的函数式接口有包含一个方法的，也有包含多个方法的，这就让我迷茫了。
 例如下面的两个函数式接口：Runnable 和 Consummer:
 <br>Runnable:<br>
 ![Runnable](/images/posts/Runnable.png)

 <br>Consummer:<br>
  ![java.util.function.Consummer](/images/posts/Java.util.function.Consummer.png)
 
 最后才了解了原因在于：函数式接口中除了那个抽象方法外还可以包含静态方法和默认方法。
 Java 8以前的规范中接口中不允许定义静态方法。 静态方法只能在类中定义。 Java 8中可以定义静态方法。
 一个或者多个静态方法不会影响SAM接口成为函数式接口。
 Java 8中允许接口实现方法， 而不是简单的声明， 这些方法叫做默认方法，使用特殊的关键字default。
 因为默认方法不是抽象方法，所以不影响我们判断一个接口是否是函数式接口。
 
 >参考链接: [Java 8函数式接口functional interface的秘密](http://colobu.com/2014/10/28/secrets-of-java-8-functional-interface/ 'Java 8函数式接口functional interface的秘密')
 
