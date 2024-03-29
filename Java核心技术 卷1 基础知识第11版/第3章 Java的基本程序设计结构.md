## 一、数据类型

### 1. 整型

| 类型  | 存储需求 | 取值范围                                               |
| :---: | :------: | :----------------------------------------------------- |
|  int  |  4字节   | -2 147 483 648 ~ 2 147 483 647(刚刚超过20亿)           |
| short |  2字节   | -32 768 ~  32 767                                      |
| long  |  8字节   | -9 223 372 036 854 775 808 ~ 9 223 372 036 854 775 807 |
| byte  |  1字节   | -128 ~ 127                                             |

- 长整型数值有一个后缀L或l（如40000000L）
- 16进制数值有一个前缀0x或0X（如0xCAFE）
- 8进制数值有一个前缀0
- 2进制数值前缀为0b或0B
- 还可以在数字下面加下划线，如1_000_000，表示100万。下划线只是为了让人更容易读，Java编译器会去除这些下划线。

### 2. 浮点类型

|  类型  | 存储需求 | 取值范围                                               |
| :----: | :------: | ------------------------------------------------------ |
| float  |  4字节   | 大约$\pm$3.402 823 47E+38F(有效位数为6~7位)            |
| double |  8字节   | 大约$\pm$1.797 693 134 862 315 70E+308(有效位数为15位) |

- float类型的数值有一个后缀f或f（例如，3.14F）

- 没有后缀的浮点数默认为double类型

- double类型的数值也可以在后面加D或d（例如，3.14D）

- 三个特殊浮点数值：

  - 正无穷大：`Double.POSITIVE_INFINITY`

  - 正无穷小：`Double.NEGATIVE_INFINITY`

  - NaN（不是一个数字）：`Double.NaN`

    - ```
      if (x == Double.NaN) // 永远是false
      
      if (Double.isNaN(x)) // 这样判断一个double数是不是NaN
      ```

### 3. 枚举类型

```java
enum Size { SMALL, MEDIUM, LARGR, EXTAR_LARGE };
	public static void main(String[] args) {
        Size s = Size.SMALL;
    }
```

### 4. 运算符

如果将一个类标记为strictfp，那么这个类中所有的方法都将使用严格的浮点计算。

```java
public static strictfp void main(String[] args)
```

### 5. 数值之间的转换

当用一个二元运算符连接两个值时（例如n + f），先要将两个操作数转换为同一类型，然后再进行计算：

- 如果两个操作数中有一个是double类型，另一个操作数就会转换为double类型
- 否则，如果其中一个操作数是float类型，另一个操作数将会转换为float类型
- 否则，如果其中一个操作数是long类型，另一个操作数将会转换为long类型
- 否则，两个操作数都将被转换为int类型

### 6. 位运算

&(“and”)	|(“or”)	^(“xor”) 	~(“not”)

### 7. 运算符优先级

|                         运算符                          |  结合性  |
| :-----------------------------------------------------: | :------: |
|                   [] . () (方法调用)                    | 从左向右 |
| ! ~ ++ – +(一元运算) -(一元运算) ( ) (强制类型转换) new | 从右向左 |
|                          * / %                          | 从左向右 |
|                           + -                           | 从左向右 |
|                        << >> >>>                        | 从左向右 |
|                  <  <=  >=  instanceof                  | 从左向右 |
|                         ==  !=                          | 从左向右 |
|                            &                            | 从左向右 |
|                            ^                            | 从左向右 |
|                           \|                            | 从左向右 |
|                           &&                            | 从左向右 |
|                          \|\|                           | 从左向右 |
|                           ?:                            | 从右向左 |
|      =  +=  -=  *=  /=  %=  &=  \|=  <<=  >>= >>>=      | 从右向左 |

## 二、简单常用类

### 8. 字符串

Java中String类对象称为是`不可变的`

- 检测两个字符串是否相等可以用方法：`s.equals(t)`
- 不区分大小写比较是否相等用方法：`s.equalsIgnoreCase(t)`

#### 8.1 构建字符串

如果需要用许多小段的字符串来构建一个字符串，那么应该按照下列步骤进行。首先，创建一个空的字符串构建器：

```java
StringBuilder builder = new StringBuilder();
builder.append("context");
String completedString = builder.toString();
```

StringBuffer效率稍低，但允许多线程添加或删除字符串，如果是在单线程中操作，应该使用StringBuilder。这两个类的API是一样的。

### 9. 输入输出

#### 9.1 文件输入输出

```java
Scanner in = new Scanner(Path.of("file.txt"), StandardCharsets.UTF_8);

PrintWriter out = new PrintWriter("file.txt", StandardCharsets.UTF_8);
```





























