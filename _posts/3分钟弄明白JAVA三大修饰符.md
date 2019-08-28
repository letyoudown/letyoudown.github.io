3分钟弄明白JAVA三大修饰符

JAVA的三个修饰：static,final,abstract，在JAVA语言里无处不在，但是它们都能修饰什么组件，修饰组件的含义又有什么限制，总是混淆。所以来总结对比一下。

1 static静态修饰符

static修饰符能够修饰属性，方法，初始代码块。不能修饰局部变量和类。
首先要明白属性分为静态和非静态，静态的称为静态属性，又叫类变量，非静态的称为实例变量。
静态变量和静态方法统称为静态成员。

修饰属性
静态属性又称类变量，它不属于某个对象，是属于类的，是所有对象共同享有。
eg：类名.静态属性 =对象1.静态属性=对象2.静态属性=同一块内存里所对应的地址
修饰方法
1：静态方法可以直接类名.方法名调用。
2：静态方法里只能:访问静态成员，不能访问非静态成员。
3：静态方法里不能用this关键字。
4：静态法法里没有多态，只能被静态方法覆盖。

修饰初始代码块
static修饰初始代码块称为静态代码块。静态代码块是在类加载的时候运行。这里回顾一下类加载。


类加载：
//TestPerson .java
 class Person{ 
     static{
          System.out.println("static here");
     }
     public Person(){
          System.out.println("构造方法");
     }
}
public class TestPerson(){
     public static void main(){
         Person p1 = new Person();
         Person p2 = new Person(); 
     }
}
运行 TestPerson .java文件会编译生成TestPerson .class 和 Person.class两个class文件。
执行java  TestPerson 首先会启动JAVA虚拟机(JVM),然后再硬盘上找到TestPeson.calss文件，并开始解释执行，
此时JVM里只有TestPerson.class这一个类的信息，顺序执行到main方法，遇到，Person p1 = new Person(),
创建Person对象，JVM会根据CLASSPATH环境变量找到Person.class文件，把Person类的信息读入到JVM里，
保存起来。这个过程就是类加载。
类加载：加载类信息；
             执行静态代码块；
             为静态属性分配空间并初始化值。
以上例子的执行顺序结果如下：
static here 
构造方法
构造方法

2final修饰符
final修饰符能够修饰变量，方法，和类。


final修饰变量
final修饰的变量称为常量，一旦赋值不能更改。对于基本类型来说是其值不能改变，对于对象类型来说是其址不能改变。
final变量的赋值说明：一般的实例变量在创建时JVM会给其分配空创建默认值。但是final变量只能有一次赋值机会，所以，对于final变量，JVM不会为其赋值，唯一的赋值机会留给程序员。
final类型的实例变量赋值在1：初始化属性，
2：调用构造方法，两种方式必须抓住其中一次机会，但不能试图抓住两种机会。
final修饰方法
final修饰方法，表示该方法不能被子类覆盖。
eg：class A{ public final void a1（）{.....}}
class B extends A{public void  a1(.....)}
//编译错误无法覆盖
final修饰类
final修饰类表示该类不能被继承
一个类中有final方法，该类可以被继承，但无法覆盖final方法，但一个类是final类，则该类不能被继承，更无从谈起覆盖。

eg:final赋值
class Person {
     final int num = 10 ; //初始化属性
     public Perosn(int num){
         this.num = num; 
     }
}
class Person {
     final int num ; 
     public Perosn(int num){//构造方法赋值
         this.num = num;
     }
}
class Person {
     final int num = 10;    // 错误，两种方式都抓住
     public Perosn(int num){//错误，两种方式都抓住
         this.num = num;
     }
}


3 abstract修饰符
abstract可以修饰类和方法，

abstract修饰类
abstract修饰类称为抽象类。抽象类只能用来声明引用不能用来创建对象。从某种意义上来说，抽象类就是让子类去继承，抽象类声明引用，让这个引用指向子类。子类去实现抽象方法。
抽象类中可以有非抽象方法，但一个类里有抽象方法就一定要是抽象类。子类继承抽象类要么自己成为抽象类，要么实现父抽象类里的所有抽象方法。
abstract修饰方法
abstract修饰方法，称为抽象方法。抽象方法指：只有声明没有实现的方法。
public abstract void  a1();//抽象方法。
public void a1(){};//空实现的方法

abstract class A{
         public void a1(){}//抽象类中可以有非抽象方法
         public abstract void a2();//但有了抽象方法就一定要是抽象类
}
class B extends A{
     public void a2(){
         System.out.print("子类要么是抽象类，要么实现父抽象类所有的抽象方法"); 
     }
}

public class TestA{
     public static void main(){
         A a ;//正确，抽象类可以用来引用
          a = new A();//错误，A抽象类，抽象类不能用来创建对象
          a = new B();//正确
          a.a2();//正确
     }
}

抽象类最大的作用就是，定义功能，具体实现由子类实现。
其充分体现了共性放在父类，这个基本原则里。抽象和多态是联系紧密的，其思想大家可以参考JAVA三大特性
--------------------- 
作者：尼古拉斯_张三 
来源：CSDN 
原文：https://blog.csdn.net/zhangdongxu999/article/details/70950334 
版权声明：本文为博主原创文章，转载请附上博文链接！