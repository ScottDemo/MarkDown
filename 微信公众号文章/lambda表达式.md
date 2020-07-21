# 1. lambda初相识

lambda表达式是一种可传递的代码块，可以在以后执行一次或多次。我们可以将lambda表达式的代码块，当做参数传递给构造方法或是普通方法以便后续执行。来看下面这样一句代码：

```java
() -> System.out.println("Hello World!")
```

来从左到右解释一下:

- `()` 为 Lambda 表达式的参数列表（本例中没有参数）
- `->`标识这串代码为 lambda 表达式（也就是说，看到 `->` 就知道这是 lambda）
- `System.out.println("Hello World!")` 为要执行的代码，即将“Hello World!”打印到标准输出流

这就是lambda表达式的一般形式。

# 2. lambda表达式语法

这里我们选择一个有参数的lambda表达式作为示例：

```java
String[] strings = {"aa", "bb","cc", "dd"};
List<String> list =  Arrays.asList(strings);
// list变量后面还会用到

list.forEach(
	(String string) -> {System.out.println(string);}
);
```

如果可以推导出lambda表达式的参数类型，则可以忽略其类型：

```java
// 编译器可以推断出string一定是一个字符串，则String可以省略
list.forEach(
        (string) -> {System.out.println(string);}
);
```

如果方法只有一个参数，而这个参数的类型可以推导出，甚至可以省略小括号：

```java
list.forEach(
        string -> {System.out.println(string);}
);
```

# 3. 函数式接口

对于只有一个抽象方法的接口，需要这种接口的对象时，就可以提供一个lambda表达式，这种接口称为`函数式接口`。

java.util.function包中有一个接口Predicate：

```java
// Predicate接口只有一个抽象方法
public interface Predicate<T> {
    boolean test(T t);
}
```

ArrayList类有一个removeIf方法，它的参数就是一个Predicate，专门用来接收lambda表达式。例如，下面的语句可以删除一个数组列表中所有的null值：

```java
arrayList.removeIf(e -> e == null);
```

# 4. 方法引用

```
list.forEach(
        System.out::println
);
```

表达式`System.out::println`就是一个方法引用，它指示编译器生成一个函数式接口的实例。

```java
String[] strings = {
        "aa", "bb","cc", "dd"
};
```

假设你想对以上字符串进行排序，而不考虑字母的大小写，可以传递如下表达式：

```java
Arrays.sort(strings, String::compareToIgnoreCase);
```

要使用`::`运算符分隔方法名与对象或类名。主要有三种情况：

- object::instanceMethod  
  - 等价于向方法传递参数的lambda表达式
- Class::instanceMethod
  - 第一个参数会成为方法的隐式参数
- Class::staticMethod
  - 所有参数都传递到静态方法

|     方法引用      |      等价的lambda表达式      |                             说明                             |
| :---------------: | :--------------------------: | :----------------------------------------------------------: |
| separator::equals |   x -> separator.equals(x)   | 这是包含一个对象和一个实例方法的方法表达式。lambda参数作为这个方法的显式参数传入。 |
|   String::trim    |        x -> x.trim()         | 这是包含一个类和一个实例方法的方法表达式。lambda表达式会成为隐式参数。 |
|  String::concat   |    (x, y) -> x.concat(y)     | 同样，这里有一个实例方法，不过这次有一个显式参数。与前面一样，第一个lambda参数会成为隐式参数，其余的参数会传递到方法。 |
| Integer::valueOf  |   x -> Integer::valueOf(x)   | 这是包含一个静态方法的方法表达式。lambda参数会传递到这个静态方法。 |
|   Integer::sum    | (x, y) -> Integer::sum(x, y) | 这是另一个静态方法，不过这一次有两个参数。两个lambda参数都传递到这个静态方法。Integer.sum方法专门创建为作为一个方法引用。对于lambda表达式，可以只写作(x, y) -> x + y |
|   Integer::new    |     x -> new Integer(x)      |       这是一个构造器应用，lambda参数传递到这个构造器。       |
|  Integer[]::new   |     n -> new Integer[n]      |          这是一个构造器应用，lambda参数是数组长度。          |

# 5. 变量作用域

lambda表达式有三个部分：

- 一个代码块；
- 参数；
- 自由变量的值，这里指非参数而不在代码中定义的变量。

```java
public static void repeat(String word){
    ActionListener listener = event -> {
        System.out.println(word);
    };
    new Timer(1000, listener).start();
}
```

自由变量即上例中的**word**。

运行上例代码我们会发现控制台并未输出任何信息。是程序出错没有运行吗？并不是哦。只是因为lambda表达式中的内容在repeat调用返回很久之后才运行。也就是说，lambda中的代码块采用的是线程并发执行。

我们来看下面一段代码：

```java
public static void repeat(String word, int times){
    ActionListener listener = event -> {
        times--; // Error
        System.out.println(word);
    };
    new Timer(1000, listener).start();
}
```

lambda表达式可以捕获外围作用域中变量的值，但要确保所捕获的值是明确定义的，只能引用值不会改变的变量。这个限制是有原因的，如果在lambda表达式中更改变量，并发同时执行多个操作就会变得不安全。

这里有一条规则：lambda表达式中捕获的变量必须实际上是`事实最终变量`，即这个变量初始化之后就不会为它赋新值。

# 6. 总结

尽管 Lambda 表达式在简化 Java 编程方面做了很多令人惊讶的努力，但在某些情况下，不当的使用仍然会导致不必要的混乱，慎用，慎用！

