# 异常Exception

## 一、异常基本介绍

### 1.异常的概念

java语言中，将程序执行中发生的不正常情况称为“异常”。（开发过程中的语法错误和逻辑错误不是异常）

### 2.执行过程中的异常事件

可分为两大类

1. Error(错误)：Java虚拟机无法解决的严重问题。比如JVM系统内部错误、资源耗尽等严重的错误 StackOverflowError、OutOfMemory，Error是严重错误，程序会崩溃
2. Exception：其他因编程错误或者偶然的外部因素导致的一般性问题，可以使用针对性的代码进行处理，例如空指针异常，试图读取不存在的文件，网络连接终端等，Exception分为两大类：运行时异常（程序运行时，发送的异常）和编译时异常（编译时，编译器检查出的异常）

## 二、异常体系图



![image-20220120213102118](https://s2.loli.net/2022/05/09/F2B7gqflXnCToJv.png)

1. 异常分为两大类，运行时异常和编译时异常
2. 运行时异常，编译器检查不出来，一般是指编程时的逻辑错误，是程序员应该避免其出现的异常，java.lang.RuntimeException类及它的子类都是运行时异常
3. 对于运行时异常，可以不作处理，因为这类异常很普遍，若全处理可能会对程序的可读性和运行效率产生影响
4. 编译时异常，是编译器要求必须处理的异常

## 三、常见的异常

### 1.常见的运行时异常

1. NullPointerException 空指针异常 
2. ArithmeticException 数学运算异常
3.  ArrayIndexOutOfBoundsException 数组下标越界异常 
4. ClassCastException 类型转换异常 ，当试图将对象强制转换为不是实例的子类时，抛出该异常。
5. NumberFormatException 数字格式不正确异常，当应用程序试图将字符串转换成一种数值类型，但该字符串不能转换为适当格式时，抛出该异常

### 2.常见的编译异常

1. SQLException 操作数据库时，查询表可能发生议程
2. IOException 操作文件时，发生的异常
3. FileNotFoundException 当操作一个不存在的文件时，发生异常
4. ClassNotFoundException 加载类，而该类不存在时，发生异常
5. EOFException 操作文件，到文件末尾，发生异常
6. ILLegalArguementException 参数异常



## 四、异常处理

### 1、基本概念

异常处理就是当异常发生时，对异常处理的方式

### 2、异常处理的方式

1. try-catch-finally 程序员在代码中捕获发生的异常，自行处理
2. throws 将发送的异常抛出，交给调用者（方法）来处理，最顶级的处理者就是JVM

### 3、异常的第一种处理方式，捕获异常try......catch

```java
try {
    可能产生异常的代码
    将异常封装成对应的异常对象，传递给catch块
}catch(定义一个异常的变量，用来接收try中抛出的异常对象) {
    异常的处理逻辑，接收异常对象之后怎么处理异常，一般在工作中
    会把异常记录到一个日志中
}
...// 多个catch
catch(异常类名 变量名) {
    try可能抛出多个异常，可以使用多个catch
}finally {
            System.out.println("这里的代码无论是否出现异常都会执行，一般用于资源回收");
            //  finally代码块不能单独使用，和try catch一起使用
            // 如果finally代码块里有return语句，那么永远返回finally中的结果，应该避免在finally中写return语句
}
```

**注意**

1. try可能回抛出多个异常对象，可以使用多个catch处理这些异常，捕获不同的异常（进行不同的业务处理），要求父类异常在后，子类异常在前，比如Exception在后，NullPointerException在前），如果发射异常，只会匹配一个catch
2. try产生了异常就执行相对应的异常处理逻辑，之后继续执行后续代码（catch之后的）
3. 没有产生异常就不执行catch，执行完try后，执行后续代码
4. 可以直接使用try-finally，这种方式相当于没有捕获异常，因此程序会直接崩溃、退出。应用场景，就是执行一段代码，不管是否发生异常，都必须执行某个业务逻辑



### 4、异常的第二种处理方式，使用throws关键字

1. 如果一个方法（或语句）可能生成某种异常，但是不确定如何处理这种异常，则此方法应显式的声明抛出异常，表明该方法将不对这些异常进行处理，而由该方法的调用者负责处理，最终交个JVM处理（中断处理）
2. JVM中断处理，后面的后续代码就不会执行了。
3. 用throws语句可以声明抛出异常的列表，throws后面的异常类型可以是方法中产生的异常类型，也可以是它的父类
4. 对于编译异常，程序中必须处理，抛给方法的调用者，调用者也必须处理
5. 对于运行时异常，程序中如果没有处理，默认就是throws的方式处理
6. 子类重写父类的方法时，对抛出异常的规定，所抛出的异常类型要么和父类抛出的异常一致，要么为父类抛出的异常的类型的子类型





throws使用格式：
当一个方法抛出了异常，就在方法声明时使用throws关键字，将异常交给方法调用者处理

```java
修饰符 返回值类型 方法名（参数列表） throws AAAException， BBBException {
    //method body
}
```

### 5、自定义异常

**概念**

当程序中出现了某些“错误”，但该错误信息并没有在Throwable子类中描述处理，这个时候可以自己设计异常类，用于描述该错误信息 

 **自定义异常的步骤**

1. 定义类:自定义异常类名(程序员自己写)继承Exception或RuntimeException
2. 如果继承Exception，属于编译异常
3. 如果继承RuntimeException，属于运行异常(一般来说，继承RuntimeException)

```java
package CustomException;

/**
 * @program: study
 * @description: 自定义异常类
 * @author: xiongfeng
 * @create: 2022-01-21 11:27
 **/
public class CustomException {
    public static void main(String[] args) {
        int age =180;
        if(!(age>=18 &&age<=120)){
            throw  new AgeException("年龄需要在18~120之间");
        }
        System.out.println("年龄正确");
    }
}
//自定义异常
// 1.一般情况下，我们自定义异常继承RuntimeException
// 2.即把自定义异常做成 运行时异常，好处是，我们可以使用默认的处理机制
//这里如果继承Exception，包括了编译异常，由于编译异常必须处理，所有main方法必须throws
class AgeException extends RuntimeException{
    public AgeException(String message) {
        super(message);
    }
}
```

### 6.throw 和 throws 的区别

|        | 意义                     | 位置       | 后面跟的东西 |
| ------ | ------------------------ | ---------- | ------------ |
| throws | 异常处理的一种方式       | 方法声明处 | 异常类型     |
| throw  | 手动生成异常对象的关键字 | 方法体中   | 异常对象     |



