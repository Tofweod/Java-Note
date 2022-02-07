# 面向对象编程OOP

面向对象直观理解<https://blog.csdn.net/ThinkWon/article/details/100667386>

## 类与对象

==对象是类的具体实例==

类的5大成员:
​	属性
​	方法
​	构造器
​	代码块
​	内部类

## 继承  Extends

说明：它是一种子类继承父类的特征和行为，使得子类对象（实例）具有父亲的实例域和方法，或子类从父类继承方法，使得子类具有父类相同的行为。

**创建子类实例时，先调用父类构造器默认super();再调用子类构造器**

本人易错----==super 与this在构造器的使用==

==注意this使用时所指对象==

## Override&Overload

Override 子类重写父类方法，不能重写父类属性；

==当需要在子类中调用父类的被重写方法时，要使用 super 关键字==

实例：

```java
class Animal{
   public void move(){
      System.out.println("动物可以移动");
   }
}

class Dog extends Animal{
   public void move(){
      super.move(); // 应用super类的方法
      System.out.println("狗可以跑和走");
   }
}
```

**方法查找机制**

从子类向父类查找，知道Object或者方法访问权限不够报错（找到但是访问不了即停止查找）

==使用super则直接从子类的父类开始查找==

Overload 是在一个类里面，方法名字相同，而参数不同。返回类型可以相同也可以不同

注意

- ==被重载的方法可以改变返回类型==
- ==被重载的方法可以改变访问修饰符(可扩充)==
- ==无法以返回值类型作为重载函数的区分标准==

## ==多态==

### 多态存在的三个必要条件

- 继承

- 重写

- 父类引用指向子类对象：Parent p = new Child();

### ==动态绑定机制==
（附：<https://blog.csdn.net/dlaugust/article/details/120577643>)

原理：
1.当调用方法时，方法会跟对象的运行类型绑定
2.当调用属性时，没有对象绑定机制，哪里声明哪里使用

注：对象的初始化存在==编译类型==（编译器管理）和==运行类型==（运行器管理）

编译类型决定能调用哪些方法，运行类型决定实际从哪个方法开始调用

### 向下转型和向上转型

向上转型：将子类转化为父类

实例：

```java
public class UpAndDown {
	public static void main(String[] args) {
		// 向上转型：将父类引用指向子类对象
		Father f = new Son();
		f.sleep();//输出“爸爸睡觉”
      
        //如果f.p();编译出错，不可执行。因为p()不是Father的方法
```

应用:

​	假设Person有个dance()跳舞方法。
​	Man extends Person      Women extends Person
​	此时Man和Women都重写了Person的dance();
​	当 Person p = new Man(); p.dance(); //这个时候就是调用男人跳舞的dance方法
​	当 Person p = new Woman(); p.dance();// 这个时候就是调用女人的跳舞的dance方法	

向下转型：将父类转化为子类

语法：子类类型 引用名 = （子类类型）父类引用；

实例：

```java
public class UpAndDown {
	public static void main(String[] args) {
		// 向下转型
		Father f = new Son();
		((Son)f).P();//输出“儿子调皮”
	}
}
```
只能强转父类引用，不能强制父类对象

==要求父类引用必须指向当前目标类型的对象（即原先指向对象）==

***本质***

内存中，因为向上转型是父类的引用指向为子类的对象，所以，它只是指向了父类应该拥有的属性和方法，而子类的独有的方法和属性就不指向了（或者说隐藏了），当再强转到子类时。又重新指向了子类对象，那属于它的东西又恢复了

### 多态使用

 - 多态数组
 - 多态参数

## this关键字使用

1.`this`关键字可用来引用当前类的实例变量。

2.`this`关键字可用于调用当前类方法(隐式)。

3.`this()`可以用来调用当前类的构造函数。

4.`this`关键字可作为调用方法中的参数传递。

5.`this`关键字可作为参数在构造函数调用中传递。

6.`this`关键字可用于从方法返回当前类的实例。

具体分析：https://www.yiibai.com/java/this-keyword.html

## equals和==的区别即equals重写

  ==基本数据类型比值，应用数据类型比地址

  equals用于字符串比较，对象比较则是比较值（可重写为比较对象成员）

## toString

toString方法默认返回：全类名+@+hashcode十六进制

==System.out.println(对象应用) 默认输出toString方法==

toString方法常常被重写

## finalize方法

- 重写释放资源
- 对象没有任何应用被视作垃圾对象，销毁对象前调用finalize方法
- 可通过System.gc主动触发垃圾回收机制

## 类变量（静态变量）static

==类变量可直接被类调用==

jdk7及其以后类变量存放在class实例中，而class对象在GC堆中

## 类方法（静态方法）

**经典使用场景**
  当方法中不涉及任何对象相关成员，可设计为静态方法

==注意：==

- ==类方法中无this和super等与对象有关的关键字==
- ==类方法中只能访问静态变量或者静态方法==
- ==静态成员只会在类加载时执行一次==

## 代码块

无方法名，无返回值，没有参数，只有方法体

**加载类或者创建对象的时候隐式被调用**

语法：
```java
[修饰符]{
	代码
}；
```

注意：
  1.修饰符只有static
  2.static修饰为静态代码块，没有的叫非静态代码块

==代码块相当于对构造器的补充机制==，可完成初始化操作

**细节**
 1.static代码块作用时对类进行初始化，随类的加载而执行，==并且只会执行一次==
 ==2.**（类什么时候被加载）**==

   - 创建对象实例（new）
   - 创建子类对象实例，父类也会被加载
   - 使用类的静态成员时

 3.普通代码块被创建一次就调用一次，只是使用类的静态成员则不会执行
 4.静态代码块和金泰属性初始化调用优先级一样，按定义顺序调用（普通代码块和普通方法同理）
 5.构造器最前面隐藏了两个语句
```java
class A{
	public A(){
		super();
		//调用普通代码块
	}
}
```

 ==**6.调用顺序**==
   1.父类静态代码块和静态属性
   2.子类静态代码块和静态属性
   3.父类普通代码块和普通属性初始化
   4.父类构造器
   5.子类普通代码块和普通属性初始化
   6.子类构造器
 7.静态代码块只能调用静态成员

## final关键字

final类不能被继承，final方法不能被重写，final属性、变量不能被修改

**final属性定义时必须初始化**

final类中的方法没必要修饰成final方法

final和static搭配使用==不会导致类的加载==

包装类和String类都是final类型

## 抽象类 Abstract

**详解<https://blog.csdn.net/wei_zhi/article/details/52736350>**

使用:父类某些方法需要声明,但不确定如何实现,将方法声明为抽象方法,这个类就是抽象类

使用原则:
- 抽象方法必须为public或者protected,缺省情况下默认为public
- 抽象类不能直接实例化，需要依靠子类采用向上转型的方式处理
- 子类（如果不是抽象类）则必须覆写抽象类之中的全部抽象方法（如果子类没有实现父类的抽象方法，则必须将子类也定义为为abstract类。）
- 抽象类里可以有具体方法

## ==接口 interface==

使用方法：
```java
interface 接口名 {
	//属性
	//方法
}
class 类名 implements 接口名 {
	//自己属性
	//自己方法
	//必须实现的接口抽象方法
}
```


接口可以提高代码的规范性

接口中属性均为==public static final==的（必须初始化）

jdk8后接口类可以有方法的具体实现

接口修饰符只能是public和默认

抽象类实现接口可以不实现接口方法

接口同样具有多态（==接口引用可指向实现了该接口的类的对象实例==）

==**接口和继承区别**==（附<https://blog.csdn.net/qq_39350172/article/details/108970220>)

 1.继承价值在于解决代码的复用性和可维护性

  接口假值在于设计好各种规范（方法），让其他类去实现

 2.接口更为灵活

 3.在接口中只能定义全局常量，和抽象方法，而在继承中可以定义属性方法，变量，常量等

## 内部类

==Q:为什么要使用内部类？==
1.增强封装，把内部类隐藏在外部类当中，不允许其他类访问这个内部类
2.增加了代码一个维护性
3.内部类可以直接访问外部类当中的成员

**内部类最大特点：直接访问私有属性**

### 局部内部类

 定义在外部类的局部位置，通常在方法中

 不能使用访问修饰符==（局部变量不能使用访问修饰符）==，但可用final

 只能在定义的方法或代码块中使用

 外部类和局部内部类成员重名，默认就近原则，可用==外部类名.this.成员==去访问（外部类     名.this就是**调用了内部类所在方法**的外部类对象）

### ==匿名内部类==
讲解<https://www.jianshu.com/p/0950c6787c7d>

- 本质是类
- 内部类
- 该类无名字
- ==同时还是一个对象==

定义在外部类的局部位置，通常在方法中

**匿名内部类的作用其实就是在==类不用实现接口的情况下==快速写一个接口的实例化，该实例只使用一次**

基本语法：
```java
new 类或接口（参数列表） {
	类体
};
```

以接口IA为例:

```java
IA ia = new IA(); //编译类型为IA，运行类型为匿名内部类
//底层存在代码: class 匿名内部类名 implements IA { }
//jdk在底层创建匿名内部类，立即创建了该类对象实例，并把地址返回给ia
```

匿名内部类使用一次就不能再使用，但其对象可反复使用

```java
public class AnonymousInnerClass {
    public static void main(String[] args) {
        Outer04 outer04 = new Outer04();
        outer04.method();
        Outer04 outer01 = new Outer04();
        outer01.method();
    }
}

interface IA {
    void cry();
}

class Outer04 {
    private int n1 = 10;
    public void method() {
        IA tiger = new IA() {
            @Override
            public void cry() {
                System.out.println("小老虎嗷嗷嗷....");
            }
        };
        tiger.cry();
        System.out.println(tiger);
    }
}
//运行结果
/*小老虎嗷嗷嗷....
com.Anonymouse.Outer04$1@43a25848
小老虎嗷嗷嗷....
com.Anonymouse.Outer04$1@3ac3fd8b
*/
//匿名内部类的两次底层创建的类名相同，都为Outer04$1，但是hashCode发生了变化
//之前创建的Outer04$1已经在返回地址给对象之后消失，但对象可以多次使用
```

注：getClass（）可以获得对象的运行类型

==匿名内部类new一个类注意是否有大括号{}==（其本质则是继承了new类的子类）

new一个类时的输入形参会传递给所new类的构造器，匿名内部类无构造器

==外部其他类不能访问匿名内部类==

==应用：匿名内部类可当作实参直接传递==

### 成员内部类

定义在外部类的成员位置，无static修饰

可以添加任意访问修饰符

外部类使用成员内部类：new内部类对象，使用其相关成员

外部其他类访问成员内部类 
- Outer.Inner inner = outer.==new== Inner; (outer为Outer实例对象)
- Outer类创建方法返回Inner类的对象实例

同名访问同样遵循就近原则

### 静态内部类

定义在外部类成员位置，有static修饰

可以直接访问外部类所有私有成员，不能访问非静态成员

外部类访问静态内部类: Inner inner = new Inner();

外部其他类访问静态内部类
- new Outer.new Inner();
- 创建方法返回静态内部类对象实例

## 枚举

枚举时一组常量的集合，只包含有限的特定的对象

- **自定义类实现枚举**

1.构造器私有化（防止直接new对象）
2.去掉set方法（防止属性被修改）(根据需求)
3.在类的内部创建固定的public final static对象

- **enum关键字实现枚举**

1.使用关键字enum替代class
2.对象名（构造器参数）；
3.如果有多个常量（对象），使用“，”间隔即可，最后一个带“；”
==4.使用enum实现枚举要求定义常量对象写在最前面==

使用enum创建一个类，默认继承Enum类（cmd内javap可以反编译class文件）

使用无参构造器创建枚举对象，实参列表和小括号可以省略

- **Enum相关方法**

toString方法返回name

name方法返回枚举对象名

ordinal方法返回该枚举对象的次序**（从0开始编号）**

values方法返回枚举类名数组，含有定义的左右枚举对象

==注：增强for循环==

```java
int[] nums = {1,2,3};
//普通for循环
for (int i = 0; i < nums.length; i++) {
	System.out.println(nums[i]);
}
//增强for循环
for(int i : nums) {//依次从nums数组取出元素赋给i直至取出完毕
	System.out.println(i);
}
```

valueOf方法将字符串转换为枚举对象，要求字符串必须为已有枚举对象名，否则报异常

compareTo方法比较两个枚举常量，比较的是编号（ordinal返回值）,**返回值为self.ordinal-other.ordinal**（ordinal为ordinal方法返回值）

enum类不能继承，但是可以实现接口

## 注解 Annotation

**@interface是注解类**

用于修饰解释 包，类，方法，属性，构造器，局部变量等数据信息

注解不影响程序逻辑，但可以被编译或者运行，相当于嵌入在代码中的补充信息

- @Override：限定某个方法，是重写父类方法，只能用于方法
- @Deprecated：用于表示某个程序元素（类，方法，字段，包，参数等）已过时
- @SuppressWarnings：抑制编译器警告

@Override 让编译器检测方法是否真的重写了父类方法，若没有重写则编译错误

@Deprecated 修饰只表示过时，即不在推荐使用，但可以使用
该注释用于新旧版本的兼容过渡

@SuppressWarnings({"希望抑制的警告信息"})，存在作用范围

元注解：用于修饰注解的注解

# 异常 Exception

## 异常介绍

程序执行中发生的不正常情况称为**异常**

异常事件可分为两大类：
1.Error（错误）——严重错误，程序崩溃
2.Exception:
		1.运行异常[]
		2.编译异常[]

## ==异常体系图==

<img src="https://img-blog.csdnimg.cn/20190514085517638.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L01hY1d4,size_16,color_FFFFFF,t_70" alt="img" style="zoom: 200%;" />

### 五大运行时异常

