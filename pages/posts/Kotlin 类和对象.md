---
title: Kotlin 类和对象
date: 2019/1/11
description: Kotlin 类和对象
tag: Kotlin
author: shiyd
---

## 类与继承

Kotlin 中使用关键字 class 声明类，由类名、类头、以及由花括号组成。如果没有类体，则无需花括号

```kotlin
class Invoice { /*类体*/}
// 无类体
class Empty
```

#### 构造函数（constructor）

在 kolin 中可以有一个 **主构造函数**以及一个或多个此构造函数。主构造函数是类头的一部分：它跟在类名与可选参数的后面

```kotlin
class Person constructor(firstName: String){/*......*/}
```

如果主构造函数没有任何注解或者可见性修饰符，可以省略这个 *constructor* 关键字。

- kotlin 中的构造函数

```kotlin
class Person(firstName: String) { /*……*/ }

// Kotlin 声明属性以及从主构造函数初始化属性的简洁方法
class Person(
	val firstName: String,
    val lastName: String,
    var age: Int
){/*......*/}
```

#### Kotlin 构造函数 demo

```kotlin
class person constructor(username: String) {
    private var username: String
    private var age: Int
    private var address: String
    init {
        println(username)
        
        this.username = username
        this.age = 20
        this.address = "shanghai"
    }
    constructor (username: String, age: Int): this(username) {
        this.username = username
        this.age = age
        this.address = address
    }
    constructor (username: String, age Int, address: String): this(username, age) {
        this.adress = address
    }
    
    fun printInfo () {
        println("username: ${this.username}, age: ${age}, address: ${address}")
    }
}

fun main(){
    var person01 = person("zhangsan")
    var person02 = person("lisi", 20)
    var person03 = person("wangwu", 18, "tianshui")
    
    person01.printInfo()
    person02.printInfo()
    person03.printInfo()
}
```

- Java 中的构造函数，构造函数签名和类名完全相同

```java
public class TestConstructor {
    String name;
    Integer age;
    char sex;
    /**
     * 无参的构造函数
     */
    public TestConstructor() {
        super();
    }

    /**
     * Java构造方法
     * 带参数的构造方法
     * @param name
     * @param age
     * @param sex
     */
    public TestConstructor(String name, Integer age, char sex) {
        this.name = name;
        this.age = age;
        this.sex = sex;
    }
}
```

#### Java 中的构造函数和 kotlin 中的构造函数的区别

- Java构造函数就是一个方法，函数名称和Java类名称相同
- 在 Java 中创建一个类时不能直接带参数，而Kotlin可以带参数，表示是一个 kotlin 语言类的构造函数

主构造函数不能包含任何的代码。初始化的代码可以放到以 ini 关键字作为前缀的初始化块（initializer blocks）中。在实例初始化期间，初始化块按照它们出现在类体中的顺序执行，与属性初始化器交织在一起：

**注：**

- **Java 中代码的执行顺序：静态块>main()>构造块>构造方法**

#### 次构造函数

类可以声明前缀有 constructor  的次构造函数

```kotlin
class Person {
    var children: MutableList<Person> = mutableListOf()
    constructor(parent: Person) {
        parent.children.add(this)
    }
}
```

Kotlin 中的代码执行顺序：

初始化块中的代码实际上会成为构造函数的一部分。因此所有初始化块与属性初始化块中的代码都会在此构造函数之前执行。即使该类没有主构造函数，这种委托仍会隐式发生，并且仍会执行初始代码块

```kotlin
class Constructor {
    init {
        println("Init block")
    }
    
    constructor(i: Int) {
        println("Constructor")
    }
}
```

#### 构造函数的生成

如果一个非抽象类没有声明任何（主或次）构造函数，它会有一个生成的不带参数的主构造函数（这点与Java相同，没有构造函数jvm会自动创建一个无参的构造函数）。构造函数的看见性是 public 。如果不希望类有一个公有构造函数，就需要声明一个带有非默认可见性的空的主构造函数：

```kotlin
class DontCreateMe private constructor (){}
```

**注意：**在 JVM 上，如果主构造函数的所有的参数都有默认值，编译器会生成 一个额外的无参构造函数，它将使用默认值。这使得 Kotlin 更易于使用像 Jackson 或者 JPA 这样的通过无参构造函数创建类的实例的库。与 Java比较，Java中如果有带参的构造函数，jvm 不会再自动创建一个无参的构造函数

