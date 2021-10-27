---

---

## 1.注释

​	java的注释不会出现在可执行代码中，因此可以在源程序中添加任意多的注释，不必担心可执行代码的膨胀。

- //  行注释

- /*    */  多行注释

- /**   */ 多行注释（可以自动生成文档）

  

## 2.数据类型

​	java是一种强类型语言，即每一个变量声明一种类型。java中一共有8种基本数据类型。4种整型，2种浮点型，1种表示Unicode编码的字符单元字符型char，1种表示真值的boolean类型

- 整型（int  short long  byte)

  int最为常用，long用于数据很大的情况，byte和short主要用于特定的场合，如底层文件处理或者是需要控制占用存储空间量的大数组。

  java中整型的范围与运行java代码的机器无关。这解决了软件从一个平台移植到另一个平台，或是从同一个平台的不同操作系统间移植的许多问题。但如C或C++为了针对不同的处理器选择最为高效的整型，这就可能造成一个在32位系统上运行很好的程序在16位系统上发生整数溢出的问题。

- 浮点型（float double)

  double类型的数值精度是float的两倍，绝大多数的程序使用double类型。

- char型

  char类型原本表示单个字符。现在有些Unicode字符可以使用一个char表示，另外的Unicode字符则需要两个char字符。

  | 转义序列 | 名称   | Unicode值 |
  | -------- | ------ | --------- |
  | \b       | 退格   | \u0008    |
  | \t       | 制表   | \u0009    |
  | \n       | 换行   | \u000a    |
  | \r       | 回车   | \u000d    |
  | \"       | 双引号 | \u0022    |
  | \'       | 单引号 | \u0027    |

  强烈建议不要在程序中使用char类型，除非其实要处理UTF-16代码单元。

- boolean类型

  ​	boolean有两个值，false和true，用来判断逻辑条件。java中整型和boolean不能相互转换。

## 3.变量

- ​	变量初始化

  声明一个变量后，必须使用赋值语句对变量进行显示初始化，不要使用未初始化的变量。

- 常量

  java中使用关键字final指示常量。如

  final double CM = 2.76;

  final关键字表示这个值只能被赋值一次，同时常量名使用大写。

  - 类常量：某个常量可以在类中的多个方法中使用，使用关键字static final 设置一个类常量。如

    ```java
    public class Constants{
        public static final double CM = 2.77;
        public static  void main(String[] args){
            double paperWitdth = 8.3;
            double paperHeight = 12;
            System.out.println("paper size in centimeter:"+paperWidth*CM+"by"+paperHeigth*CM);
        }
    }
    ```

## 4.运算符

​	在java中，使用算术运算符+，-，*，/运算，当参与运算的两个操作数都是整数时，结果为整数（向下取整），%为取模操作。整数被0除会产生一个异常。而浮点数被0除则会得到无穷大（Infinity）或是NaN（非数，意思是不是一个有效的数）结果。

- 数学函数与常量

  Math类中，包含了各种各样的数学函数

  - 计算5的平方根

  `double y = Math.sqrt(5);`

  - java中没有幂运算，要借助pow方法，计算x的a次幂

  `double y = Math.pow(x,a);`

- Math中的一些常用方法

  - Math.sin()，Math.cos()，Math.tan()，Math.exp，Math.log()，Math.PI，Math.E

    Math.round()：相当于对浮点数进行四舍五入，其返回值的类型为long类型

    Math.random():返回一个0~1之间的浮点数（不包含1）

    `int r = (int) Math.random()*n;`

    返回一个0~n-1之间的整数

- 数值类型之间的转换

  数值类型向字节高的转换，int->long->float->double

  有一些转换会使得精度损失

- 强制类型转换

  ```java
  double x = 9,999;
  int nx = (int) Math.round(x);
  ```

- 结合赋值和运算符

  `x += 4;`(+=，*=，%=)

  如果运算符得到的值类型和左侧操作数类型不同，就会发生强制类型转换。

