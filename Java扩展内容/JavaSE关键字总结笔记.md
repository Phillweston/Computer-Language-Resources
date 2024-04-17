![image-20230814155420145](https://s2.loli.net/2023/08/14/wqSQEOFuztl6vHA.png)

# Java关键字总结

我们在JavaSE阶段中学习了几乎所有的Java关键字（剩余关键字我们在SE路线的其他篇章中介绍过）这里，我们来对这些关键字进行一次详细的总结。

在Java中（截止Java17版本）目前一共有53个关键字、2个保留字、3个特殊常量，总共58个关键字，这里我们分为下面的几大类来进行总结。

## 数据类型（10个）

基本数据类型包括四个整数类型：`int`、`long`、`short`、`byte`，两个浮点类型：`float`、`double`，一个字符类型：`char`，还有一个比较特殊的`boolean`类型，它们的所占空间大小为：

- byte 字节型 （8个bit，也就是1个字节）范围：-128~+127
- short 短整形（16个bit，也就是2个字节）范围：-32768~+32767
- int 整形（32个bit，也就是4个字节）最常用的类型：-2147483648 ~ +2147483647
- long 长整形（64个bit，也就是8个字节）范围：-9223372036854775808 ~ +9223372036854775807
- float 单精度浮点型 （32bit，4字节）
- double 双精度浮点型（64bit，8字节）
- char 字符型（16个bit，也就是2字节，它不带符号）范围是0 ~ 65535
- boolean 布尔型（大小依不同JVM实现决定）

当然，某些时候我们的方法可能没有返回值，此时我们需要使用`void`类型来表示无返回值：

```java
public void test(){
    
}
```

在 Java 10 版本之后，新增一个`var`关键字来自动进行类型推断：

```java
public static void main(String[] args) {
    // String a = "Hello World!";   之前我们定义变量必须指定类型
    var a = "Hello World!";   //现在我们使用var关键字来自动进行类型推断，因为完全可以从后面的值来判断是什么类型
}
```

以上10个关键字都是数据类型相关的关键字。

***

## 特殊常量（3个）

在Java中，有着三个特殊常量值，首先就是`boolean`类型：

* `true`  -  真
* `false`  -  假

布尔类型只有两个值，要么是真要么是假，没有其他的情况，因此我们一般在进行流程判断时就会使用到布尔类型值作为判断依据。

当然，除了基本数据类型会存在特殊常量，引用类型同样存在：

* `null`   -   表示空，不引用任何对象

当一个引用类型变量的值为null时，访问对象任意属性和方法时都会出现空指针异常，因为此时并没有引用任何一个对象。

***

## 流程控制（10个）

流程控制语句相关的关键字也是非常多的，首先是分支语句：`if`、`else`、`switch`、`case`，这四个关键字是我们在分支条件中会常常用到的：

```java
if (condition) {
    
} else {
    
}
```

有些时候我们也需要循环语句来完成一些批量操作，我们可以使用`for`、`while`、`do`这三个关键字来实现循环结构：

```java
do {
    
} while (condition);
```

对于分支和循环，我们还会对其进行进一步地控制，比如加速循环或是跳出循环等，我们会用到：

* `break`   -    用于跳出循环、结束switch中的case块。
* `continue`   -   用于加速循环的进行。

我们也可以使用`return`关键字来结束整个方法：

```java
public static void main(String[] args) {
    return;
}
```

它的作用有：

* 直接结束当前方法
* 返回方法的运行结果（返回值）

以上10个关键字都是用于流程控制的。

***

## 访问控制（6个）

首先我们需要介绍一下`final`关键字，这个关键字的用途很多：

* 将变量声明为常量，首次赋值后无法被修改（无论是基本类型还是引用类型）
* 将类表明为终态，此类将无法被继承。
* 将方法表明为终态，此方法将无法被重写。

接着是三个权限修饰符：`public`、`private`、`protected`，不同的权限修饰符决定了外部对当前内容的访问权限：

|           | 当前类 | 同一个包下的类 | 不同包下的子类 | 不同包下的类 |
| :-------: | :----: | :------------: | :------------: | :----------: |
|  public   |   ✅    |       ✅        |       ✅        |      ✅       |
| protected |   ✅    |       ✅        |       ✅        |      ❌       |
|   默认    |   ✅    |       ✅        |       ❌        |      ❌       |
|  private  |   ✅    |       ❌        |       ❌        |      ❌       |

我们可以使用`package`关键字来表明当前类所处的包：

```java
package com.test;

public class Main {
  
}
```

对于非同包下的类或是非默认导入包下的类，我们需要使用`import`关键字进行导入之后才可以使用：

```java
import java.util.Arrays;

public class Main {
    public static void main(String[] args) {
        Arrays.asList();
    }
}
```

以上6个关键字是与访问控制相关的关键字。

***

## 类与对象（16个）

首先，如果我们要声明一个新的类型，肯定是要用到`class`关键字的，它主要有两个功能：

* 声明一个新的类型。
* 获取类的Class对象（基本类型和引用类型都有对应的Class对象）

```java
public static void main(String[] args) {
    Class<String> clazz = String.class;   //任意类型都可以直接.class来获取对应的Class对象
    System.out.println(clazz.getName());
}
```

我们可以使用`new`关键字直接调用类的构造方法进行对象创建：

```java
public static void main(String[] args) {
    Object o = new Object();
}
```

我们可以使用`this`关键字来表示当前对象本身：

* 表示当前对象本身。
* 在类内部使用当前类对象的属性。
* 在类内部调用当前类对象的方法。
* 调用当前类的构造器。
* 表示外部类的对象属性和方法。

同样的，如果我们需要使用父类定义的内容，可以使用`super`关键字：

* 在类内部使用父类的属性。
* 在类内部调用父类的方法。
* 调用父类的构造器。
* 表示外部类的父类属性和方法。

当我们需要将一个类作为抽象类时，可以为其添加`abstract`关键字：

* 将类型声明为抽象类，抽象类可以具有抽象方法。
* 将方法声明为抽象方法，不需要实现方法体，而是交给子类实现。

```java
abstract class Test {
    abstract void hello();
}
```

我们可以使用`extends`关键字来指明继承关系，但是只能继承一个类：

```java
public class Main extends Number{

}
```

对于接口的定义，我们可以使用`interface`关键字：

```java
public interface Cloneable {
  	
}
```

当我们实现接口时，就需要使用`implements`关键字：

```java
public class Main implements Cloneable {
  
}
```

特别的，我们可以为接口中的抽象方法添加默认实现，需要添加`default`关键字：

```java
default Stream<E> stream() {
    return StreamSupport.stream(spliterator(), false);
}
```

这个关键字有两个作用：

* 为接口中的抽象方法添加默认实现。
* 为switch语句指定其他分支。

当我们要判断某个对象是否为某个类型或是某个类型/接口的实现时，可以使用`instanceof`关键字：

```java
public static void main(String[] args) {
    Object obj = "你干嘛哎哟";
    System.out.println(obj instanceof String);
}
```

对于类中的属性，我们可以将其声明为`static`静态的，表示这些属性是属于类的，而不是对象：

```java
public static <T> List<T> asList(T... a) {
    return new ArrayList<>(a);
}
```

```java
public static void main(String[] args) {
    Arrays.asList("AAA");   //类属性可以直接通过类名.进行使用
}
```

我们还可以使用`enum`关键字来定义枚举类型：

```java
public enum Status{
    HAPPY, SAD
}
```

在Java14中，新增了记录类型，我们可以直接使用`record`关键字创建一个记录类型：

```java
public record Account(String username, String password) {  //直接把字段写在括号中

}
```

Lombok的噩梦来了。

在Java17中，正式新增了密封类型，密封类的作用就是**限制类的继承**，包含三个新的关键字`sealed`、`non-sealed`、`permits`。

```java
public sealed class A permits B{   //在class关键字前添加sealed关键字，表示此类为密封类型，permits后面跟上允许继承的类型，多个子类使用逗号隔开

}
```

只允许我们自己写的类继承A，但是不允许别人写的类继承A，就可以像上面这样实现了。

以上关键字都是我们在面向对象中认识的。

***

## 异常处理（6个）

当我们要抛出异常时，可以直接使用`throw`关键字：

```java
public static void main(String[] args) {
    throw new RuntimeException();
}
```

我们也可以将需要外部处理的异常通过`throws`关键字列出：

```java
public void test() throws IOException, ReflectiveOperationException {
    
}
```

对于异常的处理，我们可以使用`try-catch`语句块来完成：

```java
public static void main(String[] args) {
    try (FileInputStream stream = new FileInputStream("hello.txt")){
        
    } catch (IOException e){
        e.printStackTrace();
    }
}
```

对于那些无论是否发生异常都必须要在最后执行的内容，我们可以使用`finally`语句块：

```java
public static void main(String[] args) {
    try (FileInputStream stream = new FileInputStream("hello.txt")){
		
    } catch (IOException e){
        e.printStackTrace();
    } finally {
        System.out.println("我必须执行！");
    }
}
```

我们还介绍了`assert`断言语句，当后面的条件不满足时，会直接抛出错误：

```java
public static void main(String[] args) {
    assert 1 == 1;
}
```

以上都是异常处理中会使用到的一些关键字。

***

## 多线程（2个）

在多线程环境下，同步问题显得尤为重要，我们可以使用`synchronized`关键字，来添加同步代码块或是同步方法：

```java
public static void main(String[] args) {
    synchronized (Main.class) {
        
    }
}
```

只有获取到对应的锁之后，才能进入到同步代码块中，这样同一时间只能有一个线程执行这段代码。

我们在JUC篇中讲解了一个新的关键字`volatile`，这个关键字是用于保证可见性的，我们之前说了，如果多线程访问同一个变量，那么这个变量会被线程拷贝到自己的工作内存中进行操作，而不是直接对主内存中的变量本体进行操作，下面这个操作看起来是一个有限循环，但是是无限的：

```java
public class Main {
    private static int a = 0;
    public static void main(String[] args) throws InterruptedException {
        new Thread(() -> {
            while (a == 0);
            System.out.println("线程结束！");
        }).start();

        Thread.sleep(1000);
        System.out.println("正在修改a的值...");
        a = 1;   //很明显，按照我们的逻辑来说，a的值被修改那么另一个线程将不再循环
    }
}
```

虽然我们主线程中修改了a的值，但是另一个线程并不知道a的值发生了改变，所以循环中依然是使用旧值在进行判断，因此，普通变量是不具有可见性的。

此时我们可以使用`volatile`关键字来解决，此关键字的第一个作用，就是保证变量的可见性。当写一个`volatile`变量时，JMM会把该线程本地内存中的变量强制刷新到主内存中去，并且这个写会操作会导致其他线程中的`volatile`变量缓存无效，这样，另一个线程修改了这个变时，当前线程会立即得知，并将工作内存中的变量更新为最新的版本。

它的功能如下：

* 保证变量的可见性。
* 防止指令重排序。
* 不保证原子性。

***

## 其他（5个）

这里需要介绍一个我们从来没有介绍过的关键字`strictfp`，它的使用频率极低，这个关键字作用很简单：

* strictfp可以保证浮点数运算的精确性，而且在不同的硬件平台会有一致的运行结果。

一旦使用了strictfp来声明一个类、接口或者方法时，那么所声明的范围内Java的编译器以及运行环境会完全依照浮点规范IEEE-754来执行。因此如果想让浮点运算更加精确，而且不会因为不同的硬件平台所执行的结果不一致的话，那就可以使用关键字strictfp来解决，而在Java17之后直接调整为始终严格，所有这里我们只做了解就行。

我们在讲解Object类时，会发现有一些方法添加了`native`关键字：

```java
@IntrinsicCandidate
public native int hashCode();
```

可以看到这种方法时没有方法体的，也就是说没有实现，而真正的实现是由C/C++编写的，我们在JVM篇中有详细介绍，各位小伙伴如果感兴趣的话可以去看看。

此外，我们在学习IO时认识了对象流，我们可以让类实现序列化接口，并将类序列化为二进制数据存放到文件中，当时我们说，如果不希望某个属性被序列化，就可以添加`transient`关键字：

```java
public class Main {
    transient String name;
}
```

Java中还有两个保留字，目前没有任何作用，但是就是有：`goto`、`const`

————————————————
版权声明：本文为柏码知识库版权所有，禁止一切未经授权的转载、发布、出售等行为，违者将被追究法律责任。
原文链接：https://www.itbaima.cn/document/tsrkqvb6zpmtwh0n