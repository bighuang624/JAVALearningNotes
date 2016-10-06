####异常
#####异常分类
所有的异常都是由Throwable继承而来，但在下一层立即分解为两个分支：Error和Exception。

Error类层次结构描述了Java运行时系统的内部错误和资源耗尽错误。应用程序不应该抛出这种类型的对象。这种情况很少出现。

Exception层次结构分解为两个分支：一个分支派生于RuntimeException；另一个分支包含其他异常。由程序错误导致的异常属于RuntimeException；而程序本身没有问题，但由于像I/O错误这类问题导致的异常属于其他异常。

Java语言规范将派生于Error类或RuntimeException类的所有异常称为*未检查(unchecked)*异常，所有其他的异常称为*已检查(checked)*异常。编译器将检查是否为所有的已检查异常提供了异常处理器。

#####再次抛出异常和异常链
在catch语句中可以抛出一个异常，这样做的目的是改变异常的类型。如果开发了一个供其他程序员使用的子系统，那么，用于表示子系统故障的异常类型可能会产生多种解释。

强烈建议使用如下的包装技术：

`try{`

&nbsp; &nbsp; *`access the database`*

`}catch(SQLException e){`

&nbsp; &nbsp; `Throwable se = new ServletException("database error");`

&nbsp; &nbsp; `se.initCause(e);`

&nbsp; &nbsp; `throw se;`

`}`

当捕获到异常时，就可以使用下面这条语句重新得到原始异常：

`Throwable e = se.getCause();`

这样可以让用户抛出子系统中的高级异常，而不会丢失原始异常的细节。

#####带资源的try语句

带资源的try语句(try-with-resources)的最简形式为：

`try(Resorce res = ...){`

&nbsp; &nbsp; *`work with res`*

`}`

try块退出时，会自动调用res.close()。例如这里要读取一个文件中的所有单词：

`try(Scanner in = new Scanner(new FileInputStream("/usr/share/dict/words"))){`

&nbsp; &nbsp; `while(in.hasNext())`

&nbsp; &nbsp; &nbsp; &nbsp; `System.out.println(in.next());`

`}`

这个块正常退出时，或者存在一个异常时，都会调用in.close()方法，就好像使用了finally块一样。

只要需要关闭资源，就要尽可能使用带资源的try语句。

#####分析堆栈跟踪元素

*堆栈跟踪(stack trace)*是一个方法调用过程的列表，它包含了程序执行过程中方法调用的特定位置。可以调用Throwable类的printStackTrace方法访问堆栈跟踪的文本描述信息。

一种更灵活的方法是使用getStackTrace方法，它会得到StackTraceElement对象的一个数组，可以在你的程序中分析这个对象数组。例如：

`Throwable t = new Throwable();`

`StackTraceElement[] frames = t.getStackTrace();`

`for(StackTraceElement frame : frames)`

&nbsp; &nbsp; *`analyze frame`*

StackTraceElement类含有能够获得文件名和当前执行的代码行号的方法，同时，还含有能够获得类名和方法名的方法。