- 自增和自减运算符

  前缀形式会先加1或者减1，而后缀形式则会先使用变量原来的值。

  建议尽量不要在表达式中使用++

- 关系和boolean运算符

  （== <= >= && ||)

## 5.字符串

​	从概念上说，java字符串就是Unicode字符序列，java中没有内置的字符串类型，而是在标准的java类库中提供了一个预定义类，每个双引号括起来的字符串都是String类的一个实例。

- 子串

  String类中的substring方法可以从较大的字符串找那个提取出一个子串。

  ```java
  String greeting = "Hello";
  String s = greeting.substring(0,3);
  ```

  结果为"Hel"，substring(a,b)子串的长度为b-a

- 拼接

  和大多语言一样，java允许使用"+"拼接字符串

  如果需要把多个字符串连接在一起，同时使用一个定界符进行分隔可以使用静态的join()方法

  ```java
  String all = String.join("*","wu","wu","hiya");
  // all = "wu*wu*hiya";
  ```

- 不可变字符串

  String类没有提供用于修改字符串的方法，当然可以这样替换

  `greeting  = greeting.substring(0,3)+"p!";`

  java文档中将String类对象称为不可变字符串，当然不可变字符串也有其优点，就是可以实现字符串共享；即各种字符串存放在公共的存储池中，字符串变量指向存储池中相应的位置。

- 检测字符串是否相等

  可以使用equals()方法检测两字符串是否相等。

  `s.equals(t)`;

  不区分大小写，检测两字符串是否相等

  `s.equalsIgnoreCase("hello")`;

  不能使用==检测两字符串是否相等，==只能检测两个字符串是否放置在同一个位置。事实上，只有字符串常量才是共享的，像+和substring等操作产生的结果不是共享的，不能使用==检测。

- 空串和null串

  空串是字符长度为0的字符串。空串是一个java对象，有自己的长度0，和内容（空）。但是String 变量还可以存放一个特殊的值叫null，表示目前没有任何对象与该变量关联。

  有时要检查一个字符串既不是null也不是空串

  `if(str!=null&&str.length()!=0){}`

  通常会先检查是否为null，一个null调用方法，会出现错误

- 码点与代码单元

  java字符串由char值序列组成，char数据类型是一个采用UTF-16编码表示的Unicode码点的代码单元，大多数常用的Unicode字符可以使用一个代码单元表示，而辅助字符需要一定代码单元表示。

  - 使用length（）方法可以返回采用UTF-16编码表示的给定字符串所需要代码单元的数量。

    ```java
    String greeting = "hiya\n";
    System.out.println(greeting.length());
    ```

    输出结果为 5

  - 使用s.charAt(i)，可以返回位置i的代码单元

  - 常用的String方法

    | 方法                                             | 作用                                                         |
    | ------------------------------------------------ | ------------------------------------------------------------ |
    | char charAt(int index)                           | 返回给定位置的代码单元                                       |
    | int codePointAt（int index）                     | 返回给定位置开始的码点                                       |
    | int compateTo(String other)                      | 如果字符串位于other之后返回整数，相等返回0，之前返回负数     |
    | IntStream codePoints()                           | 将一个字符串的码点作为一个流返回，调用toArray将他们放在一个数组中 |
    | equals(Object other)                             | 字符串与other进行比较                                        |
    | equalsIgnoreCase(String other)                   | 忽略大小写，比较                                             |
    | int indexOf(String str)                          | 返回与str匹配的第一个子串位置                                |
    | boolean startsWith（String str）                 | 判断是否以str开头                                            |
    | boolean endWith(String str)                      | 判断是否以st结尾                                             |
    | int length()                                     | 返回字符串长度                                               |
    | String substring(int beginIndex)                 | 返回从beginIndex开始到结尾的一个子串                         |
    | String substring(int beginIndex,int endIndex)    | 返回一个从...的子串                                          |
    | String toLowerCase()                             | 将字符串全部小写（新字符串）                                 |
    | String toUpperCase()                             | 将字符串全部大写                                             |
    | String join(charSequence char,elements,elements) | 用给定的定界符，连接所有字符串                               |

  - 构造字符串StringBuilder

    使用StringBuilder类可以很方便的进行字符串的构造。

    `StringBuilder builder = new StringBuilder();`

    添加内容append()，可以链式编程

    `builder.append("hhh").append("hiya");`

    转换为字符串 toString();

    `String s = builder.toString();`

    当然从String到StringBuilder可以如下

    `String s = "hiya";`

    `StringBuilder sb = new StringBuilder(s);`

    | 方法                                        | 作用                                                 |
    | ------------------------------------------- | ---------------------------------------------------- |
    | StringBuilder()                             | 构造一个空的字符串构造器                             |
    | int length()                                | 返回构造器中代码单元数量                             |
    | StringBuilder append(String str)            | 追加一个字符串str，并返回this                        |
    | StringBuilder appendCodePoint(int cp)       | 追加一个代码点，并将其转化为相应代码单元，并返回this |
    | void setCharAt(int i,char c)                | 将第i个代码单元设置为c                               |
    | StringBuilder insert(int offset,String str) | 将字符串str，插入offset位置                          |
    | StringBuilder delete(int start,int end)     | 删除相应位置的代码单元                               |
    | String toString()                           | 返回相应的字符串                                     |

    

