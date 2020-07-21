## 1. 接口

接口用来描述类应该做什么，而不指定具体应该如何做。一个类可以实现一个或多个接口。

接口中的方法自动是public方法，声明时，不必提供public方法。

接口中没有实例字段。

### 1.1 回调

```java
import javax.swing.*;
import java.awt.*;
import java.awt.event.*;
import java.time.*;

public class callerTest {
    public static void main(String[] args) {
        TimePrinter timePrinter = new TimePrinter();
        Timer t = new Timer(1000, timePrinter);
        t.start();
        JOptionPane.showMessageDialog(null, "Quit program!");
        System.exit(0);
    }

}

class TimePrinter implements ActionListener{

    @Override
    public void actionPerformed(ActionEvent e) {
        System.out.println("Time is "
                + Instant.ofEpochMilli(e.getWhen()));
        Toolkit.getDefaultToolkit().beep();
    }
}
```

## 2. lambda表达式

### 2.1 lambda表达式语法

(参数列表) -> { 代码块 } 

### 2.2 方法引用

```java
Timer t = new Timer(1000, System.out::println);

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

## 3. 内部类

内部类是定义在另一个类中的类。使用内部类的原因：

- 内部类可以对同一个包中的其他类隐藏
- 内部类方法可以访问定义这个类的作用域中的数据，包括原有私有的数据



## 4. 服务加载器

```java
public interface Cipher {
    byte[] encrypt(byte[] source, byte[] key);
    byte[] decrypt(byte[] source, byte[] key);
    int strength();
}
```

```java
public class CaesarCipher implements Cipher {
    @Override
    public byte[] encrypt(byte[] source, byte[] key) {
        byte[] result = new byte[source.length];
        for (int i = 0; i < source.length; i++) {
            result[i] = (byte)(source[i] + key[0]);
        }
        return result;
    }

    @Override
    public byte[] decrypt(byte[] source, byte[] key) {
        return encrypt(source, new byte[]{(byte)-key[0]});
    }

    @Override
    public int strength() {
        return 1;
    }
}
```

初始化一个服务加载器：

```java
public static ServiceLoader<Cipher> cipherLoader = ServiceLoader.load(Cipher.class);
```

## 5. 代理

利用代理可以在运行时创建实现了一组给定接口的新类。只有在编译时期无法确定需要实现哪个接口时才有必要使用代理。

























