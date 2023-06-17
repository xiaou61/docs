

# java初始代码块

代码初始化块用于初始化一些成员变量

“可以直接通过‘=’操作符对成员变量进行初始化，但通过代码初始化块可以做更多的事情，比如说打印出成员变量初始化后的值。”

我们来看下面的代码可以直接通过 `=` 操作符对成员变量进行初始化。



```java
class Bike{  
    int speed=100;  
}  
```

那为什么还需要代码初始化块呢？“我们可以通过代码初始化块执行一个更复杂的操作，比如为集合填充值。来看下面这段代码

```java
public class Bike {
    List<String> list;

    {
        list = new ArrayList<>();
        list.add("1");
        list.add("2");
    }

    public static void main(String[] args) {
        System.out.println(new Bike().list);
    }
}

```



“如果只使用‘=’操作符的话，是没办法完成集合初始化的，对吧？‘=’ 后面只能 new 出集合，却没办法填充值，代码初始化就可以完成这项工作。”

再看下面的例子

```java
public class Car {
    Car() {
        System.out.println("构造方法");
    }

    {
        System.out.println("代码初始化块");
    }

    public static void main(String[] args) {
        new Car();
    }
}

```

我们可以发现输出的结果是

```java
代码初始化块
构造方法

```

从输出结果看上去，仿佛代码初始化块执行得更早，

对象在初始化的时候会先调用构造方法，这是毫无疑问的，只不过，构造方法在执行的时候会把代码初始化块放在构造方法中其他代码之前，所以，先看到了‘代码初始化块’，后看到了‘’构造方法’。

![img](pictures/22-01.png)

对于代码初始化来说，它有三个规则。

- 类实例化的时候执行代码初始化块；
- 实际上，代码初始化块是放在构造方法中执行的，只不过比较靠前；
- 代码初始化块里的执行顺序是从前到后的。

这些规则不用死记硬背，大致了解一下就行了。我们继续来看下面这段代码

```java
class A {
    A () {
        System.out.println("父类构造方法");
    }
}
public class B extends A{
    B() {
        System.out.println("子类构造方法");
    }

    {
        System.out.println("代码初始化块");
    }

    public static void main(String[] args) {
        new B();
    }
}

```

下面来看输出结果

```java
父类构造方法
代码初始化块
子类构造方法
```

在默认情况下，子类的构造方法在执行的时候会主动去调用父类的构造方法。也就是说，其实是构造方法先执行的，再执行的代码初始化块。

“这个例子再次印证了之前的第二条规则：代码初始化块是放在构造方法中执行的，只不过比较靠前。

下面是一个 Java 示例代码，演示实例初始化块和静态初始化块的用法：

```java
public class Example {
    // 静态变量
    public static int staticVar = 1;
    // 实例变量
    public int instanceVar = 2;

    // 静态初始化块
    static {
        System.out.println("执行静态初始化块");
        staticVar = 3;
    }

    // 实例初始化块
    {
        System.out.println("执行实例初始化块");
        instanceVar = 4;
    }

    // 构造方法
    public Example() {
        System.out.println("执行构造方法");
    }

    public static void main(String[] args) {
        System.out.println("执行main方法");

        Example e1 = new Example();
        Example e2 = new Example();

        System.out.println("e1的静态变量：" + e1.staticVar);
        System.out.println("e1的实例变量：" + e1.instanceVar);
        System.out.println("e2的静态变量：" + e2.staticVar);
        System.out.println("e2的实例变量：" + e2.instanceVar);
    }
}

```

在这个示例代码中，有一个静态变量 staticVar 和一个实例变量 instanceVar，以及一个静态初始化块和一个实例初始化块。在静态初始化块中，我们打印了一条消息并修改了静态变量的值；在实例初始化块中，我们也打印了一条消息并修改了实例变量的值。来看一下执行结果：



```text
执行静态初始化块
执行main方法
执行实例初始化块
执行构造方法
执行实例初始化块
执行构造方法
e1的静态变量：3
e1的实例变量：4
e2的静态变量：3
e2的实例变量：4
```

从输出结果可以看出，静态初始化块在类加载时执行，只会执行一次，并且优先于实例初始化块和构造方法的执行；实例初始化块在每次创建对象时执行，在构造方法之前执行。