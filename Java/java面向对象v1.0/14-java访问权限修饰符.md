

# Java访问权限修饰符

这个是我们掌握封装的核心知识。

考虑两个场景：

场景 1：工程师 A 编写了一个类 ClassA，但是工程师 A 并不希望 ClassA 被其他类都访问到，该如何处理呢？

场景 2：工程师 A 编写了一个类 ClassA，其中有两个方法 fun1、fun2，工程师只想让 fun1 对外可见，也就是说，如果别的工程师来调用 ClassA，只可以调用方法 fun1，该怎么处理呢？

此时，访问权限控制便可以起到作用了。

在 Java 中，提供了四种访问权限控制：

- 默认访问权限（包访问权限）
- public
- private
- protected

类只可以用默认访问权限和 public 修饰。比如说：



```java
public class Wanger{}
```

或者



```java
class Wanger{}
```

但变量和方法则都可以修饰。

### 1. 修饰类

- 默认访问权限（包访问权限）：用来修饰类的话，表示该类只对同一个包中的其他类可见。
- public：用来修饰类的话，表示该类对其他所有的类都可见。

例 1：

Main.java:



```java
package com.tobetterjavaer.test1;

public class Main {
	public static void main(String\[\] args) {

		People people = new People("Tom");
		System.out.println(people.getName());
	}

}
```

People.java



```java
package com.tobetterjavaer.test1;

class People {//默认访问权限（包访问权限）

	private String name = null;

	public People(String name) {
		this.name = name;
	}

	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}
}
```

从代码可以看出，修饰 People 类采用的是默认访问权限，而由于 People 类和 Main 类在同一个包中，因此 People 类对于 Main 类是可见的。

例子 2：

People.java



```java
package com.tobetterjavaer.test2;

class People {//默认访问权限（包访问权限）

	private String name = null;

	public People(String name) {
		this.name = name;
	}

	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}
}
```

此时 People 类和 Main 类不在同一个包中，会发生什么情况呢？

下面是 Main 类中的提示的错误：

![img](pictures/bokeyuan-jianxijavazhongdifangwenquanxiankongzhi-154ae82f-72a5-45fc-ad3c-e1eb575d8572.png)

提示 Peolple 类在 Main 类中不可见。从这里就可以看出，如果用默认访问权限去修饰一个类，该类只对同一个包中的其他类可见，对于不同包中的类是不可见的。

正如上图的快速修正提示所示，将 People 类的默认访问权限更改为 public 的话，People 类对于 Main 类便可见了。

### 2. 修饰方法和变量

- 默认访问权限（包访问权限）：如果一个类的方法或变量被包访问权限修饰，也就意味着只能在同一个包中的其他类中显示地调用该类的方法或者变量，在不同包中的类中不能显式地调用该类的方法或变量。
- private：如果一个类的方法或者变量被 private 修饰，那么这个类的方法或者变量只能在该类本身中被访问，在类外以及其他类中都不能显式的进行访问。
- protected：如果一个类的方法或者变量被 protected 修饰，对于同一个包的类，这个类的方法或变量是可以被访问的。对于不同包的类，只有继承于该类的类才可以访问到该类的方法或者变量。
- public：被 public 修饰的方法或者变量，在任何地方都是可见的。

例 3：

Main.java 没有变化

People.java



```java
package com.tobebetterjavaer.test1;

public class People {

	private String name = null;

	public People(String name) {
		this.name = name;
	}

	String getName() {    //默认访问权限（包访问权限）
		return name;
	}

	void setName(String name) {   //默认访问权限（包访问权限）
		this.name = name;
	}
}
```

此时在 Main 类是可以显示调用方法 getName 和 setName 的。

但是如果 People 类和 Main 类不在同一个包中：



```java
package com.tobebetterjavaer.test2;    //与Main类处于不同包中

public class People {

	private String name = null;

	public People(String name) {
		this.name = name;
	}

	String getName() {    //默认访问权限（包访问权限）
		return name;
	}

	void setName(String name) {   //默认访问权限（包访问权限）
		this.name = name;
	}
}
```

此时在 Main 类中会提示错误：

![img](pictures/bokeyuan-jianxijavazhongdifangwenquanxiankongzhi-b3e9dc56-53e8-42f1-b8ee-35115edfe7e7.png)

由此可以看出，如果用默认访问权限来修饰类的方法或者变量，则只能在同一个包的其他类中进行访问。

例 4:

People.java



```java
package com.tobebetterjavaer.test1;

public class People {

	private String name = null;

	public People(String name) {
		this.name = name;
	}

	protected String getName() {
		return name;
	}

	protected void setName(String name) {
		this.name = name;
	}
}
```

此时是可以在 Main 中显示调用方法 getName 和 setName 的。

如果 People 类和 Main 类处于不同包中：



```java
package com.tobebetterjavaer.test2;

public class People {

	private String name = null;

	public People(String name) {
		this.name = name;
	}

	protected String getName() {
		return name;
	}

	protected void setName(String name) {
		this.name = name;
	}
}
```

则会在 Main 中报错：

![img](pictures/bokeyuan-jianxijavazhongdifangwenquanxiankongzhi-b1d4b7ed-fc87-47d4-bdd9-3f6a8ea96100.png)

如果在 com.cxh.test1 中定一个类 Man 继承 People，则可以在类 Man 中显示调用方法 getName 和 setName：



```java
package com.tobebetterjavaer.test1;

import com.tobebetterjavaer.test2.People;

public class Man extends People {

    public Man(String name){
        super(name);
    }

    public String toString() {
        return getName();
    }
}
```

补充一些关于 Java 包和类文件的知识：

1）Java 中的包主要是为了防止类文件命名冲突以及方便进行代码组织和管理；

2）对于一个 Java 源代码文件，如果存在 public 类的话，只能有一个 public 类，且此时源代码文件的名称必须和 public 类的名称完全相同。

另外，如果还存在其他类，这些类在包外是不可见的。如果源代码文件没有 public 类，则源代码文件的名称可以随意命名。

![image-20230616180412200](pictures/image-20230616180412200.png)

简单的来说就是

![image-20230616180421789](pictures/image-20230616180421789.png)