1.NullPointerException空指针异常——程序试图在需要对象的地方使用null
2.ArithmeticException数学运算异常——出现异常的运算条件
3.ArrayIndexOutOfBoundsException数组下标越界异常
4.ClassCastException类型转换异常——试图将对象强制转换为不是实例的子类（向下转型时与原先指向对象不匹配）
5.NumberFormatException数字格式不正常异常——当应用程序试图将字符串转换成一种数值类型，但该字符串不能转换为适当格式

### 编译异常

在编译期间就必须处理的异常，否则编译不通过

常常与网络，数据库，文件操作IO有关

### 自定义异常

程序中出现的错误信息没有在Throwable子类中描述处理，可自己设计异常类

自定义异常类名-继承RuntimeException（运行异常）或Exception（编译异常）

一般情况，自定义异常继承RuntimeException，可使用默认throws异常处理

## 异常处理机制

不应该出现一个非致命错误导致程序崩溃的现象——异常处理机制

### try-catch-finally异常处理机制

```java
int num2 = 0;
//快捷键 ctrl + alt + t
try{ 
	int res = num1 / num2; //如果存在问题就捕获
} catch (Exception e) {
	e.printStackTrace(); //异常处理方法
}
```

无论是否异常，finally内代码块均要执行，故通常将释放资源的代码放在finally中

try或catch中有return，**先执行finally**，再执行return

异常发生时后面代码块不会执行，直接进入catch中

可以有多个catch处理try中不同的可能异常，其中子类异常在前，父类异常在后

存在try-finally——应用场景：执行一段代码，无论是否异常，都必须执行某个业务逻辑，其本质并未处理异常，finally之后程序仍会崩溃/退出

实际案例：
```java
// 需求;如果用户输入不是一个整数，提示其反复输入直至正确输入
public class Test {
    public static int getNum() {
        int num;
        Scanner scanner = new Scanner(System.in);
        while (true) {
            System.out.println("请输入一个整数");
            try {
                num = Integer.parseInt(scanner.next());
                break;
            } catch(NumberFormatException e) {
                System.out.println("输入有误");
            }
        }
        return num;
    }

    public static void main(String[] args) {
        System.out.println(Test.getNum());
    }
}
```

### throws异常处理机制

如果一个方法中可能生成某种异常，throws表面该方法不处理异常，而由方法的调用者负责处理

在方法声明中throws语句可以声明抛出异常列表（即多个异常），throws后异常类型可以是其父类

**注意**

- 对于编译异常，try-catch-finally和throws必须二选一
- 对于运行异常，如果没有显式使用异常处理，**默认用throws**
- **JVM处理异常机制**——输出异常信息，并退出程序
- 子类重写父类方法时，子类抛出异常要么和父类抛出异常一致，要么为父类抛出异常的子类

## throws和throw区别

- 简概表

|        | 意义                                | 位置       | 所跟内容     |
| :----: | :---------------------------------- | ---------- | ------------ |
| throws | 异常处理的一种方式                  | 方法声明处 | ==异常类型== |
| throw  | 手动生成异常对象的关键字（==new==） | 方法体中   | ==异常对象== |

# 常用类

## 包装类 Wrapper

1.针对八种基本数据类型相应的引用类型——包装类
2.具有类的特点，可以调用类中方法

**包装类类型**
- Boolean --- boolean

- Character --- char 

   ----

- Byte --- byte

- Integer --- int

- Long --- long

- Short --- short         

- Float --- float

- Double --- double
<a href="https://sm.ms/image/JLUZXSRy4GMalDC" target="_blank"><img src="https://i.loli.net/2021/10/17/JLUZXSRy4GMalDC.png" ></a>

### 装箱和拆箱

装箱：基本数据类型 -> 包装类型，反之为拆箱 

**以int和Integer为例**

1.jdk5以前手动装箱和拆箱
2.jdk5及其以后自动装拆箱，底层调用valueOf方法

手动装，拆箱：
```java
// 装箱
int n1 = 100;
Integer integer1 = new Integer(n1); //方法1
Integer integer2 = Integer.valueOf(n1); //方法2
// 拆箱
int i = integer1.intValue();
```

自动装，拆箱
```java
// 装箱
int n1 = 100;
Integer integer = n1; //底层使用的是 Integer.valueOf(n1)方法
// 拆箱
int n2 = integer; //底层使用intValue()方法
```

**其他包装类的用法类似**

==易错==：

```java
Object obj1 = true? new Integer(1) : new Double(2);
System.out.println(obj1);
/*
输出结果为1.0
三元运算符看作为一个整体，double精度更高，int自动转换了
*/
```

### 包装类型和String类型相互转换

**以Integer和int为例**

包装类 -> String
```java
Integer integer = 100;//自动装箱
//方式1
String str1 = i + "";//对integer类型无影响
//方式2
String str2 = integer.toString();
//方式3
String str3 = String.valueOf(integer);
```

String -> 包装类
```java
String str = "123";
//方法1
Integer i1 = Integer.parseInt(str);//自动装箱
//方法2
Integer i2 = new Integer(str);//构造器
```

==**包装类里方法很多且复杂，想真正学懂需要仔细阅读源码**==

## String类

String对象用于保存字符串，即一组字符序列，==存储在常量池中==

字符串的字符使用Unicode字符编码，一个字符占两个字节

继承关系：<a href="https://sm.ms/image/k9i1h4nWJVzsq6e" target="_blank"><img src="https://i.loli.net/2021/10/17/k9i1h4nWJVzsq6e.png" ></a>

**实现Serializable接口：String可以串行化（序列化）（String实例可以在网络上传输）
实现Comparable接口：String对象可以相互比较大小**

String类实现了构造器重载
常用构造器：

```java
String();
String(String ordinal);
String(char[] a);
String(char[] a,int startIndex,int count);
String(byte[] b);
```

String中有属性 private final char value[ ]（注：数组也是对象），用于存储字符串内容,value 是final类型，赋值后==地址==不能修改**(String所有操作中产生的字符串都相当于一个匿名对象，它们都被真实的创建出来)**
附：https://blog.csdn.net/guyuealian/article/details/50935168

**String对象两种创建方式**

1.直接赋值 String s = '"hsp";
2.调用构造器 String s = new String("hsp");

- 方法1先从常量池查看是否有“hsp”数据空间，如果有则直接指向；如果没有则重写创建，然后指向；s最终指向的是==常量池的空间地址==
- 方法2先在堆中创建空间，里面维护了value属性，指向常量池“hsp”空间。如果常量池没有“hsp”，则重新创建；如果有，则直接通过value指向。最终指向的是==堆中的空间地址==
<a href="https://sm.ms/image/McNQZdkEmhOwvJD" target="_blank"><img src="https://i.loli.net/2021/10/17/McNQZdkEmhOwvJD.png" ></a>

==重要==
String对象特征
例1：

```java
String s1 = "hello";
s1 = "hi";
//与常量池中创建了2个字符串对象
```

例2：
```java
String s = "hello" + "abc" //底层优化，等价于 String s = "helloabc";
```

例3：
```java
String a = "hello";
String b = "abc";
/*
 *1.先创建 StringBuilder sb = new StringBuilder();
 *2.执行 sb.append("hello");
 *3.执行 sb.append("abc");
 *4.执行 sb.toString(); return new String(value,0,count)
 *最终 c 指向堆中String对象的value[]属性(也即是对象)
 *value[] -> 常量池中“helloabc”对象
 */
String c = a + b;
// 字符串变量拼接字符串常量同理
```

**intern()方法**

当调用intern方法时，如果池已经包含与equals(Object)方法确定的相当于此String对象的字符串，则返回来自池的字符串。 否则，此String对象将添加到池中，并返回对此String对象的引用。 

理解
```java
String s = new String("123");
// String s2 = “123”; 加上这句为false
System.out.println(s == s.intern());
/*
 *当s为栈对象时当常量池中有“123”对象返回false 
 *反之为true
 *System.out.println(s2 == s2.intern())为true
 */
```

String常用方法

- charAt：获取某索引处的字符(str.charAt(index))，==字符串不能用Str[index]来索引==
- equals：判断内容是否相等，equalsIgnoreCase方法忽略大小写
- indexOf：获取字符在字符串对象中第一次出现的索引，从0开始，找不到返回-1
- lastIndexOf：获取字符在字符串对象中最后一次出现的索引（第一个字符）
- substring：截取指定范围的子串——substring(0,5)表示从0开始截取，直到索引为5-1
- toUpperCase,toLowerCase：大小写
- format 格式化字符串：参考C语言格式化IO

## StringBuffer

