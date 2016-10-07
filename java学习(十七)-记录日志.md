###记录日志

记录日志API的优点：

* 可以很容易地取消全部日志记录，或者仅仅取消某个级别的日志，而且打开和关闭这个操作也很容易。
* 可以很简单地禁止日志记录的输出，因此，将这些日志代码留在程序中的开销很小。
* 日志记录可以被定向到不同的处理器，用于在控制台中显示，用于存储在文件中等。
* 日志记录器和处理器都可以对记录进行过滤。过滤器可以根据过滤实现器制定的标准丢弃那些无用的记录项。
* 日志记录可以采用不同的方式格式化，例如，纯文本或XML。
* 应用程序可以使用多个日志记录器，它们使用类似包名的这种具有层次结构的名字，例如，com.mycompany.myapp。
* 在默认情况下，日志系统的配置由配置文件控制。如果需要的话，应用程序可以替换这个配置。

####基本日志

日志系统管理着一个名为Logger.global的默认日志记录器，可以通过调用info方法记录日志信息：

`Logger.getGlobal().info("File->Open menu item selected");`

在相应的地方调用`Logger.getGlobal().setLevel(Level.OFF);`将会取消所有的日志。

####高级日志

在一个专业的应用程序中，不要将所有的日志都记录到一个全局日志记录器中，而是可以自定义的日志记录器。

调用getLogger方法可以创建或检索记录器：

`private static final Logger myLogger = Logger.getLogger("com.mycompany.myapp");`

与包名类似，日志记录器名也具有层次结构，且其层次性更强。对于包来说，一个包的名字与其父包的名字之间没有语义关系，但是日志记录器的父与子之间将共享某些属性，例如日志级别。

通常，有以下7个日志记录器级别：

* SEVERE
* WARNING
* INFO
* CONFIG
* FINE
* FINER
* FINEST

在默认情况下，只记录前三个级别。也可以设置其他的级别。例如，

`logger.setLevel(level.FINE)；`

现在，FINE和更高级别的记录都可以记录下来。

另外，还可以使用Level.ALL开启所有级别的记录，或者使用Level.OFF关闭所有级别的记录。

对于所有的级别有下面几种记录方法：

`logger.warning(massage);`

`logger.fine(massage);`

同时，还可以使用log方法指定级别，例如：

`logger.log(Level.FINE, message);`

**默认的日志配置记录了INFO或更高级别的所有记录，因此，应该使用CONFIG、FINE、FINER和FINEST级别来记录那些有助于诊断，但对于程序员又没有太大意义的调试信息。同时，如果将记录级别设计为INFO或者更低，则需要修改日志处理器的配置。**


～～～有很多暂时感觉用不到的东西～～～

####日志记录说明

一些常用操作：

1. 为一个简单的应用程序，选择一个日志记录器，并把日志记录器命名为与主应用程序包一样的名字，例如：com.mycompany.myprog。另外，可以通过调用下列方法得到日志记录器。
`Logger logger = Logger.getLogger("com.mycompany.myprog");`
为了方便起见，可能希望利用一些日志操作将下面的静态域添加到类中：
`private static final Logger logger = Logger.getLogger("com.mycompany.myprog");`

2. 默认的日志配置将级别等于或高于INFO级别的所有消息记录到控制台。用户可以覆盖默认的配置文件。但改变配置需要做相当多的工作。因此，最好在应用程序中安装一个更加适宜的默认配置。

3. 所有级别为INFO、WARNING和SEVERE的消息都将显示到控制台上。因此，最好只讲对程序用户有意义的消息设置为这几个级别。将程序员想要的日志记录，设定为FINE是一个很好的选择。



