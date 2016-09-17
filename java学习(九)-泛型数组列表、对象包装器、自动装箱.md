####泛型数组列表
ArrayList在添加或删除元素时，具有自动调节数组容量的功能，而不需要为此编写任何代码。

ArrayList是一个采用*类型参数*的*泛型类*。为了指定数组列表保存的元素对象类型，需要用一对尖括号将类名括起来加在后面。
声明和构造一个保存Employee对象的数组列表：
`ArrayList<Employee> staff = new ArrayList<Employee>();`

java7中，可以省去右边的类型参数：
`ArrayList<Employee> staff = new ArrayList<>();`

ArrayList<T>()

构造一个空数组列表。

ArrayList<T>(int initialCapacity)

用指定容量构造一个空数组列表。

boolean add(T obj)

在数组列表的尾端添加一个元素。永远返回true。

int size()

返回存储在数组列表中的当前元素数量。(这个值将小于或等于数组列表的容量)

void ensureCapacity(int capacity)

确保数组列表在不重新分配存储空间的情况下就能够保存给定数量的元素。

void trimToSize()

将数组列表的存储容量削减到当前尺寸。

void set(int index,T obj)

设置数组列表指定位置的元素值，这个操作将覆盖这个位置的原有内容。

T get(int index)

获得指定位置的元素值。

void add(int index,T obj)

向后移动元素，以便插入元素。

T remove(int index)

删除一个元素，并将后面的元素向前移动。被删除的元素由返回值返回。

####对象包装器
所有基本类型都有一个与之对应的类，通常称为*包装器*：Integer、Long、Float、Double、Short、Byte、Character、Void和Boolean。

对象包装器类是不可变的，即一旦构造了包装器，就不允许更改包装在其中的值。同时，对象包装器类还是final，因此不能定义它们的子类。

尖括号中的类型参数不允许是基本类型，所以想定义一个整形数组列表时，可以声明一个Integer对象的数组列表（由于每个值分别包装在对象中，所以ArrayList<Integer>的效率远低于int[]数组）。

####自动装箱
Java SE 5.0的另一个改进之处是更加便于添加或获得数组元素。下面这个调用`list.add(3)；`将自动变换成`list.add(Integer.valueOf(3));`
这种变换被称为自动装箱。

自动装箱：把基本类型用它们对应的引用类型包装起来，使它们具有对象的特质，可以调用toString()、hashCode()、getClass()、equals()等方法。

拆箱：跟自动装箱的方向相反，将Integer及Double这样的引用类型的对象重新简化为基本类型的数据。

**编译器**认可装箱和拆箱，在生成类的字节码时，根据语法判断是否插入必要的方法调用。虚拟机只是执行这些字节码。