### 继承关系
![继承关系](https://obohe.com/i/2021/10/20/ytg9ay.png)
1.在StringBuffer的父类AbstractStringBuilder中有属性char[] value(不是==final==)，用于存储字符串内容，因此存放在堆中
2.StringBuffer是final类

StringBuffer里面的值可以更改，其更新实际上可以更新内容；除非空间不够，**不用每次更新地址**（即创建新对象），故效率更高

#### 构造器
1.StringBuffer(),初始容量为16
2.StringBuffer(CharSequence seq):构造一个字符串缓存区，包含与指定CharSequence相同的字符
3.StringBuffer(int capacity):通过构造器指定char[]大小（即容量）
4.StringBuffer(String str):通过str创建StringBuffer

### StringBuffer和String转换

String ->  StringBuffer
```java
//方式1 使用构造器
String str = "hello";
StringBuffer stringBuffer = new StringBuffer(str);// 对str没有影响
//方式2 append
StringBuffer stringBuffer = new StringBuffer();
StringBuffer strBuffer = stringBuffer.append(str);
```


 StringBuffer ->  String
```java
 //方式1
 String s1 = stringBuffer.toString();
 //方式2
 String s2 = new String(stringBuffer);
```


### StringBuffer常用方法

1.append：增添
2.delete：删除——`str.delete(int start,int end)`删除s字符串[start,end)的字符
3.replace：替换——`str.replace(int start,int end."替换内容")`替换s字符串[start,end)的字符，替换字符串长度可大于替换范围
4.insert：插入——`str.insert(int index,"插入内容")`，原来索引为index的内容自动后移

## StringBuilder

### 继承关系
![](https://obohe.com/i/2021/10/20/114y1k1.png)

### 使用事注意事项

一个可变的字符序列,提供与StringBuffer兼容API,但存在线程安全问题.被设计用作StringBuffer的简易替换,==用在字符串缓存区被单个线程使用时==

StringBuilder主要操作是append和insert方法

StringBuilder和StringBuffer方法一样

StringBuilder是final类

==字符序列任然存储在其父类的char[] value中==

### **String,StringBuffer和StringBuilder比较**

1.StringBuffer和StringBuilder非常类似
2.String:不可变字符序列,复用率高
3.StringBuffer:可变字符序列,效率较高,线程安全
4.StringBuilder:可变字符序列,效率最高,线程不安全

结论:如果对String做大量修改,不要使用String

**使用原则**:
1.如果字符串存在大量修改,一般使用StringBuffer或StringBuilder
2.如果字符串很少修改,被多个对象引用,使用String,如配置信息等

## Math类

**Math类方法均为静态**

常用方法：
1.abs：绝对值
2.pow：求幂
3.ceil，floor：向上，向下取整（返回double）
4.round：四舍五入 <=> `Math.floor(参数+0.5)` (返回long)
5.sqrt：开方
6.random：求随机数，返回[0，1）之间的随机小数

## Arrays类

用于管理或操作数组

常用方法：
1.`Arrays.toString`: 返回数组的字符串形式

```java
 Integer[] integer = {1,2,3};
 System.out.println(integer.toString);
```

2.sort:排序

```java
Integer arr[] = {1,-1,,7,0};
//可以使用冒泡排序
//也可以使用Arrays提供的sort方法
Arrays.sort(arr);
System.out.println(arr.toString);
//sort方法已重载，可通过传入接口Comparator实现定制排序
Array.sort(arr,new Comparator(){//匿名内部类
    @Override 
    public int compare(Object o1,Object o2) {
        Integer i1 = (Integer)o1;
        Integer i2 = (Integer)o2;
        return i2 - i1;//返回值>0,<0影响排序结果
    }
});
```

3.binarySearch:二分搜索进行查找，要求已经排序好——返回index索引，不存在返回`-(low+1)`,**low为元素应该存在时的索引**

4.copyOf:数组元素复制,若拷贝长度大于数组长度，在新数组后面增加0(int数组)或null(对象数组)；若拷贝长度<0，抛出异常NegativeArraySizeException

5.fill:数组元素填充——可以理解为替换原数组所有元素

6.equals:比较两个数组元素是否完全一致

7.asList:将一组值转换为list

```java
List aslist = Arrays.asList(1,2,3);
//aslist的编译类型是List，运行类型是Arrays$ArrayList（内部类）,即视图对象
```
**注**:
java中的视图，可以说其实就是一个具有限制的集合对象.
这里的asLIst是一个视图对象，具有==访问数组元素==set，get的方法。但是如果调用==改变数组的方法==就会抛出异常。所以可以说视图对象可以说是具有限制的集合对象。

## System类

常见方法：
1.exit:退出当前程序,`exit(参数)`，其实0表示正常退出
2.arraycopy:复制数组元素，比较适用于底层调用（Arrays.copyOf的底层就是调用arraycopy）

```java
System.arraycopy(src,srcPos,dest,desPos,length);
/*
*src      the source array.
*srcPos   starting position in the source array.
*dest     the destination array.
*destPos  starting position in the destination data.
*length   the number of array elements to be copied.
*/
// 拷贝长度不能大于被拷贝内容长度
```

3.currentTimeMilens:返回当前时间距离1970-1-1的毫秒数
4.gc:运行垃圾回收机制——`System.gc()`

## BigInteger&BigDecimal

引用场景：
1.BigInteger适合保存较大的整型
2.BigDecimal适合保存精度更高的浮点型

### BigInteger

`BigInteger bigInteger = new BigInteger("较大数");`

对bigInteger对象进行运算时不能直接加减乘除，须使用对应方法：
- add 加
- subtract 减
- multiplay 乘
- divide 除

实例：
```java
BigInteger bigInteger = new BigInteger("较大数");
bigInteger.add(int num or BigInteger b);// 其余方法同理
```

### BigDecimal

需要保存精度很高的数据时double不够用，引入`BigDecimal`

使用与BigInteger同理

使用divide时可能出现无线循环小数抛出异常，故在调用divide方法时可以指定精度
`BigDecimal.subtract(num,BigDecimal.ROUND_CEILING);` **保留到分子的精度**
具体使用：<https://blog.csdn.net/wumingdu1234/article/details/104475150>

==BigDecimal都是不可变的（immutable）的，在进行每一步运算时，都会产生一个新的对象，所以在做加减乘除运算时千万要保存操作后的值==

## 日期类

### Date

Date：精确到毫秒，代表特定的瞬间（这里的Date是`java.util`里的，注意不要和`java.sql.Date`混淆）

实现了Cloneable接口，可以实现克隆操作

SimpleDateFormat：格式化和解析日期的具体类

使用：

<img src="https://obohe.com/i/2021/10/23/12aflek.png" style="zoom: 50%;" />

```java
Date d1 = new Date(); //获取当前时间
// 格式化d1 格式化使用字母已规定好
SimpleDateFormat sdf = new SimpleDateFormat("yyyy年MM月dd日 hh:mm:ss E");
String format = sdf.format(d1);

Date d2 = new Date(long );//通过指定毫秒数得到时间

String s = "1990年01月01日 10:20:30 星期一";
Date parse =sdf.parse(s);//默认格式,且要处理ParseException异常
/*
 *String -> Date时
 *使用的sdf格式需要和String格式一样
 *否则抛出ParseException异常
*/
```


### Calendar

Calendar类是public abstract的

**Calendar构造器私有化，须用getInstance方法创建对象实例**

为特定瞬间与YEAR,MONTH,DAY_OF_MONTH,HOUR等日历字段(**均为static final**）之间的转换提供方法，并为操作日历字段提供方法

（注：字段（Field）又称为成员变量,是定义在类中，方法体之外的变量，保活类变量）

使用：
```java
Calendar c = Calendar.getInstance();
//获取日历对象的某个日历字段	
c.get(Calendar.YEAR)
c.get(Calendar.MONTH)+1 //Calendar返回月时按0开始编号，故需要加1
// HOUR是12进制，HOUR_OF_DAY则是24进制
```

Calendar没有提供对应的格式化类，需要自己组合进行输出

### 第三代日期（jdk8）

Date和Calendar存在问题：
1.可变性：日期和时间的类本应不可变
2.偏移性：Date中年份从1990年开始，而月份都是从0开始
3.格式化：Calendar没有格式化的类
4.Date和Calendar不是线程安全的
5.不能处理闰秒（每隔两天，多出1s）

第三代日期对象创建
1.LocalDate：获取日期（年月日）
2.LocalTime：获取时间（时分秒）
3.LocalDateTime：获取日期时间

使用：
```java
// 用now()返回表示当前日期时间的对象
LocalDateTime ldt = LocalDateTime.now();
// 获得字段
ldf.getYear(); //其余同理
// DateTimeFormat 对象进行格式化
DateTimeFormat dtf = DateTimeFormat.ofPattern(格式);
String str = dtf.format(日期时间对象);
```


### Instant

Instant 时间戳

类似于Date，可以和Date类相互转换

使用：
```java
Instant now = Instant.now();
// 格式化

// Instance —> Date
Date date = Date.from(now);
// Date -> Instance
Instant instant = date.toInstant();
```

# 集合

## 集合体系图

单列集合
![](https://obohe.com/i/2021/10/26/xzlqs.png)
Collection接口有两个重要子接口 List    Set，它们实现子类都是单列集合

双列集合
![]()
Map接口的实现子类是双列集合，存放的是K-V

## Collection接口

### 特点
1.Collection实现子类可以存放多个元素，每个元素可以是Object
2.有些Collection实现类可以存放重复元素，有些不行
3.有些Collection实现类，有些是有序的（List），有些是无序的（Set）
4.Collection接口没有直接的实现子类，是通过子接口List和Set实现的

### 常用方法

1.add：会将add的元素转换为**对象**
2.remove：通过index删除（返回boolean）或指定元素删除（返回被删除的对象）
3.cotains:查找元素是否存在
4.size：获取元素个数
5.isEmpty：判断是否为空
6.clear：清空
7.addAll(Collection c)：添加多个元素 （只要是**实现了Collection接口的类的对象**即可）
8.containsAll(Collection c)：查找多个元素是否都存在
9.removeAll(Collection c)：删除多个元素

### 遍历元素

#### Iterator迭代器

Iterator对象称为迭代器，主要用于遍历Collection集合中的元素

所有实现了Collection接口的集合类都有一个iterator()方法，用于返回一个实现了Iterator接口的对象

Iterator结构：
![](https://obohe.com/i/2021/10/26/gzl216.png)
==注意：==
1.next()方法返回的是**Object（编译类型）**
2.使用next()方法前必须先调用hasNext()方法进行检测。若不调用且下一条记录无效，直接调用next()会抛出NoSuchElementException异常
3.当退出while循环后，这是iterator迭代器指向最后元素，再次调用next()方法会抛出异常
4.如果想再次遍历，需要重置迭代器，即`iterator = coll.iterator;`

Iterator仅用于遍历集合，Iterator**本身并不存放对象**

#### 增强for循环

增强for循环就是简化版的iterator，本质一样。==只能用于遍历集合或数组==

基本语法：
```java
for(元素类型 元素名 : 集合名或数组名) {
	访问元素
}
// 集合中元素不一样则元素类型使用Object
```


附：普通for循环（以List为例）
```java
for (int i = 0; i < list.size(); i++) {
	System.out.println(list.get(i));
}
```

## List接口

List集合类中元素有序（即添加顺序和取出顺序一致），且可重复

List集合支持索引

List常用实现子类
- Vector
- ArrayList
- LinkedList

常用方法：
1.`void add(int index, Object ele)`:在index位置插入ele元素
2.`boolean addAll(int index, Collection eles)`:从index位置开始将eles中所有元素添加进来
3.`Object get(int index)`:获取指定index位置的元素
4.`int indexOf(Object obj)`:返回obj在集合中**首次**出现位置
5.`int lastIndexOf(Object obj)`:返回obj在集合中**末次**出现位置
6.`Object remove(int index)`:移除指定index位置的元素，并返回此元素
7.`Object set(int index, Object ele)`:设置指定index位置的元素ele，相当于替换（索引必须存在）
8.`List subList(int fromIndex, int toIndex)`:返回从fromIndex到toIndex的 位置的子集合（前闭后开）

## ArrayList

ArrayList permits all elements included **null**

ArrayList是由数组来实现数据存储的

ArrayList基本等同于Vector，但线程不安全（执行效率高）

### ==ArrayList底层结构==

ArrrayList中维护了一个Object类型的数组elementData 即`transient Object[ ] elementData`

transient关键字，表示该属性不会被**序列化（串行化）**（允许将对象进行字节级的copy，以便网络传输或存档复用）

当创建ArrayList对象时，如果使用无参构造器，则初始elementData容量为0；第一次添加，则扩容elementData为10；如需要再次扩容，则扩容elementData为1.5倍

如果使用指定大小构造器，初始elementData容量为指定大小，扩容时按当前elementData1.5倍扩容

## Vector

Vector底层也是对象数组 `protected Object[] elementData`

Vector是线程同步,即线程安全,Vector类的操作方法都带有**synchronized**关键字

需要线程同步安全时,考虑使用Vector

Vector和ArrayList比较

|           | 底层结构 | 版本   |   线程安全    |                    扩容倍数                     |
| --------- | -------- | ------ | :-----------: | :---------------------------------------------: |
| ArrayList | 可变数组 | jdk1.2 | 不安全,效率高 | 有参构造1.5倍;无参构造:第一次10,之后按1,5倍扩容 |
| Vector    | 可变数组 | jdk1.0 | 安全,效率不高 |   有参构造2倍;无参构造:第一次10,之后按2倍扩容   |

## LinkedList 双向链表

- .LinkedList底层实现了双向==链表==和双端==队列==的特点
- .可以添加任意，重复元素
- ==线程不安全==

底层机制
1.LinkedList中维护了两个属性first和last分别指向首节点和尾节点
2.每个节点（Node对象），里面又维护了prev、next、item三个属性，其中通过prev指向前一个节点，通过next指向后一个节点。最终实现双向链表
<img src="https://obohe.com/i/2021/10/30/fkhqwq.png"  />
3.LinkedList元素的==添加和删除==，不是通过数组完成，效率较高
4.LinkedList中也有CRUD方法(add,remove,set,get等)

**ArrayList和LinkedList比较**

|            | 底层结构 | 增删效率      | 改查效率 |
| :--------: | -------- | ------------- | -------- |
| ArrayList  | 可变数组 | 数组扩容,较低 | 较高     |
| LinkedList | 双向链表 | 链表追加,较高 | 较低     |

1.如果改查操作多,选择ArrayList
2.如果增删操作多,选择LinkedList

## Set接口

基本介绍
1.无序（添加和取出顺序不一致）
2.不允许重复元素，最多包含一个null
3.常见实现类：HashSet，LinkedHashSet，TreeSet等

常用方法
Set是Colleciton子接口，常用方法和Colection接口一样

遍历方式
1.可以使用迭代器
2.增强for
3.==不能使用==索引的方式获取

## HashSet

==HashSet的底层就是HashMap==,HashMap的底层是(数组+链表+红黑树)

HashSet底层机制:
```java
class Node {
	Object item;
	Node next; // 可以指向下一个节点
	
	public Node(Object item, Node next) {
		this.item = item;
		this.next = next;
	}
}

public class Strcuture {
	public static void main(String[] args) {
		// 1.创建一个数组,类型为Node[]
		// 2.Node[] 也称为表
		Node[] table = new Node[16];
		// 创建节点
		Node john = new Node("john", null);
		table[2] = john; // 在数组中存放链表
		Node jack = new Node("jack", null);
		john.next = jack; // 将jack结点挂载到john
		Node rose = new Node("rose", null);
		jack.next = rose;
		Node lucy = new Node("lucy", null);
		table[3] = lucy;
		// 目的:高效
		}
	}
}
```

HashSet添加元素机制:
1.HashSet底层是HashMap
2.添加元素时,先得到hash值-会转为->索引值(==hash值不同的元素一定可以加入==)
3.找到存储数据表table.判断索引位是否已存放元素
4.如果没有,直接加入
5.如果有,调用equals方法(**可重写**).如果相同,放弃添加,如果不同,添加在最后
6.在java8中,如果一条链表元素个数到达TREEIFY_THRESHOLD(默认位8),并且table大小>=MIN_TREEIFY_CAPACITY(默认64),就会进行树化(红黑树)

关于hashCode补充：[JAVA为什么两个不同对象的hashCode有可能相同](https://www.imooc.com/article/280528)

实践：
```java
// 1.创建3个Employee对象放入HashSet中
// 2.当name和age相同，认为是相同员工，不能添加
class Employee {
	private String name;
	private int age;
	public Employee(String name;int age) {
		this.name = name;
		this.age = age;
	}
    public String getName() {
        return name;
    }
    public int getAge() {
        return age;
    }
    // 如果name和age相同，返回相同hashcode
    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() ！= o.getClass()) return false;
        Employee employee = (Employee) o;
        return this.name == employee.getName() && this.age == employee.getAge;
    }
    @Override
    public int hashCode() {
        return Objects.hash(name, age);
        // hash()方法调用Array.hash(Object[] a)方法,返回值与a[]中每个元素的hashCode相关
    }
}
public Test {
	public static void main(String[] args) {
        HashSet hashSet = new HashSet();
        hashSet.add(new Employee("ykn", 18));
        hashSet.add(new Employee("ykn", 18)); // 此时第二个元素添加不进hashSet
	}
}
```


## LinkedHashSet

LinkedHashSet是HashSet的子类

LinkedHashSet底层是一个LinkedHashMap（是HashMap的子类），维护了一个==数组+ 双向链表==

LinkedHashSet根据元素的hashCode值决定元素存放位置，同时用链表维护元素的**次序**，使得元素看起来是以插入顺序保存的

LinkedHashSet不允许添加重复元素

## Map接口

### **Map接口实现类特点（很使用） jdk8**
1.Map与Collection没有直接关系，用于保存具有映射关系的数据：Key-Value
2.Map中的key和value可以是任何引用类型的数据，会封装到HashMap$Node[ ]（HashMap中的一个静态内部类）中
3.Map中的key不能重复——当key相同时，就等价于替换
4.Map中的value可以重复
5.Map中key可以为null，value也可以为null，但key只能有一个为null
6.常用String类作为Map的key
7.key和value之间存在一 一对应关系，即通过指定的key总能找到对应的value
8.k-v为了方便遍历，还会创建entrySet集合，存放的元素类型是Map.Entry，而一个Entry对象拥有k，v （`transient Set<Map.Entry<K,V>> entrySet`) ,**其k，v只是指向Node节点中的k，v** 
9.entrySet中，元素的编译类型是Map.Entry，但运行类型是HashMap$Node,因为Node实现了Map.Entry接口
10.创建entrySet集合目的：方便遍历Node中k，v，因为Map.Entry提供了getKey( )和getValue( )方法

### Map常见方法
1.put(K, V)：添加（可用于替换）return V
2.remove(Object key)：根据键删除映射关系 return V
3.get(Object key)：根据键获取值 return V（Object）
4.size( )：获取元素个数 return int
5.isEmpty( )：判断个数是否为0 return boolean
6.void clear( )：清除
7.containsKey(Object key)：查找键是否存在 return boolean
8.getNode(Object key)：get底层 return Node<K, V >
9.removeNode(int hash, Object key, Object value, boolean matchValue, boolean movable)：remove底层，return Node<K, V>

### Map接口遍历方法

map为实现了Map接口的HashMap实例

- containsKey：查找键是否存在
- keySet：获取所用的键,封装在Set集合中
- entrySet：获取所有关系k-v
- values：获取所有的值

第一种：
先取出所有的key，通过key取出对应value

```java
Set keyset = map.keySet();
// 增强for
for (Object key : keyset) {
	System.out.println(key + map.get(key));
}
// 迭代器
Iterator iterator = key.iterator();
while (iterator.hasNext()) {
	Object key = iterator.next();
	System.out.println(key + map.get(key));
}
```


第二种：
把所有的values取出
```java
Collection values = map.values();
// values为Collection实例，可以使用其遍历方法
```


第三种：
通过EntrySet来获取k-v
```java
Set entrySet = map.entrySet();
// 增强for
for (Object obj : entrySet) {
	//将entry转成Map.Entry
	Map.Entry entry = (Map.Entry) obj;
	System.out.println(entry.getKey() + entry.getValue());
}
// 迭代器
Iterator interator = entrySet.iterator();
while (iterator.hasNext()) {
	Object next = iterator.next();
	Map.Entry entry = (Map.Entry) next; // 向下转型+接口多态性
	System.out.println(entry.getKey() + entry.getValue());
}
```


### Map总结

1.Map接口常用实现类：HashMap，Hashtable和Properties
2.HashMap是Map接口使用频率最高的实现类
3.如果添加相同的key，则会覆盖原来的key-value，等同于修改（key不变，value变）
4.HashMap线程不安全

## HashMap

底层机制
- （k,v）是一个实现了Map.Entry<K,V>的HashMap$Node
-  底层是数组+链表+红黑数

扩容机制
1.HashMap底层的Node类型数组table（数组名），默认为null
2.创建对象时，将加载因子（loadfactor）初始化为0.75
3.**添加k-v时与HashSet一致**
4.第一次添加，需要扩容table为16，临界值（threshold）为12
5.当table元素数到达临界值进行扩容，table容量，临界值为原来两倍	

## Hashtable

基本介绍
`public class Hashtable extends Dictionary implements Map<K,V>`
1.Hashtable的k,v都不能为null，否则抛出NullPointerException异常
2.Hashtable线程安全(synchronized)

底层
1.Hashtable底层有table数组，类型为HashtableEntry[ ],初始化大小为11





# 泛型

传统方法缺陷：
1.不能对加入到集合ArrayList中的数据类型进行约束（不安全）
2.遍历时需要进行类型转换，如果集合中数据的量较大，对效率有影响

## 泛型理解

- ==泛型是一种可以表示数据类型的数据类型==
- 泛型又称参数化类型，解决数据类型的安全性问题
- 在类声明或实例化只要指定好需要的具体类型即可
- 泛型可以保证如果程序在编译时没有发出警告,运行时也不会产生ClassCastException异常
- 泛型作用:可以在类声明时通过一个标识返回类中某个属性的类型,或是某个方法的返回值类型,或是参数类型
```java
class Person<E> { // E可以指定任何类型
	E s; // 该属性类型时在创建或定义Person对象时指定,即在编译期间,就确定E是什么类型
	
	public Person(E s) { // 用E表示参数类型
	this.s = s;
	}
	
	public void f() { // 返回类型使用E
		return s;
	}
	
	public static void main (String[] args) {
		Person<String> stringPerson = new Person<String>("name"); // 指定E类型为String
		Person<Integer> integerPerson = new Person<Integer>(100); // 指定E类型为Integer
        System.out.println(stringPerson.getClass());
        System.out.println(integerPerson.getClass());
	}
}
```

## 泛型语法:

```java
// 泛型的声明
interface 接口名<T>{} 和 class 类名<K,V>{}
/**
  *说明:
  *1.T,K,V不代表值,而是表示类型
  *任意字母都可以.常用T表示,是Type缩写
  */
// 泛型的实例化--在类名后面指定类型参数的值
List<String> strList = new List<String>();
Iterator<Customer> iterator = customer.itertor();
// 泛型可以在遍历是不进行向下转型
```



### 泛型细节

1.`interface List<T>{} ，public class HashSet<E>{}`等等
  T，E只能是==引用类型==，不能是基本数据类型
2.在指定泛型具体类型后，可以传入该类型或其子类型
3.泛型使用形式
  `List<integer> list1 = new ArrayList<integer>();`
  简化形式
  `List<integer> list2 = new ArrayList<>();`
  最初写法
  `List list3 = new ArrayList();`等价于`List<Object> list3 = new ArrayList<>();`

## 自定义泛型

### 自定义泛型类

基本语法
`class 类名<T,R...> { //可以有多个泛型
	成员
}`

注意细节
1.普通成员可以使用泛型（属性，方法）
2.使用泛型数组，不能初始化(new)
3.静态方法中不能使用类的泛型（静态和类加载相关，类加载时对象还未创建）
4.泛型类的类型是在创建对象时确定的
5.如果创建对象时未指定类型默认Object

实例
```java
/**
 * 1.Tiger后是泛型，所以Tiger是自定义泛型类
 * 2.T,R,M 泛型标识符
 */
class Tiger<T,R,M> {
}
```


### 自定义泛型接口

基本语法
```java
interface 接口名<T,R...> {
}
```

注意细节
1.同自定义类
2.泛型接口的类型，在==继承接口==或==实现接口==时确定

### 自定义泛型方法

基本语法
```java
修饰符 <T,R...> 返回类型 方法名(T t, R r...) { //泛型方法中含有一个T,R类型形参
}
```

注意细节
1.泛型方法可以定义在普通类中，也可定义在泛型类中
2.当泛型方法被调用时，类型会确定
3.`public m1(E e){}` 修饰符后没有泛型标识符T, m不是泛型方法，而是使用了泛型

## 泛型的继承和通配符

泛型不具备继承
```java
List<Object> list = new ArrayList<String>(); 
// 类具有继承关系，但泛型不具有继承关系
```

`?` ： 支持任意泛型
`? extends A`：支持A类以及A类的子类，规定了泛型的上限
`? super A`：支持A类以及A类的父类，不限于直接父类，规定了泛型的下限

# JUnit

基本介绍
1.JUnit是一个java语言的单元测试框架
2.多数java的开发环境都已经集成了JUnit作为单元测试的工具

==使用@Test可以调用==

# Java绘图入门

## java坐标体系

基本介绍
坐标原点位于左上角，以==像素==为单位。
x轴水平方向，**向右为正**
y轴垂直方向，**向下为正**

==*像素是密度单位，不是长度单位*==

## 绘图入门和机制

先定义一个MyPanel类，继承JPanel类，画图就在面板上进行

```java
class MyPanel extends JPanel {
	/** 说明
	  * 1.MyPanel 对象就是一个画板（面板）
	  * 2.Graphics g 把 g 理解为一支画笔
	  * 3.Graphics 提供了很多绘画的方法
	  */
    @Override
    public void paint(Graphics g) { // 绘图方法
        super.paint(g); // 调用父类的方法完成初始化
    }
}

public class DrawCircle extends JFrame { // JFrame对应窗口，可以理解为画框
    // 定义一个面板
    private MyPanel mp;
    public static void main(String[] args) {
        new DrawCircle();
    }
    public DrawCircle() { //构造器
        // 初始化面板
        mp = new MyPanel();
        // 把面板放入到窗口（画框）中
        this.add(mp);
        // 设置窗口大小
        this.setSize(400,300);
        this.setDefaultCloseOperation(JFrame.DISPOSE_ON_CLOSE);// 关闭窗口后程序能够退出
        this.setVisible(true); // 窗口可视化
    }
}
```

绘图原理

Component类提供了两个和绘图相关最重要的方法：
1.`paint(Graphics g)`绘制组件的外观
2.`repaint()`刷新组件的外观

当组件第一次显示在屏幕时，程序会自动调用`paint()`方法来绘制组件
在以下情况`paint()`将会再次被调用
- 窗口最大化，最小化
- 窗口大小发生变化
- `repaint()`方法被调用

## Graphics类

1.画直线 `drawLine(int x1, int y1, int x2 ,int y2)`
2.画矩形边框 `drawRect(int x, int y, int width ,int height)`
3.画椭圆边框`drawOval(int x, int y, int width ,int height)`
4.填充矩形`fillRect(int x, int y, int width ,int height)`
5.填充椭圆`fillOval(int x, int y, int width ,int height)`
（注：填充方法前应设置画笔颜色 `g.setColor(Color.color)`
6.画图片`drawImage(Image img, int x, int y, int width, int height, ImageObserver observer)`

```java
// 获取图片资源
Image image = Toolkit.getDefaultToolkit().getImage(Panel.class.getResource("/文件名.后缀")); // 图片应放在该项目out的根目录中
g.drawImage(image, x, y ，width, height, observer);
```
7.画字符串`drawString(String str, int x, int y)`
```java
// 设置颜色
g.setColor(Color.red);
// 设置字体
g.setFont(new Font("行楷"，Font.BOLD(粗体), 50));
g.drawString(String str, x, y); // 坐标对应左下角
```


## Java事件处理机制

java事件处理是采取“委派事件模型”。当事件发生时产生事件的对象，会把此”信息“传递给“事件监听者”处理。

这里的“信息”实际上就是java.awt.event事件类库所创建的对象，把它称为“事件的对象”。

**事件发生和事件处理依靠==事件对象==相联系**

**相关概念**

1.事件源：产生事件的对象，比如按钮，窗口等；
2.事件：承载事件源状态时改变的对象，比如键盘使事件，鼠标事件，窗口事件等，会生成一个 事件对象，该对象保存着该事件的诸多信息。
3.事件类型：查阅jdk文档
4.事件监听器接口
   (1).当事件源产生了一个事件，可以传递给事件监听者处理
   (2).事件监听者实际上就是一个类，该类实现了某个事件监听器接口

   

# 线程（基础）

## 线程介绍 

**概念**

- 程序：是为完成特定任务，用某种语言编写一组指令集合
- 进程：进程是指运行中的程序。进程是程序的一次执行过程，或是正在进行的一个程序。是**动态过程**：有它自身产生，存在和消亡的过程
- 1.线程由进程创建的，是进程的实体
  2.一个进程可以拥有多个线程
- 单线程：同一个时刻，只允许执行一个线程
- 多线程：同一个时刻，可以执行多个线程
- 并发：同一个时刻，多个任务交替执行，造成一种==貌似同时==的错觉，简单而言，单核cpu实现的多任务就是并发
- 并行：同一个时刻，多个任务同时执行。多核cpu可以实现并行
- 并行中可包含并发
```java
// 获取cpu核数
public static void main(String[] args) {
	Runtime runtime = Runtime.getRuntime;
	int cpuNum = runtime.availableProcessors();
}
```

## 线程基本使用

### 创建线程两种方式

1.基础Thread类，重写run方法
2.实现Runnable接口，重写run方法

**关于调用start解释**

如果调用run方法，run方法为main函数中的一个方法，并未实际开辟新的线程

start则是会==调用本地start01方法==，而该方法由==jvm==调用，将线程变为可运行状态，具体什么时候执行则取决于cpu，由cpu统一调度


e.g.以三个窗口多线程出售车票为例
```java
public class SellTicket1 {
    public static void main(String[] args) {
    }

    @Test
    public void test01() {
        SellTicket01 sellTicket1 = new SellTicket01();
        SellTicket01 sellTicket2 = new SellTicket01();
        SellTicket01 sellTicket3 = new SellTicket01();
        sellTicket1.start();
        sellTicket2.start();
        sellTicket3.start();
      
    }

    @Test
    public void test02() {
        SellTicket02 sellTicket1 = new SellTicket02();
        Thread thread1 = new Thread(sellTicket1);
        Thread thread2 = new Thread(sellTicket1);
        Thread thread3 = new Thread(sellTicket1);
        thread1.start();
        thread2.start();
        thread3.start();
    }

}

// 类继承方式
class SellTicket01 extends Thread {
    private static int num = 100; // 让多个线程共享

    @Override
    public void run() {
        super.run();
        while (true) {
            if (num <= 0) {
                System.out.println("售票结束.");
                break;
            }
            try {
                Thread.sleep(50);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            System.out.println("窗口" + Thread.currentThread().getName() + "售出一张票，剩余票数=" + --num);
        }
    }
}

// 实现接口方式
class SellTicket02 implements Runnable {
    private static int num = 100;

    @Override
    public void run() {
        while (true) {
            if (num <= 0) {
                System.out.println("售票结束..");
                break;
            }
            try {
                Thread.sleep(50);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            System.out.println("窗口" + Thread.currentThread().getName() + "售出一张票，剩余票数=" + --num);
        }
    }
}
```

*注*
上例存在剩余票数为负问题
因为最后三个线程可能同时执行判断if为真，导致结果为负

## 线程终止

1.当线程完成任务后，会自动退出
2.通过使用变量控制run方法退出从而停止线程

e.g.
```java
class T extends Thread {
	// 设置一个控制变量
	private boolean loop = true;
	while (loop) {
		// 逻辑业务
	}
	
	public boolean setLoop() {
		return (loop = false);
	}
}

public class test {
	public static void main(String[] args) {
		T t1 = new T();
		t1.start();
		// main线程控制t1线程的终止,必须可以修改loop
		// 让t1退出run方法，从而终止t1线程 -> 通知方式
		
	}
} 
```

## 线程常用方法

### 第一组

1.setName 设置线程名称，使之与参数name相同
2.getName 返回该线程的名称
3.start 是该线程开始执行；==Java虚拟机底层调用的start0方法==
4.run 调用线程对象run方法
5.setPriority 更改线程优先级
6.getPriority 获取线程的优先级
7.sleep 在指定的毫秒数内让当前正在执行的线程休眠（暂定执行）
8.interrupt 中断线程

**注意事项和细节**
1.start底层会创建新的线程，调用run，run就是一个简单的方法调用，不会启动新线程
2.线程优先级的范围
     `MAX_PRIORITY = 10, MIN_PRIORITY = 1, NORM_PRIORITY = 10`
3.interrupt是中断线程，但并没有真正的结束线程。故一般用于中断正在休眠的线程，将该线程唤醒(即在catch InterruptException异常中加入业务逻辑)
4.sleep是线程静态方法

**关于[interrupt](https://blog.csdn.net/canot/article/details/51087772?spm=1001.2101.3001.6650.1&utm_medium=distribute.pc_relevant.none-task-blog-2~default~CTRLIST~default-1.no_search_link&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2~default~CTRLIST~default-1.no_search_link)的详解**

### 第二组

1.yield 线程的礼让。让出cpu，让其他线程执行，但礼让的时间不确定，所以也不一定能礼让成功
2.join 线程的插队。插队的线程一旦插队成功，则肯定先执行完插入线程的所有任务

## 用户线程和守护线程

1.用户线程：也叫工作线程，当线程的任务执行完或通知方式结束
2.守护线程：一般是为了工作线程服务，当所有的用户线程结束，守护线程自动结束
常见守护线程：垃圾回收机制

e.g.将一个线程设置为守护线程
```java
public class Test() {
	public static void main(String[] args) {
		DaemonThread dt = new DaemonThread();
		dt.setDaemon(true); // 设置dt为守护线程
		dt.start();
		for(int i = 0; i < 10; i++) {
			System.out.print("主线程运行中。。");
			Thread.sleep(1000);
		}
	}
}

class DaemonThread extends Thread {
	@Override
	public void run {
		for(;;) { // 无限循环
			try{
				Thread.sleep(50);
			}
			catch (InterruptExpection e) {
				e.printStackTrace();
			}
			System.out.print("循环中。。。");
		}
	}
}
```

**将一个线程作为守护线程用于监控其他线程或者获取其他线程信息，有利于对多线程的管理**

## 线程的生命周期

**线程状态**

- NEW
  尚未启动的线程处于此状态
-  RUNNABLE
  在JVM中执行的线程处于此状态
-  BLOCKED
  被阻塞等待前十七锁定的线程处于此状态
-  WAITING
  正在等待另一个线程执行特定动作的线程处于此状态
-  TIMED_WAITING
  正在等待另一个线程执行动作达到指定等待时间的线程处于此状态
-  TERMINATED
  已退出的线程处于此状态

## 线程同步机制

在多线程编程中，一些敏感数据不允许多个线程同时访问，此时就用同步访问技术，保证数据在任何同一时刻，==最多有一个线程访问==

线程同步，即当有一个线程在对内存进行操作时，其他线程都不可以对这个内存地址进行操作，直到该线程操作完成

### Synchronized

1.同步代码块
 `synchronized (Object obj){
 	// 需要被同步代码;
 }`
2.sychronized还可以放在方法声明中，表示某个方法为同步方法
`public synchronized void or ohters m() {
	// 需要被同步的代码块;
}`

![](https://obohe.com/i/2021/11/23/10q14sy.png)

### 互斥锁

1.Java中引入了对象互斥锁，来保证共享数据操作的完整性
2.每个对象都对应于一个可称为“互斥锁”的标记，这个标记用来保证在任意时刻只能由一个线程访问该对象
3.关键字synchronized来与对象的互斥锁联系。当某个对象用sychronized修饰，表明该对象在任意时刻只能由一个线程访问
4.同步局限性：导致程序执行效率降低
5.同步方法（非静态）的锁可以是this，也可以是其他对象（要求是同一个对象）
6.同步方法（静态）为当前对象类本身 `类.class`

注意事项
1.同步方法没有使用static修饰，默认锁对象为this
2.如果方法使用static修饰，默认对象为`当前类.class`
3.实现互斥锁方法
  - 需要先分析上锁的代码
  - 选择同步代码块（优先）或同步方法
  - ==要求多个线程的锁对象为同一个==

e.g.
```java
public class Test {
    public static void main(String[] args) {
        T t = new T();
        new Thread(t).start();
        new Thread(t).start();
        new Thread(t).start();
    }
}

class T implements Runnable {
    private int num;
    private boolean loop;

    public T() {
        num = 0;
        loop = true;
    }

    @Override
    public void run() {
        while (loop) {
            synchronized (this){
                if (num >= 100000) {
                    break;
                }
                add();
            }
        }
    }

    public void add() {
        System.out.println(Thread.currentThread().getName()
                           + "+" 
                           + ++num);
    }
}
```

### ==死锁==

**基本介绍**
多个线程都占用了对方的锁资源,但不肯相让,导致了死锁

应用案例
妈妈:你先完成作业,才让你玩手机
小明:你先让我玩手机,我才完成作业

```java
public class Deadlock {
    public static void main(String[] args) {
        // 模拟死锁现象
        DeadLockDemo deadLockDemo1 = new DeadLockDemo(true);
        DeadLockDemo deadLockDemo2 = new DeadLockDemo(false);
        deadLockDemo1.start();
        deadLockDemo2.start();
    }
}

class DeadLockDemo extends Thread {
    static Object o1 = new Object(); // 共享类对象
    static Object o2 = new Object();
    boolean flag;

    public DeadLockDemo(boolean flag) {
        this.flag = flag;
    }

    @Override
    public void run() {
        super.run();
        // 1.如果flag为真，线程a就会先得到o1对象锁，然后尝试去获取o2对象锁
        // 2.如果线程a得不到o2对象锁，就会进入BLOCKED状态
        // 3.如果flag为假，线程b就会先得到o2对象锁，然后尝试去获取o1对象锁
        // 4.如果线程b得不到o2对象锁，就会进入BLOCKED状态
        // 5.此时a,b线程均不能获得锁且释放锁,故产生死锁
        if (flag) {
            synchronized (o1) {
                System.out.println(Thread.currentThread().getName() + "进入1");
                synchronized (o2) {
                    System.out.println(Thread.currentThread().getName() + "进入2");
                }
            }
        } else {
            synchronized (o2) {
                System.out.println(Thread.currentThread().getName() + "进入3");
                synchronized (o1) {
                    System.out.println(Thread.currentThread().getName() + "进入4");
                }
            }
        }
    }
}
```

### 释放锁

==为避免死锁现象,应明确线程什么时候释放锁==

**释放锁的情况**
1.当前线程的同步方法、同步代码块执行结束
2.当前线程在同步代码块、同步方法中遇到break、return语句
3.当前线程在同步代码块、同步方法中出现了未处理的Error或Exception,导致异常结束
4.当前线程在同步代码块、同步方法中执行了线程对象的wait方法,当前线程会暂停并释放锁

**不会释放锁的情况**
1.线程执行同步代码块或同步方法时，程序调用Thread.sleep( )或Thread.yield( )方法暂停当前线程的执行，不会释放锁
2.线程执行同步代码块时，其他线程调用了该线程的suspend( )方法将该线程挂起，该线程不会释放锁
提示：尽量避免使用suspend( )和resume( )来控制线程

# IO流

## 文件

文件就是保存数据的地方

**文件流**

文件在程序中是以==流的形式==来操作的

==流：数据在数据源（文件）和程序（内存）之间经历的路径==

### 常用文件操作

- 创建文件对象相关构造器和方法
相关方法
`new File(String pathname) //根据路径构建一个File对象`
`new File(File parent, String child) //根据父目录文件+子路径构建`
`new File(String parent, String child) //根据父目录+子路径构建`

`creatNewFile` 创建新文件

- 获取文件相关信息
相关方法
`getName()` 获取文件名
`getAbsolutePath()` 获取绝对路径
`getParent` 获取文件夫级目录
`length` 获取文件大小（按字节算）
`exists` 判断文件是否存在
`isFile` 判断是否是文件
`isDirectory` 判断是否是目录

- 目录操作和文件删除（均返回boolean）
`mkdir()` 创建一级目录
`mkdirs()` 创建多级目录
`delete()` 删除==空目录==或文件

**在java中，目录也被当做文件**

### java IO流

**java IO流原理**

1.I/O是Input/Output缩写，I/O流是非常实用的技术，用于处理数据传输，如读/写文件，网络通讯等。
2.java程序中，对数据的输入/输出操作以“流（stream）”的方式进行
  ==即以流的对象操作数据io==
3.java.io包下提供了各种“流”类和接口，用于获取不同数据类型，并通过方法输入或输出数据

**流的分类**

- 按操作数据单位不同分为：字节流（8 bit），字符流（按字符）
  （字节流用于操作二进制文件，可以无损；字符流用于操作文本文件）
- 按数据流的流向不同分为：输入流，输出流
- 按流的角色的不同分为：节点流，处理流/包装流

| 抽象基类 |    字节流    | 字符流 |
| :------: | :----------: | :----: |
|  输入流  | InputStream  | Reader |
|  输入流  | OutputStream | Writer |

<img src="https://img-blog.csdnimg.cn/20190503233300304.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTAxNDUyMTk=,size_16,color_FFFFFF,t_70" style="zoom:67%;" />

## 字节流

### FileInputStream

构造器
1.`FileInputStream(String filePath)`

方法
1.`read()` 从该输入流读取一个字节的数据，如果没有输入，此方法将阻止 
          返回int，如果返回-1表示读取完毕
2.`read(byte[] b)` 从该输入流读取最多b.length字节的数据到指定字符数组，如果没有输入，此方法将阻塞，直到某些输入可用
          返回**实际读取字节数**，如果返回-1表示读取完毕


**注：**
**操作完流对象之后应该调用close( )方法关闭文件流，释放文件资源**

### FileOutputStream

```java
/** 在a.txt中写入“hello，world！”
  * 如果文件不存在，则创建文件
  */
@Test
public void write(){
    String filePath = "d:\\hello.txt";
    FileOutputStream fileOutputStream = null;
    try {
        // 得到fileOutputStream流，并创建a.txt文件
        // 构造器
        // public FileOutputStream(String name) throws FileNotFoundException 
        //     {this(name != null ? new File(name) : null, false);}
        fileOutputStream = new FileOutputStream(filePath);
        String str = "hello,world!";
        fileOutputStream.write(str.getBytes());
    } catch (IOException e) {
        e.printStackTrace();
    } finally {

        try {
            fileOutputStream.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

该创建流的方式是覆盖的，当每次运行程序写入内容时会覆盖原来内容

解决方法：
FileOutputStream有`boolean append`属性，存在`public FileOutputStream(File file, boolean append)`构造器
若append为true，则字节将被写入文件的末尾而不是开头

**文件拷贝**

思路：
1.创建文件输入流，将文件读入程序
2.创建文件输入流，将读入文件输出到指定位置
3.==应该是读取部分文件，就写入到指定文件==

```java
public class FileCopy {
    public static void main(String[] args) {
        String srcfilePath = "C:\\Users\\Lenovo\\Desktop\\yknbirth.jpg";
        String destfilePath = "C:\\Users\\Lenovo\\Pictures\\yknbirth.jpg";
        FileOutputStream fileOutputStream = null;
        FileInputStream fileInputStream = null;
        try {
            // 字节数组提高读取效率
            byte[] buf = new byte[1024];
            fileInputStream = new FileInputStream(srcfilePath);
            fileOutputStream = new FileOutputStream(destfilePath);
            int readLean = 0;
            while ((readLean = fileInputStream.read(buf)) != -1) {
                // 不能使用fileOutputStream.write(buf);
                fileOutputStream.write(buf,0,readLean);
            }
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            if (fileInputStream != null) {
                try {
                    fileInputStream.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
            if (fileOutputStream != null) {
                try {
                    fileOutputStream.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }	
        }
    }
}
```



## 字符流

### FileReader

相关方法
1.`new FileReader(File/String)` 构造器
2.`read()` 每次读取单个==字符==，返回该字符，如果到文件末尾返回-1
3.`read(char[])` 批量读取多个字符到数组中，返回读取到的字符数，如果到文件末尾返回-1
4.相关API:
   1.`new String(char[])` 将char[]转换成String
   2.`new String(char[],off,len)` 将char[]指定部分转换为String

### FileWriter

相关方法：
1.`new FileWriter(File/Strng)` 覆盖模式，相当于流的指针在首端
2.`new FileWriter(File/String)` 追加模式，相当于流的指针在末端
3.`write(int)` 写入单个字符
4.`write(char[])` 写入指定数组
5.`write(char[],off,len)` 写入指定数组的指定部分
6.`write(String)` 写入字符串
7.`write(String,off,len)` 写入字符串的指定部分
8.相关API:
   String类：toCharArray：将String转换为char[ ]

==FileWriter使用后，必须要关闭（close）或刷新（flush），否则写入不到指定的文件==（因为数据还在内存中）
**close() 等价于 flush() + 关闭**

## 节点流和处理流

[JAVA节点流和处理流](https://www.cnblogs.com/wxgblogs/p/5647415.html)

### 基本介绍

1.节点流可以从一个指定的数据源读写数据，如FileWriter，FileReader
    数据源：存储数据的地方

2.处理流（包装流）是“连接”在已存在的流（节点流或处理流）之上，为程序提供更为强大的读写功能，如BufferedReader，BufferedWriter

以BufferRead为例，该类中有属性Reader，即可以封装一个是Reader子类的节点流

3.处理流本质对节点流进行包装，使用了**修饰器设计模式**，不会直接与数据源相连

e.g.模拟修饰器设计模式
```java
public abstract class Reader_ {
	public void readFile() {}
	public void readString() {}
}

// 节点流
class FileReader_ extends Reader_{
	public void readFile() {
		// 读取文件
	}
}

// 节点流
class StringReader_ extends Reader_{
	public void readString() {
		// 读取字符串
	}
}

// 处理流
class BufferedReader_ extends Reader_{
	private Reader_ in;
	public BufferedReader_(Reader in) {
		this.in = in;
	}
    // 封装readFile方法
    public void readFile() {
        in.readFile();
    }
	// 在BufferedReader_里扩展FileReader_的业务，多次读取或添加byte[]缓冲
	public void readFiles(int num) {
		for (int i = 0; i < num; i++) {
			readFile();
		}
	}
}

class Test {
	public static void main(String[] args){
		BufferedReader_ bufferedReader_ = new BufferedReader_(new FileReader_());
 		bufferedReader_.readFiles(10);
	}
}
```

处理流功能：
1.性能提高：主要以增加缓冲的方式来提高输入输出效率
2.操作便利：处理流提供更便利发次一次性处理大批量数据

 ### BufferedReader&BufferedWriter

BufferedReader和BufferedWriter属于字符流，按==字符==来读取数据

关闭处理流时，只需关闭外层流即可

不要用该流操作二进制文件（声音，视频，doc，pdf等），可能造成文件损坏

e.g.BufferedCopy
```java
public class BufferedCopy {
    public static void main(String[] args) {
        String srcfilePath = "c:\\Users\\Lenovo\\Desktop\\note.txt";
        String destfilePath = "c:\\Users\\Lenovo\\Desktop\\note1.txt";

        BufferedReader br = null;
        BufferedWriter bw = null;
        String lines;

        try {
            br = new BufferedReader(new FileReader(srcfilePath));
            bw = new BufferedWriter(new FileWriter(destfilePath));

            while ((lines = br.readLine()) != null) {
                // 每读取一行就写入
                bw.write(lines);
                // 换行 因为readLine读取一行内容，但是没有换行符
                bw.write('\n');
            }
            System.out.println("拷贝完毕。。。");
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            // 关闭流
            try {
                if (br != null) {
                    br.close();
                }
                if (bw != null) {
                    bw.close();
                }
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
}
```


### BufferInputStream&BufferedOutputStream

























#  网络编程

## 相关概念

- 网络通信
  1.概念：两台设备之间通过网络实现数据传输
  2.网络通信：将数据通过网络从一台设备传输到另一台设备
  3.java.net包提供了一系列类或接口，完成网络通信



- 网络
  1.概念：两台或多台设备通过一定物理设备连接起来构成了网络
  2.根据网络覆盖范围不同，对网络进行分类：
  - 局域网
  - 城域网
  - 广域网
    - IP地址
      1.概念：用于唯一标识网络中的每一台计算机/主机
      2.查看ip地址：ipconfig
      3.ip地址表示形式 ==点分十进制==  xx.xx.xx.xx
         ipv4: 4个字节（32位） ，每个字节范围0—255
         ipv6: 16个字节（128位）
      4.ip地址的组成 = ==网络地址+主机地址==，比如：192.168.16.69
      5.ipv6仕用于替代ipv4的下一代ip协议，由于ipv4网络地址资源有限，ipv6的使用能解决网络地址资源数量的问题，而且也解决了多种接入设备连接互联网的障碍
      6.ipv4地址分类
         A类：0+7位网络号+24位主机号		0.0.0.0-127.255.255.255
         B类：10+14位网络号+16位主机号	128.0.0.0-191.255.255.255
         C类：110+21位网络号+8位主机号	192.0.0.0-223.255.255.255
         D类：1110+28位多播组号				  224.0.0.0-239.255.255.255
         E类：11110+27位留待后用		        240.0.0.0-255.255.255.255
         特殊的：**127.0.0.1表示本机地址**
      ​						
- 域名
  1.概念：将ip地址映射（HTTP协议）成域名 e.g. www.baidu.com 
  2.好处：为方便记忆，解决记ip的困难
- 端口号
  1.概念：用于表示计算机上某个特定的网络程序，ip+端口访问特定服务，**一个端口只能被一个服务监听**
  2.表示形式：以整数表示，范围0~65535（2字节）
  3.0~1024已经被占用，e.g. ssh-22,ftp-21,smtp-25,http-80（在网络开发中不要使用该范围端口）
  4.常见的网络程序端口号：
     - tomcat：8080
     - mysql：3306
     - oracle：1521
     - sqlserver：1433
- 网络通信协议
  协议：在网络编程中数据的组织形式 
  TCP/IP协议:传输控制协议/英特网互联协议

| OSI模型（理论） | TCP/IP模型（实际） | TCP/IP模型各层对应协议 |
| :-------------: | :----------------: | :--------------------: |
|     应用层      |       应用层       | HTTP,ftp,telnet,DNS... |
|     表示层      |                    |                        |
|     会话层      |                    |                        |
|     传输层      |    传输层（TCP)    |       TCP,UDP...       |
|     网络层      |    网络层（IP)     |     IP,ICMP,ARP...     |
|   数据链路层    |  物理+数据链路层   |          Link          |
|     物理层      |                    |                        |

- TCP和UDP
  TCP协议（传输控制协议）：
    1.使用TCP协议前，须先建立TCP连接，形成传输数据通道
    2.传输前，采用“三次握手”方式，是==可靠的==
    3.TCP协议进行通信的两个应用进程：客户端、服务端
    4.在连接中可进行大数据量的传输
    5.传输完毕，须**释放已建立的连接**，==效率低==
  UDP协议（用户数据协议）：
    1.将数据、源、目的封装成数据包，不需要连接
    2.每个数据包的大小限制在64K内，==不适合传输大量数据==
    3.因无需连接，古是不可靠的
    4.发送数据结束时无需释放资源（因为不是面向连接的），==速度快==

## InetAddress类

- 相关方法
  1.获取本机InetAddress对象 `getLocalHost`（静态方法）
  2.根据指定主机名/域名获取ip地址对象 `getByName`（静态方法）
  3.获取InetAddress对象的主机名 `getHostName`
  4.获取InetAddress对象的地址 ` getHostAddress`

## Socket

- 基本介绍
  1.套接字（Socket）开发网络应用程序被广泛采用，以至于成为事实上的标准
  2.通信的两端都要有Socket，是两台机器间通信的端点
  3.==网络通信其实就是Socket间的通信==
  4.Socket允许程序把网络连接当成一个流，数据在两个Socket间通过IO传输
  5.一般主动发起通信的应用程序称为客户端，等待通信请求的称为服务端

当我们需要通讯时（读写数据）
 1.`socket.getOutputStream()`
 2.`socket.getInputStream()`

- Socket分类
  1.TCP编程
  2.UDP编程

## TCP网络通信编程

- 基本介绍
  1.==基于客户端-服务端的网络通信==
  2.底层应用TCP/IP协议
  3.基于Socket编程

e.g.SocketTCP01.java（使用字节流）
```java
/**
 * 1.编写一个服务器端和一个客户端
 * 2.服务器端在9999端口监听
 * 3.客户端连接到服务器端，发送“hello，server！”，然后退出
 * 4.服务器端接受到客户端发送的信息，输出，并退出
 */
package SocketTCP01Server
public class SocketTCP01Server{
	public static void main (String[] args) throws IOException{
		//1.在本机的9999端口监听，等待连接
		//	细节:要求在本机没有其他服务在监听9999端口
        //  ServerSocket可以通过accept()返回多个Socket[多个客户端连接服务器的并发]
		ServerSocket serverSocket = new ServerSocket(9999);
		
		//2.当没有客户端连接9999端口时，程序会阻塞，等待连接
		//  如果有客户端连接，则会返回一个Socket对象，程序继续
		Socket socket = serverSocket.accept();
		
		//3.通过socket.getInputStream()读取客户端写入到数据通道的数据，显示
        InputStream inputStream = socket.getInputStream();
        
        //4.IO读取
        byte[] buf = new byte[1024];
        int readLen = 0;
        while ((readLen = inputStream.read(buf)) != -1) {
        	//根据读取到的实际长度显示字符串
        	System.out.println(new String(buf,0,readLen));
        }
        
        //5.关闭流和socket
        inputStream.close();
        socket.close();
        serverSocket.close();
	}
}

package SocketTCP01Client
public class SocketTCP01Client {
    public static void main(String[] args) throws IOExpeciton{
        //1.连接服务端（ip，端口）
        //解读：连接这台主机的9999端口，如果连接成功，返回Socket对象
        Socket socket = new Socket(InetAddress.getLocalHost(),9999);
        
        //2.连接上后，生成Socket，通过socket.getOutputStream()得到和socket对象			关联的输出流对象
        OutputStream outputStream = socket.getOutputStream();
        
        //3.通过输出流，写入数据到数据通道
        outputStream.write("hello,server!".getBytes());
        
        //4.关闭流对象和socket
        outputStream.close();
        socket.close();
    }
}
```


e.g.SocketTCP02.java（使用字节流）
```java
/**
 * 1.编写一个服务器端和一个客户端
 * 2.服务器端在9999端口监听
 * 3.客户端连接到服务器端，发送“hello，server！”，并接受服务器端回发的“hello，client！”，再退出
 * 4.服务器端接受到客户端发送的信息，输出，并发送“hello，client！”，退出
 */
package TCPCoding.SocketTCP02;
public class SocketTCP02Server {
    public static void main (String[] args) throws IOException{
        //1.在本机的9999端口监听，等待连接
        //	细节:要求在本机没有其他服务在监听9999端口
        //  ServerSocket可以通过accept()返回多个Socket[多个客户端连接服务器的并发]
        ServerSocket serverSocket = new ServerSocket(9998);

        System.out.println("等待客户端连接。。。");

        //2.当没有客户端连接9999端口时，程序会阻塞，等待连接
        //  如果有客户端连接，则会返回一个Socket对象，程序继续
        Socket socket = serverSocket.accept();

        //3.通过socket.getInputStream()读取客户端写入到数据通道的数据，显示
        InputStream inputStream = socket.getInputStream();

        OutputStream outputStream = socket.getOutputStream();
        outputStream.write("hello,client!".getBytes());
        //关键点
        socket.shutdownOutput();

        //4.IO读取
        byte[] buf = new byte[1024];
        int readLen = 0;
        while ((readLen = inputStream.read(buf)) != -1) {
            //根据读取到的实际长度显示字符串
            System.out.println(new String(buf,0,readLen));
        }

        //5.关闭流和socket
        inputStream.close();
        socket.close();
        serverSocket.close();
    }
}

package TCPCoding.SocketTCP02;
public class SocketTCP02Client {
    public static void main(String[] args) throws IOException {
        //1.连接服务端（ip，端口）
        //解读：连接这台主机的9999端口，如果连接成功，返回Socket对象
        Socket socket = new Socket(InetAddress.getLocalHost(),9998);

        //2.连接上后，生成Socket，通过socket.getOutputStream()得到和socket对象			关联的输出流对象
        OutputStream outputStream = socket.getOutputStream();

        InputStream inputStream = socket.getInputStream();
        byte[] buf = new byte[1024];
        int readLen = 0;
        while((readLen = inputStream.read(buf)) != -1) {
            System.out.println(new String(buf,0,readLen));
        }

        //3.通过输出流，写入数据到数据通道
        outputStream.write("hello,server!".getBytes());

        //4.关闭流对象和socket
        outputStream.close();
        socket.close();
    }
}
```

==注意==：
  socket在发送完一个数据时应有一个结束标记，即`socket.shutdownOutput()`
  `socket.shutdownOutput()`——写入结束标记

附:[socket.shutdownOutput()理解]([socket.shutdownOutput()的理解_u011403239的博客-CSDN博客_socket.shutdownoutput](https://blog.csdn.net/u011403239/article/details/113806772))



e.g.SocketTCP03.java（使用字符流）
```java
/**
 * 1.编写一个服务端，一个客户端
 * 2.服务端在9999端口监听
 * 3.客户端连接到服务器端，发送“hello，server！”，并接受服务器端回发的“hello，client！”，再退出
 * 4.服务器端接受到客户端发送的信息，输出，并发送“hello，client！”，退出
 */
// 将字节输出流换为字符输出流
BufferdeWriter bw = new BufferedWriter(new OutputStreamWriter(outputStream));
bw.write("hello");
bw.newLine(); //插入一个换行符，作为写入结束标记，但要求对方使用readLine()!!!
bw.flush();//使用字符流需要手动刷新
// 将字节输入流转换为字符输入流
BufferedReader br = new BufferedReader(new InputStreamReader(inputStream));
System.out.println(br.readLine());
// 关闭IO流
bw.close();
br.close();
```



e.g.TCPFileCopy.java
```java
/**
 * 1.编写一个服务端，一个客户端
 * 2.服务端在9999端口监听
 * 3.客户端连接到服务端，发送一张图片e:\\qie.png
 * 4.服务端接收到客户端发送的图片，保存到src下，发送“收到图片”，退出
 * 5.客户端接收到服务端发送的“收到图片”，再退出
 */
public class Server {
    public static void main(String[] args) throws IOException {
        ServerSocket serverSocket = new ServerSocket(9999);
        System.out.println("服务端等待连接。。。");

        Socket socket = serverSocket.accept();

        String scrPathName = "new_die.png";
        InputStream inputStream = socket.getInputStream();
        BufferedOutputStream bo = new BufferedOutputStream(new FileOutputStream(scrPathName));
        byte[] buf = new byte[1024];
        int readLen = 0;
        while ((readLen = inputStream.read(buf)) != -1) {
            bo.write(buf);
        }
        bo.flush();
        bo.close();
        socket.shutdownInput();

        OutputStream outputStream = socket.getOutputStream();
        outputStream.write("收到图片".getBytes());
        outputStream.close();

        socket.close();
    }
}

public class Client {
    public static void main(String[] args) throws IOException {
        Socket socket = new Socket(InetAddress.getLocalHost(),9999);

        // 发送图片
        String pathName = "e:\\qie.png";
        OutputStream outputStream = socket.getOutputStream();
        BufferedOutputStream bo = new BufferedOutputStream(outputStream);
        BufferedInputStream bi = new BufferedInputStream(new FileInputStream(pathName));
        byte[] buf = new byte[1024];
        int readLen = 0;
        while ((readLen = bi.read(buf)) != -1) {
            bo.write(buf,0,readLen);
        }
        bo.flush();
        socket.shutdownOutput();
        bi.close();

        InputStream inputStream = socket.getInputStream();
        byte[] buf2 = new byte[1024];
        readLen = 0;
        while((readLen = inputStream.read(buf2)) != -1 ) {
            System.out.println(new String(buf2,0,readLen));
        }
        inputStream.close();
        
        socket.close();
    }
}
```

==总结==：
  socket获取IO流操作完毕后应用`socket.shutdown`关闭流
  即`socket.shutdown`**即是结束标记，也是关闭流的方法**

==补充：ByteArrayuInputStream&ByteArrayOutputStream==

**对于要创建临时性文件的程序以及网络数据的传输、数据压缩后的传输等可以提高运行的的效率，可以不用访问磁盘**

`java.io.ByteArrayInputStream、java.io.ByteArrayOutputStream`就是将字节数组当作流输入来源、输出目的地的类

有时候我们需要对同一个`InputStream`对象使用多次,但第一次读取`InputStream`对象后，第二次再读取时可能已经到Stream的结尾了（EOFException）或者Stream已经`close`掉了。而`InputStream`对象本身不能复制，因为它没有实现`Cloneable`接口。此时，可以先把`InputStream`转化成`ByteArrayOutputStream`，后面要使用`InputStream`对象时，再从`ByteArrayOutputStream`转化回来

当你资源不足够用时,选择`BufferedOutputStream`是最佳的选择, 当你选择快速完成一个作业时,可以选择`ByteArrayOutputStream`之类的输出流

e.g.
```java
/**
 * 将输入流转换为byte[],即可将文件内容读入到byte[]
 */
public static byte[] streamToByteArray(InputStream is) throws IOException{
	ByteArrayOutputStream bos = new ByteArrayOutputStream();
	byte[] b = new byte[1024];
	int len = 0;
	while ((len = is.read()) != -1) {
		bos.write(b,0,len);//将读入数据写入bos
	}
	byte[] array = bos.toByteArray();//将bos转换为byte数组
	return array;
}
```


## netstat指令

1.netstat -an 可以查看当前主机网络情况，包括端口监听情况和网络连接情况
2.netstat -an | more 可以分页显示
3.要求早dos控制台下执行

e.g
协议	本地地址	外部地址	状态
TCP	0.0.0.0:135		0.0.0.0:0	LISTENING

注：
1.本地地址中0.0.0.0和127.0.0.1均表示本地地址
2.135表示端口号
3.连接到主机的某个连接（包括本地连接）

## TCP连接扩展

==当客户端连接当服务端后，实际上客户端也是通过一个端口来与服务端进行通讯的，这个端口是TCP/IP来分配的==

## UDP网络通信编程

- ==基本介绍==
  1.类`DatagramSocket`【数据包套接字】和`DatagramPacket`【数据包】实现了基于UDP协议的网络程序
  2.UDP数据包**通过数据包套接字发送和接收**，系统并不保证UDP数据包一定能够安全送到目的地，也不能确定什么时候可以抵达
  3.`DatagramPacket`对象封装了UDP数据包，在数据包中包含了发送端的IP地址和端口号以及接收端的IP地址和端口号
  4.UDP协议中每个数据包都给出了完整的地址信息，因此**无需建立发送方和接收方的连接**

- 基本流程
  1.核心的两个类/对象`DatagramSocket`和`DatagramPacket`
  2.建立发送端，接收端
  3.发送数据前，建立数据包
  4.调用`DatagramSocket`的发送，接收方法
  5.关闭`DatagramSocket`

UDP说明：
  1.没有明确的服务端和客户端，演变成数据的发送端和接收端
  2.接收数据和发送数据时通过`DatagramSocket`对象完成
  3.将数据封装到`DatagramPacket`对象中，发送
  4.当接收到`DatagramPacket`对象，需要进行拆包，取出数据
  5.`DatagramSocket`的接收端指定某个端口接收数据

e.g.UDPExercise01.java
```java
/**
 * 1.编写一个接收端A，一个发送端B
 * 2.接收端在9999端口等待接收数据
 * 3.发送端B向接收端A发送数据“hello”
 * 4.接收端A接收到发送端B发送的数据，回复“hi”，退出
 * 5.发送端接收回复的数据，退出
 */

public class UDPReceiverA{
	public static void main (String[] args) throws IOExcepiton{
		//1.创建DatagramSocket对象，准备在9999端口接收数据
		DatagreamSocket socket = new DatagramSocket(9999);
        
        //2.构建一个DatagramPacket对象，准备接收数据
        //  UDP协议每个数据包大小限制在64K
        byte[] buf = new byte[64*1024];
        DatagramPacket packet = new DatagramPacket(buf,buf.length);
        
        //3.调用接收方法,将网络传输的DatagramPacket对象填充到packet中
        //  如果没有数据包发送到本机9999端口，就会堵塞
        System.out.println("接收端等待接收。。。")
        socket.receive(packet);
        
        //4.packet拆包,并显示
        int length = packet.getLength();//实际接收到的数据长度
        byte[] data = packet.getData();//接收到数据
        String s = new String(data,0,length);
        
        //5.发送hi
        byte[] sendData = "hi".getBytes();
        DatagramPacket packet2 = new DatagramPacket(sendData,sendData.length,InetAddress.getLocalHost(),9998);
        socket.send(packet2);
        socket.close();
	}
}

public class UDPSendB{
	public static void main (String[] args) {
        //1.创建DatagramSocket，准备在9998端口接收数据
		DatagramSocket socket = new DatagramSocket(9998);
        
        //2.将需要发送的数据，封装到DatagramPacket中
        byte[] data = "hello".getBytes();
        DatagramPacket packet = new DataPacket(data,data.length,InetAddress.getLocalHost,9999);
        
        //3.发送数据
        socket.send(packet);
        
        //4.接收数据，拆包并显示
        byte[] buf = new byte[64*1024];
        DatagramPacket packet2 = new DatagramPacket(buf,buf.length);
        socket.receive(packet2);
        int length = packet2.getLength();//实际接收到的数据长度
        byte[] data = packet2.getData();//接收到数据
        String s = new String(data,0,length);
        socket.close();
	}
}
```




# 项目开发流程简介

一.需求分析：
 1.需求分析师
 2.需求分析报告，该项目功能，客户具体要求

二.设计阶段
 1.架构师/项目经理
 2.设计工作(UML类图,流程图,模块设计,数据库,架构)
 3.原型开发
 4.组建团队

三.实现阶段
 1.程序员
 2.完成架构师的模块功能
 3.测试自己模块

四.测试阶段
 1.测试工程师
 2.单元测试,测试用例,白盒测试,黑盒测试,集成测试

五.实施阶段
 1.实施工程师
 2.把项目正确的部署到客户的平台,并保证运行正常

六.维护阶段
 1.发现bug解决
 2.项目升级







# 多用户通信系统

- 需求分析
  1.用户登录
  2.拉取在线用户列表
  3.无异常退出（客户端，服务端）
  4.私聊
  5.群聊
  6.发文件
  7.服务器推送新闻

- 项目：[Tofweod/Multi-users-Net-Communication (github.com)](https://github.com/Tofweod/Multi-users-Net-Communication)



# 反射

- 1.需求：

根据配置文件re.properties指定信息，创建对象并调用方法

classfullpath = psn.study.Cat
method = hi

```java
// 传统方式:new对象->调用方法
package psn.study.Cat
Cat cat = new Cat();
cat.hi();

// 尝试
// 1. 使用properties类,读取配置文件
Properties properties = new Properties();
properties.load(new FileInputStream("src\\re.properties"));
String classfullpath = properties.get("classfullpath").toString();
String methodName = properties.get("method").toString;

// 创建对象
new classfullpath(); // 该方法不行
```

- 2.这种需求在学习框架时特别多，即通过外部文件配置，在不修改源码的情况下，来控制程序，也符合设计模式==ocp原则（开闭原则）==

- 3.开闭原则:不修改源码(闭),扩展功能(开)

解决方法:
```java
// 使用反射机制(快速入门)

// 1.加载类,返回Class类型对象
Class cls = Class.forName(classfullpath); // throws ClassNotFoundException
// 2.通过cls对象得到加载的类psn.study.Cat的对象实例
Object obj = cls.newInstance();
// 3.通过cls得到加载得类psn.study.Cat的methodName的方法对象
//   即在反射中，可以把方法视为对象（万物皆对象）
Method method = cls.getMethod(methodName);
// 通过method调用方法：即通过方法对象实现调用方法
// 反射机制 方法.invoke(对象)
method.invoke(obj);
```

## Java Refleciton

- 反射机制允许程序在执行期借助ReflectionAPI取得任何类的内部信息（比如成员变量，构造器，成员方法等等），并能操作对象的属性及方法

- 加载完类之后，在堆中就产生了一个`Class`类型的对象（一个类只有一个Class对象），这个对象包含了类的完整结构信息，通过这个对象得到类的结构。这个对象就像一面镜子，透过这个镜子看到类的结构，故称之为“==反射==”

cat对象 ---> 类型Person类
cls对象 ---> 类型Class类

![](D:\JAVA\Note\src\Reflection\Reflection01.png)

作用：反射就是将类别的各个组成部分进行剖析，**可以得到每个组成部分，就可以对每一部分进行操作**。在比较复杂的程序或框架中来使用反射技术，可以简化代码提高程序的复用性

**==Java反射机制可以完成==**

- 在运行时判断任意一个对象所属的类
- 在运行时构造任意一个类的对象
- 在运行时得到任意一个类所具有的成员变量和方法
- 在运行时调用任意一个对象的成员变量和方法
- 生成动态代理

## 反射相关类

1.`java.lang.Class`:代表一个类，Class对象表示==某个类加载后在堆中的对象==

2.`java.lang.reflect.Method`:代表类的方法

3.`java.lang.reflect.Field`:代理类的成员变量

4.`java.lang.reflect.Constructor`:代表某个类的构造方法

## 反射机制

- 反射优点和缺点
  1.优点：可以动态的创建和使用对象（也是框架底层的核心），使用灵活，没有反射机制，框架技术就失去底层支撑
  2.缺点：使用反射基本是解释执行，对执行速度有影响

```java
/**
 * 测试反射调用性能和优化方案
 */
public class Test{
	public static void main(String[] args){
		m1();
        m2();
	}
	
	// 传统方法调用hi
	public static void m1(){
		Cat cat = new Cat();
		long start = System.currentTimeMillis();
		for(int i = 0; i <900000; i++){
			cat.hi();
		}
		long end = System.currentTimeMillis();
		System.out.println("m1用时" + (end - start) + "毫秒");
	}
	
	// 反射机制调用hi
	public static void m2(){
		Class cls = Class.forName("Cat");
		Object o = cls.newInstance();
		Method method = cls.getMethod("hi")
		long start = System.currentTimeMillis();
		for(int i = 0; i <900000; i++){
			method.invoke(o);
		}
		long end = System.currentTimeMillis();
		System.out.println("m2用时" + (end - start) + "毫秒");
	}
}

class Cat{
	public void hi() {
		
	}
}

/**
 * 结果
 * m1用时9毫秒
 * m2用时16毫秒
 * 结论
 * 反射调用方法性能远低于直接调用
 */
```


- 反射调用优化-关闭访问检查
  1.Method和Filed,Constructor对象都有`setAccessible()`方法
  2.`setAccessible()`作用是启动或禁止访问安全检查
  3.参数值为true表示反射的对象在使用时取消访问检查，提高反射效率；参数值为false则表示反射的对象执行访问检查

```java
// 反射调用优化+关闭访问检测
public static void m3(){
	Class cls = Class.forName("Cat");
	Object o = cls.newInstance();
    Method method = cls.getMethod("hi")
    method.setAccessible(true);//在反射调用方法时，取消访问检查
	long start = System.currentTimeMillis();
    for(int i = 0; i <900000; i++){
		method.invoke(o);
	}
	long end = System.currentTimeMillis();
    System.out.println("m2用时" + (end - start) + "毫秒");
}
```


## Class类

- 基本介绍
  1.Class<?>也是类，继承Object类 （`<?>`表示不确定的Java类型）
  2.Class类不是new出来的，而是系统创建的`ClassLoader.loadClass();`
  3.对于某个类的Class类对象，在内存中只能有一份，因为在内存中只能加载一次
  4.每个类的实例都会几点自己是由哪个Class实例生成的
  5.通过Class对象以及一系列API可以完整得到一个类的完整结构
  6.Class对象是存放在堆中的
  7.[类的字节码二进制数据是放在方法区的，也称类的元数据（包括方法代码，变量名，方法名，访问权限等等）](https://zhihu.com/question/38496907)	


- ==获取Class类对象的方法==
  1.编译阶段
    `Class.forName`
    前提:已知一个类全类名,且该类在类路径下,可通过Class静态方法`Class.forName()`获取,可能抛出ClassNotFoundException
    ==应用场景==:多用于配置文件,读取类全路径,加载类
  2.加载阶段
    `类.class`
    前提:若已知具体的类,通过类的class获取,该方法**最为安全可靠,程序性能最高**
    ==应用场景==:多用于参数传递,比如通过反射得到对应构造器对象
  3.运行阶段
    `对象.getClass()`
    前提:已知某个类的实例,调用该实例的`getClass()`获取Class对象
    ==应用场景==:通过创建好的对象,获取Class对象
  4.类加载器得到Class对象
    ```java
    // 以car对象为例
    ClassLoader cl = car.getClass().getClassLoader();   
    Class cls = cl.loadClass(classAllPath);
    ```
  5.基本数据类型(byte,char,boolean,int,float,double,long,short)按如下方式得到Class对象
    ```java
    // 以int为例
    Class<Integer> integerClass = int.class; // 存在自动装箱,拆箱过程(底层是Integer)
    ```
  6.基本数据j类型对应包装类,可通过`.TYPE`得到Class对象
    ```java
    Class<Integer> IntegerClass = Integer.TYPE;
    ```

注:上例中integerClass与IntegerClass相同

- 拥有Class对象的类型
  1.外部类，内部类
  2.interface
  3.数组
  4.enum
  5.annotation
  6.基本数据类型
  7.void

## 类加载

- 基本说明
  反射机制是java实现动态语言的关键，也就是通过反射实现类动态加载 
  1.静态加载：编译时加载相关的类，如果没有没有则报错，依赖性强
  2.动态加载：运行时加载需要的类，如果运行时不用该类，则不报错，降低了依赖性

  e.g.
 ```java
 // 此案例Dog类和Person类均未创建
 public class ClassLoarder_ {
 	public static void main(String[] args) throws Exception{
 		Scanner scanner = new Scanner(System.in);
 		String key = scanner.next();
 		switch(key){
 			case "1":
 				Dog dog = new Dog(); // 静态加载，编译时报错
 			case "2":
 				Class cls = Class.forName("Person"); // 动态加载，不运行不报错
		}
	}
 }
 ```
- ==类加载时机==
  1.创建对象时（new）
  2.当子类被加载时，父类也会加载
  3.调用类中的静态成员
  4.反射

  **类加载过程图**

<img src="D:\Java\Note\src\Reflection\Reflection02.png" style="zoom:50%;" />

<img src="D:\Java\Note\src\Reflection\Reflection03.png" style="zoom: 60%;"/>

- 加载阶段
  JVM在该阶段的主要目的是将字节码从不同的数据源（class文件，jar包，甚至网络）转化为二进制字节流加载到内存中，并生成一个代表该类的`java.lang.Class`对象
- 连接阶段-验证
  1.目的是为例确保Class文件的字节流中包含的信息符合当前虚拟机要求，并不会危害虚拟机滋生的安全
  2.包括：文件格式验证（是否以魔数**0xcafebabe**开头)，元数据验证，字节码验证和符号引用验证
  3.可以考虑使用`-Xverify：none`参数开关闭大部分类的验证措施，缩短虚拟机类加载时间
- 连接阶段-准备
  1.JVM会在该阶段对静态变量分配内存并进行默认初始化（对应数据类型的默认初始值，如`0、0L、null、false`等）。这些变量所使用的内存都会在方法区中进行分配
  2.`final static`类型数据是常量，在此阶段**直接赋值**
- 连接阶段-解析
  1.虚拟机将常量池的符号引用替换为直接引用的过程
  2.在编译过程类与类之间没有真正分配内存地址,为符号引用
- 初始化阶段
  1.该阶段真正执行类中定义的Java程序代码,此阶段是执行`<clinit>()`方法的过程
  2.`<clinit>()`方法是由编译器按语句在源文件中出现的顺序，依次自动收集类中所有==静态变量==的赋值动作和==静态代码块==中的语句，并进行合并
  3.虚拟机会保证一个类的`<clinit>()`方法在多线程环境中被正确地加锁、同步，如果多个线程同时去初始化一个类，那么只会有一个线程去执行这个类的`<clinit>()`方法，其他线程都需要阻塞等待，直到活动线程执行的该方法完毕

## 通过反射获取类的结构信息

- 第一组
  1.`getName()`：获得全下·类名
  2.`getSimpleName()`:获得简单类名
  3.`getFileds()`:获取所有public修饰的属性，==包括本类以及父类==
  4.`getDeclaredFields()`:获取本类所有属性，==不包括父类==
  5.`getMethods()`:获取所有public修饰的方法，==包括本类及父类==
  6.`getDeclaredMethods()`:获取本类所有方法，==不包括父类==
  7.`getConstructors()`:获取所有public修饰的构造器，==不包括父类==
  8.`getDeclaredConstructors()`:获取本类所有构造器
  9.`getPackage()`:以Package形式返回包信息
  10.`getSuperClass()`:以Class形式返回父类信息
  11.`getInterfaces`:以Class[]形式返回接口信息
  12.`getAnnotations()`:以Annotation[]形式返回注解



- 第二组
  1.`getModifiers()`:以int形式返回修饰符
    （默认修饰符是0，public是1，private是2，protected是4，static是8，final是16)e.g.`public static`为1+8=9
  2.`getType()`:以Class形式返回类型

  
  
- 第三组
  1.`getReturnType()`:以Class形式获取返回类型
  2.`getParameterTypes()`:以Class[]返回参数类型数组

## 反射暴破

使用反射可以访问private修饰的类成员

```java
/**
 * 暴破演示
 */
public class Test{
    Class personCls = Class.forName("Person");
    
    public static void main(String[] args){
        
    }
    
    // 暴破构造器
    public void testConstructor(){
        // 获取私有构造器
        Constructor<?> constructor = personCls.getDeclaredConstructor(int.class, String.class);
        // 暴破
        constructor.setAccessible(true);
        // 创建对象
        constructor.newInstance(10,"person"); // 如果没有暴破，则会抛出IllegalAccessException
    }
    
    // 暴破属性
    public void testField(){
        // 创建对象
        Object o = personCls.newInstance();
        // 获得私有属性
        Field field = personCls.getDeclaredField("age");
        // 暴破
        field.setAccessible(true);
        // 设置age，原值为10
        field.set(o,20); // 将对象o的age设置为20
        field.get(o); // 获取o对象的age属性
        // 如果是静态属性，对象参数可以设置为null
	}
    
    // 暴破方法
    public void testMethod(){
        // 与暴破属性同理
        // 获取方法 Method m = personCls.getDeclaredMethod("方法名"，参数.class);
    }
}

class Person{
    private int age = 10;
    private String name = "aPerson";
    
    public Person{}
    
    private Person(int age, String name){
        this.age = age;
        this.name = name;
	}
}
```

# ==MySQL==

连接到MySQL服务的指令

`mysql -h 主机IP -P 端口号 -u 用户名 -p密码`

注：
 1.-p密码后无空格
 2.-h 主机IP 默认本机IP；-P 端口号默认3306
 3.-P 端口号必须和my.ini配置文件相匹配

## MySQL三层结构

1.安装MySQL数据库，就是在主机上安装一个数据库管理胸痛DBMS(database manage system),这个管理程序可以管理多个数据库
2.一个数据库中可以创建多个表，以保存数据

- 数据库管理系统、数据库和表关系示意图

<img src="D:\Java\Note\src\MySQL\MySQL01.png">

==数据库-表的本质仍然是文件==

表的一行称之为一条记录->在java程序中，一行记录往往使用对象来映射

- SQL语句分类
  1.DDL:数据定义语句 [creat表，库。。]
  2.DML:数据操作语句 [增insert，删delete，改update]
  3.DQL:数据查询语言 [select]
  4.DCL:数据控制语句 [管理数据库，比如用户权限grant&revoke]

## MySQL操作

### 数据库操作

创建数据库:

 `CREATE DATABASE [IF NOT EXISTS]db_name [create_specification[,create_specification]...]` 

create_specification:
  [DEFAULT]CHARACTER SET character_name
  [DEFAULT]COLLATE collation_name

  1.CHARACTER SET:指定数据库采用的字符集，默认utf8
  2.COLLATE:指定数据库字符集的校对规则，默认utf8_general_ci
            		常用的utf8_bin[区分大小写],utf8_general_ci[不区分大小写]

```mysql
# 创建字符集为utf8，校对规则为utf8_general_ci的数据库db01
CREATE DATABASE db01 CHARARCTER SET utf8 COLLATE utf8_general_ci
```

 ==注==:在创建数据库、表时,为避免关键字,可以用反引号解决

显示数据库语句:

`SHOW DATABASES LIKE '数据库名' ` 

显示数据库创建语句:

`SHOW CREATE DATABASE db_name`

数据库删除语句[==慎用==]

`DROP DATABASE [IF EXISTS] db_name`

备份数据库(在==DOS执行==命令行)----**备份的文件就是对应的sql语句**

`mysqldump -u 用户名 -p密码 -B 数据库1 数据库2 ... 数据库n > 路径/文件名.sql` # 备份多个数据库	
`mysqldump -u 用户名 -p密码 数据库 表1 表2 ... 表n > 路径/文件名.sql` # 备份数据库中具体的表

恢复数据库(进入==MySQL命令行==执行)

 1.`source 文件名.sql`
 2.直接将sql文件内容粘贴至查询编译器执行
 注：备份数据库和恢复数据库**使用命令行不同**，前者是DOS，后者是Mysql

### 表操作

创建表

`CREATE TABLE table_name
 (
 	field1 datatype,
 	field2 datatype,
 	field3 datatype
 )character set 字符集 collate 校对规则 engine 存储引擎`

 field:指定列名	datatype:指定列类型（字段类型）
 engine:引擎

 创建表的时候，要根据需保存数据创建相应的列，并根据数据的类型定义相应的列类型

```mysql
/*
 创建表实例
 */
CREATE TABLE `user`(
	id int,
    `name` varchar(255),
    `password` varchar(255),
    `birthday` date)
    CHARACTER SET utf8 COLLATE utf8_bin ENGINE INNODB;
)
```

## MySQL数据类型

MySQL数据类型即MySQL列类型

**分类**

- 数值类型
- 文本、二进制类型
- 时间日期类型

### 数值类型

- 整型
  1.`tinyint` [一个字节] 
  2.`smallint` [两个字节]
  3.`mediumint` [三个字节]
  **4**.`int` [四个字节]
  5.`bigint` [八个字节]
  定义无符号整数，在类型后加`unsigned`
  
- 小数类型
  1.`float` [单精度 4个字节]
  **2**.`double` [双精度 8个字节]
  **3**.`decimal[M,D]` [大小由M,D决定] 定点数 M指定长度，D表示小数点位数
  decimal说明：
  1.如果D为0，则值没有小数部分或分数部分
  2.M最大值为65，D最大值为30；M默认值为10，D默认值为0
  3.希望小数精度最高，推荐使用decimal
  4.decimal占字节M+2个字节
  e.g.
  decimal(5，2)最大值为9999.99

### 文本类型(字符串类型)

  **1**.`char` 0-255
  **2**.`varchar` 0-65535(2^16^-1)
  **3**.`text` 0-65535
  4.`longtext` 0-2^32^-1

- 细节
  - size表示==字符数==
  - CHAR(size)
    固定长度字符串 最大255==字符==
  - VARCHAR(size) 0-65535 
    可变长度字符串 最大65535==字节== [uft8编码最大21844字符，因为有1-3个字节用于记录大小，则65532/3=21844]

### 二进制数据类型

  1.`blob` 0-65535
  2.`longblob` 0-2^32^-1

### 日期类型

  1.`date` 日期类型[年-月-日]
  2.`time` 时间类型[时-分-秒]
  **3**.`datetime` [年-月-日-时-分-秒] 格式：YYYY-MM-DD HH:mm:ss
  **4**.`timestamp` 时间戳
  5.`year` 年





**特殊** ：==bit== 

- 基本使用 
  bit(M)
  
- 细节说明
  1.bit字段显示时，按==位==的方式显示，m=8表示一个字节
  2.查询时仍热可以使用添加的数值
  3.如果一个值只有0和1，可以考虑使用bit(1)节约空间
  4.M指定位数，默认位1，范围1-64
  

e.g.
255位表示为`b'11111111'`















# 设计模式

## 单例模式

应用场景：在整个软件系统中，对某个类只能存在一个对对象实例，并且该类只提供一个获取其对象实例的方法

1.饿汉式
```java
class Single() {
	private Single() {} //1.构造器私有化
	private static Single single = new Single(); //2.在类的内部直接创建
	public static Single getsingle() { //3.提供公共static方法返回对象
		return single;
	}
}
```

2.懒汉式

```java
class Single() {
	private Single() {}
	private static Single single;
	public static Single getsingle() {
		if(single == null ) {
			single = new Single();
		}
		return single;
	} 
}
```

**本质区别：创建对象时机不同**

- 饿汉式在类加载就创建对象实例，懒汉式使用时才创建
- 饿汉式不存在线程安全问题，懒汉式则存在该问题
- 饿汉式存在资源浪费可能
- javaSE标准类中，java.lang.Runtime就是经典单例模式

## 模板设计模式
（附<https://blog.csdn.net/zxd1435513775/article/details/120080387>)

**适用于一些复杂操作进行步骤分割、抽取公共部分由抽象父类实现、将不同的部分在父类中定义抽象实现、而将具体实现过程由子类完成。对于整体步骤很固定，但是某些部分易变，可以将易变的部分抽取出来，供子类实现。**

```java
public abstract class SoyaMilk {

	//模板方法：可以做成final，不让子类去覆盖
	final void make() {
		select();
		if(customerWantCondiment()) {
			addCondiment();
		}	
		soak();
		beat();
	}

	//1.选材料
	void select() { System.out.println("第一步：选择新鲜的豆子"); }
	//2.添加不同的配料：抽象方法，由子类具体实现
	abstract void addCondiment();
	//3.浸泡
	void soak() { System.out.println("第三步：豆子和配料开始浸泡3H"); }
	//4.榨汁
	void beat() { System.out.println("第四步：豆子和配料放入豆浆机榨汁"); }

	//钩子方法：决定是否需要添加配料
	boolean customerWantCondiment() {
		return true;//默认情况下是要加配料的
	}
}

// PureSoyaMilk.java
public class PureSoyaMilk extends SoyaMilk {
	@Override
	void addCondiment() {
		// 添加配料的方法 空实现 即可
	}
	@Override
	boolean customerWantCondiment() {
		return false;
	}
}

// Client.java
public class Client {
	public static void main(String[] args) {
		System.out.println("=制作纯豆浆=");
		SoyaMilk pureSoyMilk = new PureSoyaMilk();
		pureSoyMilk.make();
	}
}
```