```kotlin
// 带有默认值的构造参数，系统会自动创建一个午餐构造函数
class Customer(val customerName: String = "")
```

#### 类成员

- 构造函数与初始化块
- 函数
- 属性
- 嵌套类与内部类
- 对象声明

### 继承

再 Kotlin 中所有的类都有一个共同的超类 Any ，对于没有超类型声明的类是默认超类，有三个方法 equals()、hashCode() 、toString()，因此所有的类都定义了这三个方法

```
class Example // 从 Any 隐式继承
```

**比较 ：在 Java 中所有的类都有一个超类是 Object ，也有三个方法 equals()、hashCode()、toString()**	

**在 Kotlin 中默认情况下类是最终的（final），不能被继承，要是想要类被继承，需要使用 open 关键字标记它。**	

```kotlin
// kotlin 类是不能被继承的，如果需要被继承需要使用open 关键字标记
open class Base // 该类开放继承
```

如需声明一个显示的超类，在类头中把超类型放到冒号之后：

```kotlin
open class Base(p: Int)
class Derived(p: Int) : Base(p)
```

**注意：**

​	设计一个基类时，避免在构造函数、属性值初始化器以及 init 块中使用 open 成员

**封装**

隐藏内部类实现的细节，kotlin 中实现封装是使用关键字 private ，只要当前类才可以调用

## 属性与字段

使用 val 和 var 声明属性，val 是只读的没有setter，var 是可读可写的，有getter 和 setter

**定义getter  和 setter**

```kotlin
var stringRepresentation: String
	get() = this.toString()
	set(value) {
        setDataFormString(value)	// 解析字符串并复制给其他属性
    }
```

**从Kotlin1.1 起，如果可以从getter推断出属性类型，则可以省略它**

```kotlin
val isEmpty get() = this.size == 0 // 具有类型 Boolean
```

**在接口中没有方法体时默认为抽象**

**解决覆盖冲突**

实现多个接口时可能会遇到同一个方法继承多个实现的问题

```kotlin
interface A {
    fun foo() { print("A")}
    fun bar()
}

interface B {
    fun foo() { print("B") }
    fun bar() { print("B bar") }
}

class C : A {
    override fun bar() {print("A bar")}
}

class D : A, B {
    override fun foo() {
		// 实现接口 A 和 B 都有 foo() 方法，使用 supper指定接口类来解决冲突
       	super<A>.foo()	
        super<B>.foo()	
    }
}
```

## 可见性修饰符

Kotlin 中可见性修饰符：private、protected、**Internal**、public，如果没有显示指定，默认可见性是public，如果一个类定义有一个成员函数与一个扩展函数，而这两个函数又有相同的接收者类型、 相同的名字，并且都适用给定的参数，这种情况总是取成员函数

```kotlin
fun main() {
    class Example {
        fun printFunctionType() { println("Class method") }
    }
    fun Example.printFunctionType() { println("Extension function") }
    Example().printFunctionType()
}
```

java 中的可见性修饰符；Kotlin 中的 Inernal 修饰符类似于Java中的 default 属性。

| 类成员修饰符 | 同一个类中可访问 | 同一个包中可以访问 | 在子类中访问 | 在不同包中访问 |
| ------------ | ---------------- | ------------------ | ------------ | -------------- |
| public       | **√**            | **√**              | **√**        | **√**          |
| protected    | **√**            | **√**              | **√**        | **·**          |
| (default)    | **√**            | **√**              | **·**        | **·**          |
| private      | **√**            | **·**              | **·**        | **·**          |

## 扩展是静态解析的

扩展不能真正的修改他们所扩展的类，而是通过定义一个扩展，并没有在一个类中插入新成员，仅仅是可以通过该类型的变量用 .表达式 去调用这个新函数。他们不是根据接收者类型的虚方法。这意味着调用的扩展是由函数调用所在的表达式的类型来决定，而不是由表达式运行时求值结果决定

```kotlin
fun main{
    open class Shape
    class Rectangle: Shape()
    fun Shape.getName() = "shape"
    fun Rectangle.getName = "Rectangle"
    fun printClassName(S: Shape) {
        println(s.getName)
    }
    printClassName(Rectangle())		// 运行结果是 shape
}
```

