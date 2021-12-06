# Java 知识点

## problems

* 声明类型是父类
  运用多态时，引用类型可以是实际对象类型的父类
```java
Animal Dog = new Dog();
```

* 为什么不直接声明 ArrayList<int>?

generic 泛型，规则是你只能指定类或接口类型。
generic 泛型类型在 JDK 5 中引入，泛型提供了编译时期类型安全检测机制，该机制允许程序员在编译器检测到非法的类型。

## note
* 实例变量永远都会有默认值。即使没有明确的赋值给实例变量。
  integer 0, float 0.0, boolean false, reference null.
* 局部变量没有默认值，如果在变量被初始前就使用的话，编译器你会显示错误。
* 使用 == 来比对 pribitive 数据是否相等， == 来判断两个引用是否都指向同
一对象。用 equals() 来判断两个对象是否在意义上是否相等。
* 其实真的有这样的集合，但它不是数组，而是 ArrayList, 它是 Java 函数库中
的另一个类。
* &&, || 短运算符，&，|长运算符。
* import 只是省下每个类前面的包名称，不会因为用了 import 而变大或变慢。
* java.lang 是个预先被引用的包，因为 java.lang 是个经常会用到的基础包，
所以你可以不必指定名称。  
* 方法的搜索，Java 虚拟机从继承关系的树形图最下方开始搜索方法，编译器会保证
引用特定的方法是一定能够被调用到，但在执行期它不会在乎该方法实际上是从哪个类
找到的。
* 继承
  子类是 extends 父类出来的，子类会继承父类所有 public 类型的实例变量和方法，但不会
  继承父类所有 private 类型的变量和方法。
  继承下来的方法可以被覆盖掉，但实例变量不会被覆盖掉。
  当每个方法在子类中被覆盖过，调用这个方法时会调用到赴该国的版本。

 * IO
 字节
 字符
 抽象类 Reader/Writer
 InputStream/OutputStream
 File
 Path
 FileInputStream/FileOutputStream
  Closeable 接口
  Serializable
  Comparable
  File

* 文件

## JSP - Java Server Pages

what ? JSP 是解决 Servlet 输出 HTML 问题的，JSP 本质就是 Servlet。

* JSP 脚本
`<%%>`定义局部变量，编写语句
`<%=%>`表达式输出
`<%!%>`定义类或方法

* JSP 指令
`<%@指令 属性名="值"%>`, page, include, taglib

* JSP 行为
`<jsp:action>`
attribute, body, element, forward, getProperty, include, param, params, plugin, root, setProperty, text, useBean
JavaBean:
```jsp
<jsp:useBean>,在 JSP 页面查找 JavaBean 对象或实例化 JavaBean 对象。
<jsp:setProperty> 设置 JavaBean 的属性
<jsp:getProperty> 获取 JavaBean 的属性
```

* directive 行为
该行为就是代替指令`<%@%>`语法的，相当于`<%@include file=""%>`，相当于`<%@page %>`，相当于`<%@taglib%>`
```java
<jsp:directirve.include file="head.jsp"></jsp:directive.include>
<jsp:directirve.include file="foot.jsp"></jsp:directive.include>
```

### JSTL 
* 什么是EL表达式？
表达式语言（Expression Language，EL）,EL表达式是用"${}"括起来的脚本，用来更方便的读取对象！
EL表达式主要用来读取数据，进行内容的显示！
ServletContext对象的时候讲过一个方法findAttribute(String name),EL表达式语句在执行的时候会调用该方法，用标识符作为关键字分别从page、request、session、application四个域中查找相应的对象。这也解释了为什么EL表达式可以仅仅通过标识符就能够获取到存进域对象的数据！
findAttribute()的查找顺序：从小到大，也就是page->request->session->application
EL表达式主要是来对内容的显示，为了显示的方便，EL表达式提供了11个内置对象。
pageContext    对应于JSP页面中的pageContext对象（注意：取的是pageContext对象）
pageScope    代表page域中用于保存属性的Map对象
requestScope    代表request域中用于保存属性的Map对象
sessionScope    代表session域中用于保存属性的Map对象
applicationScope    代表application域中用于保存属性的Map对象
param    表示一个保存了所有请求参数的Map对象
paramValues表示一个保存了所有请求参数的Map对象，它对于某个请求参数，返回的是一个string[]
header    表示一个保存了所有http请求头字段的Map对象
headerValues同上，返回string[]数组。
cookie    表示一个保存了所有cookie的Map对象
initParam    表示一个保存了所有web应用初始化参数的map对象
