---
title: Kotlin
date: 2020/7/20
description: Kotlin
tag: Kotlin
author: shiyd
---

[Kotlin基本语法使用 - 简书 (jianshu.com)](https://www.jianshu.com/p/37f8cc208d83)

- **kotlin特点**

1. 末尾没有分号
2. 被调用的方法需要放到上边
3. Kotlin时空安全的：在编译时期就处理了各种null的情况，避免执行时异常
4. 它可以扩展函数：我们也可以扩展任意类的更多特性
5. 他也是函数式的：比如，使用lambda表达式来更方便地解决问题
6. 高度互操作性：你可以继续使用所有用Java写的代码和库，甚至可以在一个项目中使用Kotlin和Java两种语言混合编程

- **安装插件及添加依赖**

插件安装：File-->setting->plugin->kotlin

添加依赖：Tools—>Kotlin->Configure kotlin in project 选定模块后自动添加依赖

## 基本类型

基本数据类型和Java相似，类型名称首字母大写

```kotlin
var a: Byte = 2
var b: Short = 2
var c: Int = 2
var d: Long = 2L  	// 长整型由大写字母L标记
var e: Float = 2f 	// 单精度浮点型由f或F标记
var f: Double = 2.0
```

### 数字类型

（Byte、Short、Int、Long）是根据值的大小改变（依次递增）：所有以未超出 `Int` 最大值的整型值初始化的变量都会推断为 `Int` 类型。如果初始值超过了其最大值，那么推断为 `Long` 类型。 如需显式指定 `Long` 型值，请在该值后追加 `L` 后缀

```kotlin
val one = 1 // Int
val threeBillion = 3000000000 // Long
val oneLong = 1L // Long
val oneByte: Byte = 1
```

### 浮点型

对于以小数初始化的变量，编译器会推断为 `Double` 类型。 如需将一个值显式指定为 `Float` 类型，请添加 `f` 或 `F` 后缀。 如果这样的值包含多于 6～7 位十进制数，那么会将其舍入。

```kotlin
val pi = 3.14 // Double
val e = 2.7182818284 // Double
val eFloat = 2.7182818284f // Float，实际值为 2.7182817，只保留7位小数
```

**注意：****Kotlin 中的数字没有隐式拓宽转换**。 例如，具有 `Double` 参数的函数只能对 `Double` 值调用，而不能对 `Float`、 `Int` 或者其他数字值调用。

```kotlin
fun main() {
    fun printDouble(d: Double) { print(d) }
    val i = 1    
    val d = 1.1
    val f = 1.1f 

    printDouble(d)
//    printDouble(i) // 错误：类型不匹配
//    printDouble(f) // 错误：类型不匹配
}
```



**如需将数值转换为不同的类型，请使用显示转换**

### 显示转换

因此较小的类型**不能**隐式转换为较大的类型。 这意味着在不进行显式转换的情况下我们不能把 `Byte` 型值赋给一个 `Int` 变量。

```kotlin
val b:Byte = 1 // 字面值是静态检测的
val i:Int = b	// 错误，较小类型不能转换为较大类型
```

**显示转换：**

```kotlin
val i:Int = b.toInt() // 将Byte类型（b）转换成Int
```

**每个数字类型支持如下的转换:**

- `toByte(): Byte`
- `toShort(): Short`
- `toInt(): Int`
- `toLong(): Long`
- `toFloat(): Float`
- `toDouble(): Double`
- `toChar(): Char`

## 字符串字面值

Kotlin 有两种类型的字符串字面值: 转义字符串可以有转义字符， 以及原始字符串可以包含换行以及任意文本。以下是转义字符串的一个示例:

```kotlin
val s = "Hello, world!\n"
```

*原始字符串* 使用三个引号（`"""`）分界符括起来，内部没有转义并且可以包含换行以及任何其他字符:

```kotlin
val text = """
    for (c in "foo")
        print(c)
"""
```

**使用trimMargin()函数去除前导空格：**

```kotlin
val text = """
    |Tell me and I forget.
    |Teach me and I remember.
    |Involve me and I learn.
    |(Benjamin Franklin)
    """.trimMargin()
```

## 字符串模板

字符串字面值可以包含*模板表达式* ，即一些小段代码，会求值并把结果合并到字符串中。 模板表达式以美元符（`$`）开头

- **由简单的名字构成**

```kotlin
fun main(){
    val i = 10
    println("i = $i")
}
```

- **用花括号括起来的任意表达式**

```kotlin
fun main(){
    val s = "abcd"
    println("s.length is ${s.length}") //输出“abc.length is 3”
}
```

**原始字符串与转义字符串内部都支持模板。 如果你需要在原始字符串中表示字面值** `**$**` **字符（它不支持反斜杠转义，但可以使用** {'**'}），你可以用下列语法：**

```kotlin
val price = """
${'$'}9.99
"""
```

## 字符串比较

- 在 kotlin 中字符串比较使用 === 和 equals，如果 
- == 和 equals 一样比较的是内容
- === 比较的是引用对象

其中 equals 中有两个参数，第一个参数是比较的内容，第二个参数是 Boolean 类型，true 表示比较内容忽略大小写，false 则是不忽略大小写

```kotlin
var str1 = "Any"
var str2 = "any"
str1.equals(str2,true)	// true
str2.equals(str1,false)	// false
```

## 字符串的参数和具名参数

如果一个方法有多个参数，且只想要一个参数时可以使用 " _ "代替其他不需要的参数或者使用具名参数（给需要的参数直接赋值（参数名=赋值））

## mian函数

```kotlin
// kotlin的main函数
fun main(args: Array<String>){}
```

- fun：声明函数的关键字
- main：函数名称
- args：参数名，和Java中的args一样
- ：冒号~在这里就是参数名称和类型之间的间隔

## 数组

```kotlin
var int_array:Array<Int> = arrayOf(1, 2, 3)
var long_array:Array<Long> = arrayOf(1, 2, 3)
var float_array:Array<Float> = arrayOf(1.0f, 2.0f, 3.0f)
var double_array:Array<Double> = arrayOf(1.0, 2.0, 3.0)
var boolean_array:Array<Boolean> = arrayOf(true, false, true)
var char_array:Array<Char> = arrayOf('a', 'b', 'c')
```

## 定义局部变量-var/val

**关键字var和val**

- **var：** 被它修饰的变量可读可写
- **val：** 被他修饰的变量属性可读，但是只能被赋值一次，此后该值不可在改变，相当于Java中的final关键字

**声明变量需要在变量名前面加上上面两个关键字的任意一个来修饰变量**

## NULL检查机制

Kotlin的空安全设计对于声明可为空的参数，在使用时要进行空判断处理，有两种处理方式，字段后加!!像Java一样抛出空异常，另一种字段后加?可不做处理返回值为 null或配合?:做空判断处理

**在 kotlin 中直接在语法阶段避免了空值**

```kotlin
fun heat (str:String): String {
	return "热"+str
}
fun main(){
	var result01 = heat("水")
    println(result01)
    heat(null) 		// 在编译器直接显示错误
    
}

// 解决null
fun heat (str : Stirng?): String {
	return "热" + str
}
```

```kotlin
//类型后面加?表示可为空
var age: String? = "23" 
//抛出空指针异常
val ages = age!!.toInt()
//不做处理返回 null
val ages1 = age?.toInt()
//age为空返回-1，类似于Java中的三元运算符
val ages2 = age?.toInt() ?: -1
```

- **安全调用：**
  kotlin之所以是空安全，是因为有这个空安全调用

```kotlin
var_int?.inc()
```

- ?. 的意思就是：假如这个变量不是null的话，就调用后面的函数，否则不调用

- **!!**

```kotlin
var_int!!.inc()
```

- 这个操作符的结果就是当你的var_int不为null时就正常调用 inc() 函数，否则抛出异常
- **字符串模板($)**

```kotlin
$ 表示一个变量名或者变量值

$varName 表示变量值

${varName.fun()} 表示变量的方法返回值:
var a = 1
// 模板中的简单名称：
val s1 = "a is $a" 

a = 2
// 模板中的任意表达式：
val s2 = "${s1.replace("is", "was")}, but now is $a"
```

## 区间

var nums = 1 until 100 (1 100] 前闭后开

1..100 [1 100] 闭区间

```kotlin
// step 步长，如下列每隔2打印一次
var nums = 1..15
	for(i in nums step 2){
        println(i)
    }
```

## 其他特性

1. 创建一个对象不需要new关键字

```kotlin
class Greeter(val name: String){
    fun greet(){
        println("hello,$name");
    }
}
```

1. 没有以分号";"结尾
2. 定义参数时：参数名称在类型的前面，且使用":"隔开

```kotlin
fun main(val args: Arrays<String>){
	println("hello kotlin")
}
```

1. kotlin的返回值：
2. 

1. 1. 方法的后面使用": 返回值类型"

```kotlin
fun sum(a: Int, b: Int): Int{
    return a+b
}
```

1. 1. 可以根据函数主体推断返回值类型

```kotlin
fun sum(a: Int, b: Int) = a + b
```

符号：$，表示是一个值（类似于占位符）

在Kotlin中 $ 是特殊的字符，如果在字符串中，需要使用反斜杠或 {'$'} 进行转义

1. **交换两个变量**

```kotlin
var a = 1
var b = 2
a = b.also { b = a }
```

1. **with操作符**

```kotlin
// 下面是常见的UI配置逻辑
applicationWindow.title = "Just an example"
applicationWindow.position = FramePosition.AUTO
applicationWindow.content = createXontent()
applicationWindow.show()
```

1. 在这里 **applicationWindow** 被反复使用，此时我们可以使用 **with** 进行优化，使代码更加简洁易读

```kotlin
with(applicationWindow) {	// this： Applicationwindow
    title = "Just an example"
    position = FramePositin.AUTO
    content = createCOntent()
    show()
}
```

## 迭代数字

使用  ***downTo()*** 函数，这里的 **i** 和不需要给初始值，**i** 相当于一个动态的标志，相当于Java中的 ***i--***

```kotlin
for (i in 4 downTo 1) print(i) // 输出4 3 2 1，i 开始时等于4 ，downTo 1 表示每循环一次该数字将减一
```

使用  ***step()*** 函数，可以指定任意步长，相当于Java中的 **i++**

```kotlin
for (i in 1..4 step 2) print(i) // 输出 1 3，表示i从1开始到4结束
```

## 控制流

#### When表达式

When表达式取代了类C语言的switch语句。其简单的形式如下：

```kotlin
when (x) {
    1 -> print("x == 1")
    2 -> print("x == 2")
    else -> {
        // 注意这个快
        print("x is neither 1 nor 2")
    }
}
```

如果很多分支需要用到相同的方式处理，则可以把多个分支放到一起，用逗号隔开：

```kotlin
when (x) {
    0, 1 -> print("x == 0 or x == 1")
    else -> print("otherwise")
}
```

我们可用任意表达式（而不只是常量）作为分支条件

```kotlin
when (x) {
    parseInt(s) -> print("s encode x") // 报错：Unresolved reference: parseInt
    else -> print("s does not encode x")
}
```

我们也可以检测一个值在（in）或者不在（!in）一个区间或者集合中

```kotlin
when (x) {
    in 1..10 -> print("x is in range")
    in validNumbers -> print("x is valid")
    !in 10..20 -> print("x is outside the range")
    else -> print("none of the above")
}
```

**在** ***when*** **主语中引入的变量的作用域仅限于** ***when*** **主体。**

#### For循环

***for*** 循环可以对任何提供迭代器（iterator）的对象进行遍历，这相当于像C#这样的语言中的 foreach 循环

```kotlin
for (item in collection) print(item)
```

循环体可以是一个代码块

```kotlin
for (item: Int in item){}
```

如需在数字区间上迭代，使用区间表达式

```kotlin
for (i in 1..3) {
    println(i)
}
for (i in 6 downTo 0 step 2) {
    println(i)
}
```

**对区间或者数组的** ***for*** **循环会被编译为并不创建迭代器的基于索引的循环**

如果想通过索引遍历一个数组或者一个list

```kotlin
for (i in array.indices){
    println(array[i])
}
```

或者可以用库函数 *withIndex*

```kotlin
for ((index, value) in array.withIndex) {
    println("the element at $index is $value")
}
```

## 返回和跳转

- **return：**返回
- **break：**中断
- **continue：**继续

### beak

用来退出单层循环可退出多层循环

### continue

退出当前循环（退出一次循环），循环体中continue后面的语句不执行且如果循环没有结束，继续执行该循环，直到循环结束

### return

跳出一个方法，跳转到上层调用的方法，在使用**标签时**按照标签的位置结束

### Break与Continue标签

在Kotlin中任意表达式都可以用标签（label）来标记。标签的格式为标识符后跟 @ 符号，列如：abc@\ fooBar@ 都是有效的标签（参见语法）。要为一个表达式加标签，我们只要在其前加标签即可

```kotlin
loop@ for (i in 1..100) {}
```

**使用标签限制break或者continue，标签限制break跳转到刚好位于该标签指定的循环后面的执行点**

```kotlin
loop@ for (i in 1..100) {
    for (j in 1..100){
        if(i == j) break@loop
    }
}
```

**使用隐式标签更方便，该标签与接受该lambda的函数同名(forEach---**[**@forEach)** ]() 

```kotlin
fun foo () {
    listOf(1, 2, 3, 4 5).forEach {
        if (it == 3) return@forEach		// 局部返回到该lambda表达式的调用者，即 forEach 循环
        print(it)
    }
    print(" done with implicit label")
}
```