## 数据类

就是创建一些只保存数据的类，类似于 Java 中 MVC 中的 pojo 类，通过将数据库中的数据封装成一个 JavaBean 对象，但是在Kotlin 中，这叫做 **数据类** 并使用 data 标记

```kotlin
data class User(val name: String, val age: Int)
```

数据类必须满足以下要求

- 主函数至少需要一个参数
- 主构造函数的所有参数需要标记为val 或 var
- 数据类不能抽象、开放、密封或者内部的
- 数据类只能实现接口

## 密封类

作用：为一个有限的数据类型的类添加多个状态，因为密封类的子类可以有可包含状态的多个实例。要声明一个密封类需要使用在一个类的前面添加 **sealed** 修饰符

## 泛型

Java 中的泛型是使用通配符

- 常用的通配符 T、E、K、v、？
- ？ 无界通配符
- 上界通配符  ? super E
- ? 和 T 的区别

**在Java中泛型是不型变的，但是一般来说是可以发生转换的但是在 java 中是不可以的**

在 `Source` 类型的变量中存储 `Source ` 实例的引用是极为安全的——没有消费者-方法可以调用。但是  java 并不知道这一点，并且仍然禁止这样操作：

```kotlin
// Java
void demo(Source<String> strs) {
  Source<Object> objects = strs; // ！！！在 Java 中不允许
  // ……
}
```

为了修正这一点，我们必须声明对象的类型为如下代码所示，这是毫无意义的，因为我们可以像以前一样在该对象上调用所有相同的方法，所以更复杂的类型并没有带来价值。但编译器并不知道。在 Kotlin 中，有一种方法向编译器解释这种情况。这称为**声明处型变**：我们可以标注 `Source` 的**类型参数** `T` 来确保它仅从成员中**返回**（生产），从不被消费。 为此提供 **out** 修饰符：

```kotlin
Source<? extends Object>
```

```kotlin
interface Source<out T> {
    fun nextT(): T
}

fun demo(strs: Source<String>) {
    val objects: Source<Any> = strs // 这个没问题，因为 T 是一个 out-参数
    // ……
}
```

Kotlin 中提供了处型变

- in 表示消费者
- out 表示生产者

## 嵌套类

kotlin 中的嵌套类和Java中的语法规则类似，按照 kotlin 创建类的语法规则正常创建嵌套类

```kotlin
// 嵌套类
class Outer {
    private val bar: int = 1
    class Nested {
        fun foo() = 2
    }
}
val demo = Outer.Nested.foo() // 2
```

接口中的嵌套类

```kotlin
interface OuterInterface {
    class InnerClass
    interface InnerInterface
}

class OuterClass {
    class InnerClass
    interface InnerInterface
}
```

## 内部类

记为 inner 的嵌套类能够访问其外部类的成员。内部类会带有一个对外部类的对象的引用：

```kotlin
class Outer {
    private val bar: Int = 1
    inner class Inner {
        fun foo() = bar
    }
}
val demo = Outer().Inner().foo() // == 1
```

## 枚举类

枚举类的最基本的用法是实现类型安全的枚举：

```kotlin
enum class Direction {
    NORTH, SOUTH, WEST, EAST
}
```

每个枚举常量都是一个对象。枚举常量用逗号分隔。

### 初始化

因为每一个枚举都是枚举类的实例，所以他们可以是这样初始化过的：

```kotlin
enum class Color(val rgb: Int) {
        RED(0xFF0000),
        GREEN(0x00FF00),
        BLUE(0x0000FF)
}
```

## 其他

1. **it**
   指代作用域前面表达式或计算

```kotlin
open class Base(val name: String) {

    init { println("Initializing Base") }

    open val size: Int = 
        name.length.also { println("Initializing size in Base: $it") }
}

class Derived(
    name: String,
    val lastName: String,
) : Base(name.capitalize().also { println("Argument for Base: $it") }) {

    init { println("Initializing Derived") }
	
    // it 指代 also 作用域前面的 (super.size + lastNmae.length)表达式
    override val size: Int =
        (super.size + lastName.length).also { println("Initializing size in Derived: $it") }
}

fun main() {
    println("Constructing Derived(\"hello\", \"world\")")
    val d = Derived("hello", "world")
}
```
