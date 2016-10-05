####应用程序首选项存储
#####属性映射
属性映射(property map)是一种存储键/值对的数据结构。属性映射经常被用来存放配置信息。它有三个特性：

* 键和值都是字符串。
* 键/值对可以很容易地写入文件或从文件读出。
* 用二级表存放默认值。

实现属性映射的java类被称为Properties。属性映射对指定程序的配置选项非常有用。例如：

`Properties settings = new Properties();`

`settings.put("width","200");`

`settings.put("title","Hello,world!");`

可以使用store方法将这个属性映射列表保存到文件中。在这里，将属性映射保存在Myprog.properties文件中。第二个参数是包含到这个文件的诸事。

`FileOutPutStream out = new FileOutPutStream("Myprog.properties");`

`settings.store(out,"Program Properties");`

想要从文件中加载这些属性，可以使用：

`FileInputStream in = new FileInputStream("Myprog.properties");`

`settings.load(in);`

要想查看用户的主目录，可以调用System.getProperties方法。还可以使用Properties对象描述系统信息。

Properties类有两种提供默认值的机制。第一种是在试图获得字符串值时指定默认值。当键值不存在时，就会自动地使用它：
`String title = settings.getProperty("title","Default title");`

如果觉得在每次调用getProperty方法时指定默认值太麻烦，那么就可以将所有的默认值放在一个二级映射中，并在主属性映射的构造器中提供映射。且用它来构造查询表：
`Properties defaultSettings = new Properties();`

`defaultSettings.put("width","300");`

`defaultSettings.put("height","200");`

`Properties settings = new Properties(defaultSettings);`

#####API java.util.Properties 1.0
* Properties getProperties() 获得全部系统属性。应用程序必须有访问全部系统属性的权限，否则将抛出安全异常。
* String getProperty(String key) 返回具有给定键名的系统属性。应用程序必须有访问全部系统属性的权限，否则将抛出安全异常。

#####API java.lang.System 1.0
* Properties(Properties defaults) 用一组默认值创建空的属性映射。
* String getProperty(String key, String defaultValue) 如果没有找到键，返回defaultValue字符串。如果键在表中出现，则返回对应键的字符串或默认字符串。

#####Preferences API
用的好像不多_(:3」∠)_ p464
