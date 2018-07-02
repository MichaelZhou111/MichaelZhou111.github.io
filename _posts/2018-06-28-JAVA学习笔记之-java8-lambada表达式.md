---
layout: post
title: 这些概念你不懂的话，你好意思说你懂java?
date:  2018-06-29 11:15:06
tags: JAVA笔记    lambada    函数式编程 

---

## 一：lambada表达式
>说起java8的新特性，很多人第一反应都是lambada表达式和流式的API，那么到底什么是lambada表达式，为什么要引入lambada表达式，以及引入lambada表达式为
>java8带来了哪些改变呢，本文接来下会一一讨论。
 
### 1. Definition: 什么是lambada表达式？
直白的先让大家有个第一印象，在java8之前，在创建一个线程的时候，我们可能这么写：
```java
Runnable r = new Runnable() {
    @Override
  public void run() {
        System.out.println("Hello");
  }
};
```
这段代码使用了匿名类，Runnable 是一个接口，这里new 了一个类实现了 Runnable 接口，然后重写了 run方法，run方法没有参数，方法体也只有一行打印语句。
这段代码我们其实只关心中间打印的语句，其他都是多余的。
java8后，我们采用lambada表达式后，我们就可以简写为：

```java
Runnable r = () -> System.out.println("Hello");
```

Lambda 表达式是一种匿名函数(对 Java 而言这并不完全正确，但现在姑且这么认为)，简单地说，它是没有声明的方法，也即没有访问修饰符、返回值声明和名字。

你可以将其想做一种速记，在你需要使用某个方法的地方写上它。当某个方法只使用一次，而且定义很简短，使用这种速记替代之尤其有效，这样，你就不必在类中费力写声明与方法了。

### 2. lambaba表达式的语法
lambda 表达式的语法格式如下：
> (parameters) -> expression
  或
  (parameters) ->{ statements; }
  
*  一个 Lambda 表达式可以有零个或多个参数
*  参数的类型既可以明确声明，也可以根据上下文来推断。例如：(int a)与(a)效果相同
*  所有参数需包含在圆括号内，参数之间用逗号相隔。例如：(a, b) 或 (int a, int b) 或 (String a, int b, float c)
*  空圆括号代表参数集为空。例如：() -> 42
*  当只有一个参数，且其类型可推导时，圆括号（）可省略。例如：a -> return a*a
*  Lambda 表达式的主体可包含零条或多条语句
*  如果 Lambda 表达式的主体只有一条语句，花括号{}可省略。匿名函数的返回类型与该主体表达式一致
*  如果 Lambda 表达式的主体包含一条以上语句，则表达式必须包含在花括号{}中（形成代码块）。匿名函数的返回类型与代码块的返回类型一致，若没有返回则为空

以下是lambada表达式的一些例子：
```java
(int a, int b) -> {  return a + b; }

() -> System.out.println("Hello World");

(String s) -> { System.out.println(s); }

() -> 42

() -> { return 3.1415 };

```
### 3. 为什么java 会需要lambada 表达式？
Java 是一流的面向对象语言，除了部分简单数据类型，Java 中的一切都是对象，即使数组也是一种对象，每个类创建的实例也是对象。
在 Java 中定义的函数或方法不可能完全独立，也不能将方法作为参数或返回一个方法给实例。

在Java的面向对象的世界里面，“抽象”是对数据的抽象，而“函数式编程”是对行为进行抽象，在现实世界中，数据和行为并存，程序也是如此。
所以java8中lambada表达式的出现也就弥补java在对行为进行抽象方面的缺失。


## 二：函数式接口
### 1、Definition: 什么是函数式接口？
函数式接口(Functional Interface)是Java 8对一类特殊类型的接口的称呼。 这类接口只定义了唯一的抽象方法的接口（除了隐含的Object对象的公共方法），
 因此最开始也就做SAM类型的接口（Single Abstract Method）。
 
 首次看到这个概念的时候，有些迷茫。因为接口中的方法都是public abstract 的（即便省略掉这两个关键字也是ok的，接口中每一个方法也是隐式抽象的,接口中的方法会被隐式的指定为 public abstract（只能是 public abstract，其他修饰符都会报错）），那么上面的定义就变成了：只有一个方法声明的接口就是函数式接口。
 但是实际上在代码中看到的函数式接口有包含一个方法的，也有包含多个方法的，这就让我迷茫了。
 例如下面的两个函数式接口：Runnable 和 Consummer:
 
#### Runnable:
```java
@FunctionalInterface
public interface Runnable {
    /**
     * When an object implementing interface <code>Runnable</code> is used
     * to create a thread, starting the thread causes the object's
     * <code>run</code> method to be called in that separately executing
     * thread.
     * <p>
     * The general contract of the method <code>run</code> is that it may
     * take any action whatsoever.
     *
     * @see     java.lang.Thread#run()
     */
    public abstract void run();
}

```

<!--  ![Runnable](/images/posts/Runnable.png) -->