## 6.输入输出

​	标准输出流，即调用`System.out.println(" ");`

​    标准输出流，通常需要先构造一个Scanner对象，并与标准输入流相关联。

    ```java
    Scanner sc = new Scanner(System.in);
    String name = sc.nextLine();//输入行中，有空格
    String hiya = sc.next();//输入字符串没有空格
    int num = sc.nextInt(); //输入为整数数据
    double num = sc.nextDouble();//输入为浮点数数据
    ```

- 除了以上常用的方法，还有

  `boolean hasNext();`检测输入中是否还有其他单词

  `boolean hasNextInt();`检测输入中是否还有整数

  `boolean hasNextDouble();`检测输入中是否还有浮点数

- 格式化输出

  使用`System.out.printf("hello,%s,next year, you will be %d",name, age);`

  每个以%开始的格式说明符都用了相应的参数替换，用于printf的转换符

  | 转换符 | 类型         |
  | ------ | ------------ |
  | d      | 十进制整数   |
  | x      | 十六进制整数 |
  | o      | 八进制整数   |
  | f      | 定点浮点数   |
  | s      | 字符串       |
  | c      | 字符         |
  | b      | 布尔值       |

  同时还可以给控制格式化输出各种标志。

  `System.out.printf("%,.2f",1000.0/3);`

  输出为 3,333.33;

  | +    | 打印正数和负数符号   |
  | ---- | -------------------- |
  | 空格 | 正数前添加空格       |
  | 0    | 在数字面前补0        |
  | -    | 左对齐               |
  | (    | 将负数括在括号内     |
  | ，   | 添加分组分隔符       |
  | $    | 给定格式化的参数索引 |

- 文件的输入与输出

  想要对文件进行读取，就需要用File对象构造一个Scanner对象

  `Scanner sc = new Scanner(Path.get("myfile.txt"),"UTF-8");`

  此时可以使用之前的nextInt(), nextLine()等方法进行操作

​       注意如果文件名包含反斜杠，需要在反斜杠处额外加一个反斜杠

​       如："c:\\\\ user\\\\ myfile.txt"

​       如果要写入文件，就需要构造一个PrintWriter对象

​      `PrintWriter out=PrintWrinter("file.txt","UTF-8");`

## 7.控制流程

- 块作用域，不能在嵌套的两个块中声明同名的变量

- 条件语句
- 循环
  - while(){}
  - do{}while()
  - for(){} 注意该循环的顺序
  - for(each) 加强for循环

- 多重选择 switch语句 

   switch(choice){

   		case 1:

  ​        ...break;

  ​        case 2:

  ​        ...break;

  ​        default:

  ​        ...break;

  } 

  case可以是 char，byte，short，int的常量表达式等

- 中断控制流程

  break 跳出当下循环

  continue 越过当前循环体的剩余部分

  java中还提供了跳出多重循环的带标签的break语句

  ```java
  int n;
  read_date:
  while(...){
  	for(...){
  		for(...){
  		if(n<0) break read_date;
              //此时直接跳出多重循环
  		}
  	}
  }
  ```

## 8.大数值

​	如果基本的整数和浮点数精度不能满足需求，可以使用java.math包中的类：BigInteger和BigDecimal，这两个类可以处理包含任意长度数字序列的数值，前者实现任意精度整数运算，后者实现任意精度的浮点数运算。

- 可以使用静态方法valueOf()方法将普通的数值转换为大数值

  `BigInteger a = BigInteger.valueOf(100);`

- 同时不能使用熟悉的算术运算符处理大数值，如（+ *），但可以使用类中的add和multiply方法

  ```java
  BigInteger c = a.add(b); //c = a+b;
  BigInteger d = c.multipy(b.add(BigInteger.valueOf(2)));
  //d = c*(b+2)
  ```

## 9.数组

​	数组是一种数据结构，用于存储同一类型值的集合。通过整型下标可以访问数组的每一个值。

创建并初始化一个数组

`int[] a = new int[100];`

可以使用a.length获得数组个数，同时一旦创建了数组，就不能改变它的大小了，如果需要经常扩展数组的大小，就应该使用另一种数据结构--数组列表。

- 数组初始化

  java中提供了一种创建数组对象并同时赋予初始值的简化书写形式。

  `int[] smallPrimes = {2,4,5,6,7,3};`

  甚至可以初始化一个匿名数组

  `new int[] {14,2,45,32,34};`使用这种语法可以在不创建新变量的情况下重新初始化一个数组。

- 数组拷贝

  在java中，允许将一个数组变量拷贝到另一个数组变量中，此时两个变量将引用同一个数组，即两个变量指向同一个地址。

  ```
  int[] luckNum = smallPrimes[5];
  luckNum[5] = 12;//now smallPrimes[5] = 12;
  ```

  

  如果希望将一个数组的所有值拷贝到一个新的数组中，就要使用到Arrays类中copyOf方法。

  `int[] copiedLuckyNumbers = Arrays.copyOf(luckNum,luckNum.length);`

- 命令行参数

  每个java程序都有一个带String[] args 参数的方法，这个参数表明main方法将接收一个字符串数组，即我们命令行输入的字符串。

- 数组排序

  想要对数组进行排序，可以使用Arrays类中的sort()方法。

  `Arrays.sort(a);`

- Arrays的一些方法

  | 方法                                                         | 作用                                               |
  | ------------------------------------------------------------ | -------------------------------------------------- |
  | static String toString(type[] a)                             | 返回a中数据元素的字符串，放在括号内，并用逗号分隔  |
  | static type copyOf(type[] a, int length)                     | 如果length>a.length后面元素为0或false              |
  | static type copyOf(type[] a, int start,int end)              | 返回一个与a相同的数组，长度为length，或者end-start |
  | static void sort(type[] a)                                   | 优化后的快速排序算法                               |
  | static int binarySearch(type[] a,type v)                     | 二分法查找v                                        |
  | static int binarySearch(type[] a, type v, int start,int end) |                                                    |
  | static void fill(type[] a,type v)                            | 将数组所有元素设置为v                              |
  | static boolean equals(type[] a,type[] b)                     | 判断两数组是否相等                                 |

- 多维数组，如二维数组，即矩阵。此时可以进行一些矩阵的操作，如对角线遍历，矩阵的翻转，以及零矩阵。