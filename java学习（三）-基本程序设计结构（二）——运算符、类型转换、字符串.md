#####运算符
***
与`&`、`|`相比，`&&`和`||`是按照“短路”方式求值的：如果第一个操作数已经能够确定表达式的值，第二个操作数就不必计算了。
`^`异或
`~`非 
`>>`和`<<`运算符将二进制位进行右移或左移操作。`>>>`运算符用0填充高位；`>>`用符号位填充高位。没有`<<<`运算符。
三元操作符`?:` ：表达式*`condition?expression1:expression2`*，当条件condition为真时计算第1个表达式，否则计算第2个表达式。

在Math类中，包含了各种各样的数学函数：
`sqrt(x)` 计算平方根
`pow(x,a)` 计算x的a次幂（两个参数为double型，返回结果也是double型）
常用三角函数：sin、cos、tan、atan、atan2
指数函数、自然对数和以10为底的对数：exp、log、log10
用于表示π和e常量的近似值：PI、E
#####类型转换
***
![数值类型之间的合法转换.jpg](http://upload-images.jianshu.io/upload_images/2702529-14ac4ad3bcab7b63.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
**强制类型转换**的语法格式是在圆括号中给出想要转换的目标类型，后面紧跟待转换的变量名。强制类型转换通过截断小数部分将浮点值转换为整型。
如果想对浮点数进行四舍五入运算，以便得到最接近的整数，需要用Math.round方法：
`double x = 9.997;
int nx = (int) Math.round(x);`


#####字符串
***
java没有内置的字符串类型，而是在标准java类库中提供了一个预定义类String。
由于不能修改java字符串中的字符，在java文档中将String类对象称为**不可变字符串**（比起字符型数组，java字符串更加像char*指针）。

`String substring(int beginIndex,int endIndex)`方法可以从一个较大的字符串提供出一个字串，其中第二个参数是**不想复制**的第一个位置。
`boolean equals(Object other)`方法检测两个字符串是否相等。
`boolean equalsIgnoreCase(String other)`方法检测两个字符串是否相等，而不区分大小写。
`String trim()`返回一个删除了原始字符串头部和尾部的空格的新字符串。
`int codePointAt(int index)`返回从给定位置开始或结束的代码点。
更多方法查看API文档。

如果需要由许多较短的字符串构建一个字符串，采用字符串连接的方式每次都会构建一个新的String对象，既耗时，又浪费空间。此时使用StringBuilder类可以提高效率：
首先，构建一个空的字符串构建器。每次需要添加一部分内容时，调用append方法。在需要构建字符串时就调用toString方法，得到一个包括构建器中的字符串的String对象。

相比StringBuilder类，StringBuffer效率稍低，但是线程安全的。因此：
如果要操作少量的数据用String；
单线程操作字符串缓冲区下操作大量数据用StringBuilder；
多线程操作字符串缓冲区下操作大量数据用StringBuffer。
