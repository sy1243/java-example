### 使用MAVEN构建项目骨架
```
mvn archetype:generate -DgroupId=org.java -DartifactId=java-example -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=true
```

### 面向对象三大特性

    继承：单继承，接口可以多实现
    
    封装：访问权限控制public > protected > 包 > private 内部类也是一种封装
    
    多态：编译时多态，体现在向上转型和向下转型，通过引用类型判断调用哪个方法（静态分派）。
    
    运行时多态，体现在同名函数通过不同参数实现多种方法（动态分派）。

### 基本数据类型

    byte int long short string char float double
    基本类型位数，自动装箱，常量池
    
    例如byte类型是8位，可以表示的数字是-128到127，因为还有一个0，加起来一共是256，也就是2的八次方。
    
    基本数据类型的包装类只在数字范围-128到127中用到常量池，会自动拆箱装箱，其余数字范围的包装类则会新建实例
    
### String及包装类

    String类型是final类型，在堆中分配空间后内存地址不可变。
    
    底层是final修饰的char[]数组，数组的内存地址同样不可变。
    
    但实际上可以通过修改char[n] = 'a'来进行修改，不会改变String实例的内存值，不过在jdk中，用户无法直接获取char[]，也没有方法能操作该数组。
    所以String类型的不可变实际上也是理论上的不可变。
    
    StringBuffer和StringBuilder底层是可变的char[]数组，继承父类AbstractStringBuilder的各种成员和方法，实际上的操作都是由父类方法来完成的。
    
### final关键字

    final修饰基本数据类型保证不可变
    
    final修饰引用保证引用不能指向别的对象
    
    final修饰类，类的实例分配空间后地址不可变，子类不能重写所有父类方法。
    
    final修饰方法，子类不能重写该方法。
    
### 抽象类和接口

    1 抽象类可以有方法实现。
    抽象类有非final成员变量。
    抽象方法要用abstract修饰。
    抽象类可以有构造方法，但是只能由子类进行实例化。
    
    2 接口可以用extends加多个接口实现多继承。
    接口只能有public final类型的成员变量。
    接口只能由抽象方法，不能有方法体、
    接口不能实例化，但是可以作为引用类型。
    
### 代码块和加载顺序

    假设该类是第一次进行实例化。那么有如下加载顺序
    静态总是比非静态优先，从早到晚的顺序是：
    1 静态代码块 和 静态成员变量的顺序根据代码位置前后来决定。
    2 代码块和成员变量的顺序也根据代码位置来决定
    3 最后才调用构造方法构造方法
### 包、内部类、外部类
    1 Java项目一般从src目录开始有com.*.*.A.java这样的目录结构。这就是包结构。所以一般编译后的结构是跟包结构一模一样的，这样的结构保证了import时能找到正确的class引用包访问权限就是指同包下的类可见。
    
    import 一般加上全路径，并且使用.*时只包含当前目录的所有类文件，不包括子目录。
    
    2 外部类只有public和default两种修饰，要么包内可访问，要么全局可访问。
    
    3 内部类可以有全部访问权限，因为它的概念就是一个成员变量，所以访问权限设置与一般的成员变量相同。
    
    非静态内部类是外部类的一个成员变量，只跟外部类的实例有关。
    
    静态内部类是独立于外部类存在的一个类，与外部类实例无关，可以通过外部类.内部类直接获取Class类型。

### 异常

    1 异常体系的最上层是Throwable类
    子类有Error和Exception
    Exception的子类又有RuntimeException和其他具体的可检查异常。
    
    2 Error是jvm完全无法处理的系统错误，只能终止运行。
    
    运行时异常指的是编译正确但运行错误的异常，如数组越界异常，一般是人为失误导致的，这种异常不用try catch，而是需要程序员自己检查。
    
    可检查异常一般是jvm处理不了的一些异常，但是又经常会发生，比如Ioexception，Sqlexception等，是外部实现带来的异常。
    
    3 多线程的异常流程是独立的，互不影响。
    大型模块的子模块异常一般需要重新封装成外部异常再次抛出，否则只能看到最外层异常信息，难以进行调试。

### 泛型

    Java中的泛型是伪泛型，只在编译期生效，运行期自动进行泛型擦除，将泛型替换为实际上传入的类型。
    
    泛型类用class <T> A {
        
    }这样的形式表示，里面的方法和成员变量都可以用T来表示类型。泛型接口也是类似的，不过泛型类实现泛型接口时可以选择注入实际类型或者是继续使用泛型。
    
    泛型方法可以自带泛型比如void <E> E go();
    
    泛型可以使用?通配符进行泛化 Object<?>可以接受任何类型
    
    也可以使用 <? extends Number> <? super Integer>这种方式进行上下边界的限制。

### Class类和Object类

    Java反射的基础是Class类，该类封装所有其他类的类型信息，并且在每个类加载后在堆区生成每个类的一个Class<类名>实例，用于该类的实例化。
    
    Java中可以通过多种方式获取Class类型，比如.class,getClass方法以及Class.forName方法。
    
    Object是所有类的父类，有着自己的一些私有方法，以及被所有类继承的9大方法。

### javac和java

    javac 是编译一个java文件的基本命令，通过不同参数可以完成各种配置，比如导入其他类，指定编译路径等。
    
    java是执行一个java文件的基本命令，通过参数配置可以以不同方式执行一个java程序或者是一个jar包。
    
    javap是一个class文件的反编译程序，可以获取class文件的反编译结果，甚至是jvm执行程序的每一步字节码实现。

### 反射

    Java反射包reflection提供对Class，Method，field，constructor等信息的封装类型。
    
    通过这些api可以轻易获得一个类的各种信息并且可以进行实例化，方法调用等。
    
    类中的private参数可以通过setaccessible方法强制获取。
 
### 枚举类
    枚举类继承Enum并且每个枚举类的实例都是唯一的。
    
    枚举类可以用于封装一组常量，取值从这组常量中取，比如一周的七天，一年的十二个月。
    
    枚举类的底层实现其实是语法糖，每个实例可以被转化成内部类。并且使用静态代码块进行初始化，同时保证内部成员变量不可变。
    
### 序列化

    序列化的类要实现serializable接口
    
    transient修饰符可以保证某个成员变量不被序列化
    
    readObject和writeOject来实现实例的写入和读取。
    
    待更新。

### 动态代理

    jdk自带的动态代理可以代理一个已经实现接口的类。
    
    cglib代理可以代理一个普通的类。
    
    动态代理的基本实现原理都是通过字节码框架动态生成字节码，并且在用defineclass加载类后，获取代理类的实例。
    
    一般需要实现一个代理处理器，用来处理被代理类的前置操作和后置操作。

### 多线程
    这里先不讲juc包里的多线程类。juc相关内容会在juc专题讲解。
    
    Java中的线程有7种状态，new runable running blocked waiting time_waiting terminate
    blocked是线程等待其他线程锁释放。
    waiting是wait以后线程无限等待其他线程使用notify唤醒
    time_wating是有限时间地等待被唤醒，也可能是sleep固定时间。
    
    线程的实现可以通过继承Thread类和实现Runable接口
    也可以使用线程池。callable配合future可以实现线程中的数据获取。
    
    一个线程实例连续start两次会抛异常。

### 网络编程

    主要是Socket编程，相关类比较多。
    待更新

### Java8

    接口中的默认方法，接口终于可以有方法实现了
    lambda表达式实现了函数式编程
    Option类实现了非空检验
    新的日期API
    各种api的更新，包括chm，hashmap的实现等
    Stream流概念，实现了集合类的流式访问
    待更新