#### java.util.function.Consummer:
```java
@FunctionalInterface
public interface Consumer<T> {

    /**
     * Performs this operation on the given argument.
     *
     * @param t the input argument
     */
    void accept(T t);

    /**
     * Returns a composed {@code Consumer} that performs, in sequence, this
     * operation followed by the {@code after} operation. If performing either
     * operation throws an exception, it is relayed to the caller of the
     * composed operation.  If performing this operation throws an exception,
     * the {@code after} operation will not be performed.
     *
     * @param after the operation to perform after this operation
     * @return a composed {@code Consumer} that performs in sequence this
     * operation followed by the {@code after} operation
     * @throws NullPointerException if {@code after} is null
     */
    default Consumer<T> andThen(Consumer<? super T> after) {
        Objects.requireNonNull(after);
        return (T t) -> { accept(t); after.accept(t); };
    }
}
```
 
 <!-- ![java.util.function.Consummer](/images/posts/Java.util.function.Consummer.png) -->
 
 最后才了解了原因在于：函数式接口中除了那个抽象方法外还可以包含静态方法和默认方法。
 + Java 8以前的规范中接口中不允许定义静态方法。 静态方法只能在类中定义。 Java 8中可以定义静态方法。
 一个或者多个静态方法不会影响SAM接口成为函数式接口。
 + Java 8中允许接口实现方法， 而不是简单的声明， 这些方法叫做默认方法，使用特殊的关键字default。
 因为默认方法不是抽象方法，所以不影响我们判断一个接口是否是函数式接口。
 
 >参考链接: [Java 8函数式接口functional interface的秘密](http://colobu.com/2014/10/28/secrets-of-java-8-functional-interface/ 'Java 8函数式接口functional interface的秘密')
 
 
### 2、Brief introduction: 函数式接口简介
 为什么会单单从接口中定义出此类接口呢？ 
 原因是在Java Lambda的实现中， 开发组不想再为Lambda表达式单独定义一种特殊的Structural函数类型，
 称之为箭头类型（arrow type）， 依然想采用Java既有的类型系统(class, interface, method等)， 原因是增加一个结构化的函数类型会增加函数类型的复杂性，
 破坏既有的Java类型，并对成千上万的Java类库造成严重的影响。 权衡利弊， 因此最终还是利用SAM 接口作为 Lambda表达式的目标类型。
 
 函数式接口代表的一种契约， 一种对某个特定函数类型的契约。 在它出现的地方，实际期望一个符合契约要求的函数。 
 Lambda表达式不能脱离上下文而存在，它必须要有一个明确的目标类型，而这个目标类型就是某个函数式接口。
 换句话说：什么地方可以用lambada表达式呢？ 所有需要FI (Functional Interface)实例的地方，都可以使用lambada表达式。
 
 Java 不会强制要求你使用@FunctionalInterface注解来标记你的接口是函数式接口， 然而，作为API作者，
  你可能倾向使用@FunctionalInterface指明特定的接口为函数式接口， 这只是一个设计上的考虑， 可以让用户很明显的知道一个接口是函数式接口。
 
### 3、Why: 为什么会有函数式接口?
 说起函数式接口的起因就不得不提lambada表达式，说起lambada表达式的起因就不得不说函数式编程，函数式编程相比命令式编程有诸多的优点：（最突出的优点有2点：
 引用透明-->函数的运行部依赖于外部的状态；没有副作用-->函数的运行不改变外部的状态），java8为了使用函数式编程的优点，从而就使用了lambada表达式，从而
 就定义了一种规范和约束，这个规范和约束就是函数式接口。
 关于函数式编程的一些基础概念会在下面将。（注意：函数式编程和函数式接口是不同的概念。函数式编程是一种编程范式，与之在同一个维度的有：命令式编程、逻辑式编程）
 
 ### 4、What: java8里面的函数式接口都有哪些？

#### JDK8 之前已经有的函数式接口
* java.lang.Runnable
* java.util.concurrent.callable
* java.awt.event.ActionListener
这里就列举这几个，还有其他的暂时就不列举了。  

#### JDK8 新定义的函数式接口

|接口	|参数	|返回类型|	描述|
| --------   | -----:   | :----: |:----: |
|Predicate<T>	|T	|boolean	|用于判别一个对象。比如求一个人是否为男性|
| Consumer<T>	 | T	 | void	 | 用于接收一个对象进行处理但没有返回，比如接收一个人并打印他的名字 | 
| Function<T, R>	 | T	 | R	 | 转换一个对象为不同类型的对象 | 
| Supplier<T> | 	None | 	T	 | 提供一个对象 | 
| UnaryOperator<T> | 	T	 | T	 | 接收对象并返回同类型的对象 | 
| BinaryOperator<T>	 | (T, T)	 | T | 	接收两个同类型的对象，并返回一个原类型对象 | 

> + 其中 Cosumer 与 Supplier 对应，一个是消费者，一个是提供者。
> + Predicate 用于判断对象是否符合某个条件，经常被用来过滤对象。
> + Function 是将一个对象转换为另一个对象，比如说要装箱或者拆箱某个对象。
> + UnaryOperator 接收和返回同类型对象，一般用于对对象修改属性。BinaryOperator 则可以理解为合并对象。

如果以前接触过一些其他 Java 框架，比如 Google Guava，可能已经使用过这些接口，对这些东西并不陌生。


## 三：函数式编程
### 1、编程范式
1. 命令式编程（Imperative Programming）: 专注于”如何去做”，这样不管”做什么”，都会按照你的命令去做。解决某一问题的具体算法实现。
2. 函数式编程（Functional Programming）：把运算过程尽量写成一系列嵌套的函数调用。
3. 逻辑式编程（Logical Programming）：它设定答案须符合的规则来解决问题，而非设定步骤来解决问题。过程是事实+规则=结果。

> 关于这个问题也有一些争议，有人把函数式归结为声明式的子集，还有一些别的七七八八的东西，这里就不做阐述了。 
  声明式编程：专注于”做什么”而不是”如何去做”。在更高层面写代码，更关心的是目标，而不是底层算法实现的过程。 
  如， css, 正则表达式，sql 语句，html，xml… 
  
### 2、函数式编程简介
相比于命令式编程关心解决问题的步骤，函数式编程是面向数学的抽象，关心数据（代数结构）之间的映射关系。函数式编程将计算描述为一种表达式求值。

在狭义上，函数式编程意味着没有可变变量，赋值，循环和其他的命令式控制结构。即，纯函数式编程语言。
+ Pure Lisp, XSLT, XPath, XQuery, FP
+ Haskell (without I/O Monad or UnsafPerformIO)
在广义上，函数式编程意味着专注于函数
+ Lisp, Scheme, Racket, Clojure
+ SML, Ocaml, F#
+ Haskell (full language)
+ Scala
+ Smalltalk, Ruby

### 3、“函数”概念的不同！
函数式编程中的函数，这个术语不是指命令式编程中的函数，而是指数学中的函数，即自变量的映射（一种东西和另一种东西之间的对应关系）。
也就是说，一个函数的值仅决定于函数参数的值，不依赖其他状态。

在函数式语言中，函数被称为一等函数（First-class function），与其他数据类型一样，作为一等公民，处于平等地位，可以在任何地方定义，在函数内或函数外；
可以赋值给其他变量；可以作为参数，传入另一个函数，或者作为别的函数的返回值。

纯函数是这样一种函数，即相同的输入，永远会得到相同的输出，而且没有任何可观察的副作用。
+ 不依赖外部状态
+ 不改变外部状态

### 4、函数式编程的好处
函数式的最主要的好处主要是不变性带来的：

#### 4.1 引用透明（Referential transparency）
引用透明（Referential transparency），指的是函数的运行不依赖于外部变量或”状态”，只依赖于输入的参数，任何时候只要参数相同，
引用函数所得到的返回值总是相同的。

其他类型的语言，函数的返回值往往与系统状态有关，不同的状态之下，返回值是不一样的。这就叫”引用不透明”，很不利于观察和理解程序的行为。

没有可变的状态，函数就是引用透明（Referential transparency）

#### 4.2 没有副作用（No Side Effect）
 副作用（side effect），指的是函数内部与外部互动（最典型的情况，就是修改全局变量的值），产生运算以外的其他结果。
 
 函数式编程强调没有”副作用”，意味着函数要保持独立，所有功能就是返回一个新的值，没有其他行为，尤其是不得修改外部变量的值。
 
 函数即不依赖外部的状态也不修改外部的状态，函数调用的结果不依赖调用的时间和位置，这样写的代码容易进行推理，不容易出错。这使得单元测试和调试都更容易。
 
 还有一个好处是，由于函数式语言是面向数学的抽象，更接近人的语言，而不是机器语言，代码会比较简洁，也更容易被理解。
 
#### 4.3 无锁并发
 没有副作用使得函数式编程各个独立的部分的执行顺序可以随意打乱，（多个线程之间）不共享状态，不会造成资源争用(Race condition)，
 也就不需要用锁来保护可变状态，也就不会出现死锁，这样可以更好地进行无锁（lock-free）的并发操作。
 
 尤其是在对称多处理器（SMP）架构下能够更好地利用多个处理器（核）提供的并行处理能力。
 
#### 4.4  惰性求值
惰性求值（lazy evaluation，也称作call-by-need）是这样一种技术：是在将表达式赋值给变量（或称作绑定）时并不计算表达式的值，
而在变量第一次被使用时才进行计算。

这样就可以通过避免不必要的求值提升性能。
 
 
 总而言之，函数式编程由于其不依赖、不改变外部状态的基本特性，衍生出了很多其他的有点，尤其简化了多线程的复杂性，提升了高并发编程的可靠性。
 
### 参考资源
 * [Java 8函数式接口functional interface的秘密](http://colobu.com/2014/10/28/secrets-of-java-8-functional-interface/) 
 * [函数式编程介绍](https://blog.csdn.net/u013007900/article/details/79104110) 
 * [深入浅出 Java 8 Lambda 表达式](http://blog.oneapm.com/apm-tech/226.html)