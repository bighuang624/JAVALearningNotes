####JAR文件和资源
在applet和应用程序中使用的类通常需要使用的一些相关的数据文件被称作**资源**。将这些文件和其他程序文件一起放在JAR文件中是最方便的。

类加载器知道如何搜索类文件，直到在类路径、存档文件或web服务器上找到为止。利用资源机制，对于非类文件也可以同样方便地进行操作。下面是必要的步骤：

1. 获得具有资源的Class文件，例如，AboutPanel.class。
2. 如果资源是一个图像或声音文件，那么就需要调用getResource(filename)获得作为URL的资源位置，然后利用getImage或getAudioClip方法进行读取。例如：
`URL url = ResourseTest.class.getResource("about.gif");`
`Image img = new ImageIcon(url).getImage();`
3. 与图像或声音文件不同，其他资源可以使用getResourceAsStream方法读取文件中的数据。例如：
`InputStream stream = ResourceTest.class.getResourceAsStream("about.txt");`
`Scanner in = new Scanner(stream);`

除了可以将资源文件与类文件放在同一个目录中外，还可以将它放在子目录中。可以使用下面所示的层级资源名：`data/text/about.txt`
这是一个相对的资源名，它会被解释为相对于加载这个资源的类的所在包。必须使用"/"作为分隔符，而不要理睬存储资源文件的系统实际使用哪种目录分隔符。

一个以"/"开头的资源名被称为绝对资源名。它的定位方式与类在包中的定位方式一样。例如`/corejava/title.txt`定位于corejava目录下。