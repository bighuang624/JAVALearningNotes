### 输入输出（通过控制台）
***
#### 读取“标准输入流”：
1.构建Scanner对象（定义在java.util包中），并与“标准输入流”System.in关联：
`Scanner in = new Scanner(System.in);`

2.使用Scanner类的各种方法实现输入操作，如nextLine方法（输入行中可以有空格）：
`String aLine = in.nextLine;`

想要读取一个单词（以空白符为分隔符），调用next方法；

想要读取一个整数，调用nextInt方法；浮点数同理；

`boolean hasNext()`检测输入中是否还有其他单词。
#### 格式化输出：
java SE 5.0沿用了C语言库函数中的printf方法：

```java
System.out.printf("Hello, %s. Next year, you 'll be %d", name ,age);
System.out.printf("%fc", new Date());
```
这条语句将完整打印当前的日期和时间。

用于printf的转换符、用于printf的标志、日期和时间的转换符等信息查阅书本（p57-p60）。
#### 文件输入与输出：
要想对文件进行读取，需要用File对象构建一个Scanner对象：
`Scanner in = new Scanner(Paths.get("myfile.txt"));`
如果文件名中包含反斜杠符号，要在每个反斜杠之前再加一个额外的反斜杠,例如：“c:\\mydirectory\\myfile.txt”。之后用前面介绍的Scanner类的方法对文件进行读取。
如果用一个不存在的文件构建一个Scanner，或者用一个不能被创建的文件名构造一个PrintWriter，就会发生异常。

要想写入文件，需要构建一个PrintWriter对象。在构造器中，只需要提供文件名：
`PrintWriter out = new PrintWriter("myfile.txt");`
如果文件不存在，创建该文件。可以像输出到System.out一样使用print、println、printf命令。

### 控制流程
***
#### 多重选择：switch语句
`switch(choice){
    case 1:
    ...
    break;
    case 2:
    ...
    break;
    default:
    ...
    break;
}`
如果在case分支语句的末尾没有break语句，就会接着执行下一个case分支语句。

#### for each循环
`for(variable:collection) statement`定义一个变量用于暂存集合中的每一个元素，并执行相应语句。例如：
`for(int element:a)
    System.out.println(element);  //打印数组a的每一个元素，一个元素占一行。`
遍历数组中的每个元素时，for each循环语句的循环变量不需要使用下标值。
想要访问二维数组a的所有元素，需要使用两个嵌套的循环。
#### 中断控制流程语句
java提供了一种带标签的break语句，用于跳出多重嵌套的循环语句。标签必须放在希望跳出的最外层循环之前，并且必须紧跟着一个冒号。示例为if语句：
`label:
{
...
if(condition)  break label;    //exits block
...
}`

continue语句将控制转移到最内层循环的首部。如果将continue语句用于for循环中，就可以跳到for循环的“更新”部分。
### 大数值
***
如果基本的整数和浮点数精度不能够满足需求，那么可以使用java.math包中的两个类：BigInteger和BigDecimal。BigInteger类实现了任意精度的整数运算，BigDecimal实现了任意精度的浮点数运算。
使用静态的valueOf方法可以将普通的数值转化为大数值：
`BigInteger a = BigInteger.valueOf(100);`
处理大数值不能用运算符，而需要使用大数值类中的add和multiply方法：
`BigInteger d = c.multiply(b.add(BigInteger.valueOf(2)));    //d = c * (b+2)`

### 数组
***
和C++不同，java中习惯在声明时把数组类型和变量名分开，如：`int[] a;`
在java中，允许数组长度为0（与null不同）。
#### 数组拷贝
在java中，允许将一个数组变量拷贝给另一个数组变量。这时，两个变量将引用同一个数组：

```java
int[] a = b;
a[4] = 12;    // now b[4] is also 12
```
如果希望将一个数组的所有值拷贝到一个新的数组中去，就要使用Arrays类的copyOf方法。
#### 命令行参数
每一个java应用程序都带有一个带String arg[]参数的main方法。这个参数表明main方法将接收一个字符串数组，也就是命令行参数。
#### Arrays类的常用方法
`static void sort(type[] a)`  采用优化的快速排序算法对数组进行排序。

`static int binarySearch(type[] a, int start, int end, type v)`    采用二分搜索算法查找值v（与a的数据元素类型相同）。如果查找成功，则返回相应的下标值；否则，返回一个负数值r。-r-1是为保持a有序v应插入的位置。

`static boolean equals(ttype[] a, type[] b)`    如果两个数组大小相同，并且下标相同的元素都对应相等，返回true。
#### 多维数组
java实际上没有多维数组，只有一维数组。多维数组被解释为“数组的数组”。因此，java中可以构建“不规则”数组。
