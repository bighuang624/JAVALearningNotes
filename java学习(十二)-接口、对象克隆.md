####接口
接口不是类，尤其不能使用new运算符实例化一个接口。但尽管不能构造接口的对象，却能声明接口的变量：
`Comparable x;    //OK`

接口变量必须引用实现了接口的类对象。

如同使用instanceof检查一个对象是否属于某个特定类一样，也可以使用instanceof检查一个对象是否实现了某个特定接口。

虽然在接口中不能包含实例域或静态方法，但可以包含常量。
####对象克隆
当拷贝一个变量时，原始变量与拷贝变量引用同一对象。这就是说，改变一个变量所引用的对象将会对另一个变量产生影响：
`Employee original = new Employee("Huang",50000);`
`Employee copy = original;`
`copy.raiseSalary(10); //also changed original`

而clone方法可以创建最初状态相同，能单独改变状态的对象：
`Employee copy = original.clone();`
`copy.raiseSalary(10); //original unchanged`

但是，默认的克隆操作是**浅拷贝**，并没有克隆包含对象中的内部对象。即如果在对象中包含了子对象的引用，拷贝的结果会使得两个域引用同一个子对象，因此原始对象与克隆对象共享这一部分信息。

如果原始对象与浅克隆对象共享的子对象是**不可变的**，将不会产生任何问题（例如子对象属于像String类这样不允许改变的类；也有可能子对象在其生命周期内不会发生变化，既没有更改它们的方法，也没有创建对它产生引用的方法）。

然而，更常见的情况是子对象可变，因此必须重新定义clone方法，以实现克隆子对象的**深拷贝**。此时类必须实现Cloneable接口，并且使用public访问修饰符重新定义clone方法。

在这里Cloneable接口只是一个标记，表明类设计者知道要进行克隆处理。它并没有指定clone方法。如果一个对象需要克隆，而没有实现Cloneable接口，就会产生一个**已检验异常**。因此需要声明异常：
`public Employee clone() throws CloneNotSupportedException`

即使clone的默认实现（浅拷贝）能够满足需求，也应该实现Cloneable接口，将clone重定义为public，并调用super.clone()。










