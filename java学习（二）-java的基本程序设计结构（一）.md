java中所有函数都属于某个类的方法。因此，java中的main方法必须有个外壳类。
### 数据类型
***
#### java整型
int(4字节)、short(2字节)、long(8字节)、byte(1字节)
长整型数值有一个后缀L，十六进制数值有一个前缀0x，八进制有一个前缀0。从java7开始，加上前缀0b就可以写二进制数。

#### java浮点类型
float(4字节)、double(8字节)
float类型的数值有一个后缀F，没有的浮点数值默认为double类型。
下面是用于表示溢出和出错情况的三个特殊的浮点数值：
1.正无穷大，用常量Double.POSITION_INFINITY表示
2.负无穷大，用Double.NEGATIVE_INFINITY表示
3.NaN（不是一个数字），用Double.NaN表示
可以使用Double.isNaN(x)方法检测特定值x是否等于Double.NaN。

#### char类型
转义序列 | 名称 | Unicode值
:------: | :--: | :--------:
\b | 退格 | \u0008
\t  | 制表 | \u0009
\n  | 换行 | \u000a
\r | 回车 | \u000d
\''  | 双引号 | \u0022
\'  | 单引号 | \u0027
\\\  | 反斜杠 | \u005c
#### boolean类型
在java中，整型类和布尔值之间不能进行相互转换。

### 变量
***
在java中，利用关键字final指示常量，表示这个变量只能被赋值一次，之后不能更改。习惯上常量名使用全大写。
可以使用关键字static final设置类常量。
