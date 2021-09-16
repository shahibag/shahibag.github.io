# Shahibag的Java笔记之面向对象

> 在此整理关于Java的知识点

# 方法

## 重载

如果同一类中编写多个同名但不同形参列表的方法则叫方法的重载。

```java
class MyClass{
    //同名不同参数列表的成员方法，构成重载
    public int myMethod(int num){
        return num;
    }
    
    public void myMethod(){
        System.out.println("overload example")
    }
    
    public double myMethod(double num1, double num2)(){
        return num1 + num2;
    }  
}
```

重载的好处是减轻了起名的麻烦和记名的麻烦。

**构成方法重载的条件：**

- 必须同名
- 参数列表必须不同
- 返回类型没有要求



## 递归



## 可变参数

java中允许将多个同名同功能但参数个数不同的方法封装成一个方法。

``` java
class MyClass{
    //三个方法都完成求和的任务
    public int sum(int n1){
        return n1;
    }
    public int sum(int n1, int n2){
        return n1 + n2;
    }
    public int sum(int n1, int n2, int n3){
        return n1 + n2 + n3;
    } 
    //将三个函数整合成一个方法
    public int sum(int... num){
       int result = 0;
        for(int i = 0; i < num.length; i++){
            result += num[i];
        }
        return result;
    }
}
```

### 可变参数特性及细节

- 可变参数的实参可以是0个或任意多个
- 可变参数实参可以为数组，其可变参数的本质就是数组
- 可变参数可以和普通参数一起放在形参列表，但必须放到最后
- 一个参数列表中只能出现一个可变参数

```java
public class Main{
    public static void main(String[] args){
       MyClass student = new MyClass(); //创建一个MyClass的对象student
       System.out.println(student.totalScore("Shahi", 82, 67)); //可变参数接受两个实参
       System.out.println(student.totalScore("Ted", 77, 81, 73)); //可变参数接受三个实参
    }
}

class MyClass{
    //可变参数和普通参数一起放时，必须放到最后，而且可变参数只能有一个
    public int totalScore(String name, int... score){
       int result = 0;
        for(int i = 0; i < score.length; i++){
            result += num[i];
        }
        return "name: " + name + ", total score: " + result;
    }
}
```







# 构造器

构造器时一个特殊的方法，它的主要作用时完成对象的初始化，而不是创建对象。创建新对象时系统会自动调用构造器。

## 构造器的特性及细节

- 构造器的方法名必须和类名相同
- 构造器没有返回值，而且不能写void
- 参数列表的规则和成员方法一样
- 构造器可以重载，即一个类中可以定义多个构造器
- 如果没有主动定义构造器，系统自动生成默认无参构造器
- 如果自定义构造器，默认构造器就被覆盖，不能再使用默认构造器，除非再显示定义

```java
public class Main{
	//编写main方法
    public static void main(String[] args){
        Person ted = new Person(); //用无参构造器创建新对象
        Person shahi = new Person("shahi", 12); //用有参构造器给对象属性传初始值
    	System.out.println("name: " + name + "age: " + age); //输出shahi和12   
    }
}

class Person{
    //定义属性
    public String name;
    public int age;
    //无参构造器
    public Person(){ 
    }
    //有参构造器
    public Person(String pName, int pAge){
        name = pName;
        age = pAge;
    }    
}
```



# 作用域

在Java中，主要变量是属性（成员变量）和局部变量，局部变量一般指方法中定义的变量。

|          | 全局变量（属性）                             | 局部变量                                               |
| -------- | -------------------------------------------- | ------------------------------------------------------ |
| 作用域   | 整个类体                                     | 定义它的代码块                                         |
| 初始值   | 有初始值                                     | 没有初始值，必须赋值后再使用                           |
| 生命周期 | 伴随着对象的创建而创建，随着对象的销毁而销毁 | 伴随着它的代码块的执行而创建，伴随着代码块的结束而销毁 |
| 使用范围 | 可以被本类使用，或其他类使用                 | 只能在本类对应的方法体中使用                           |
| 修饰符   | 可以加修饰符                                 | 不能加修饰符                                           |

属性和局部变量名可以重名，访问时遵循就近原则，而同一作用域中的两个局部变量不能重名。

```java
class MyClass{
    public String name = "Ted";
    public void myMethod(){
        String name= "Shahi"; //属性和局部变量可以重名
        System.out.println(name); //输出Shahi，遵循就近原则，访问最近一次定义的name变量
    }
}
```



# 访问修饰符

Java提供四种访问修饰符，用于控制方法和属性的访问权限

| 访问级别 | 访问修饰符    | 同类 | 同包 | 子类 | 不同包 |
| -------- | ------------- | ---- | ---- | ---- | ------ |
| 公开     | **public**    | √    | √    | √    | √      |
| 受保护   | **protected** | √    | √    | √    |        |
| 默认     | default       | √    | √    |      |        |
| 私有     | **private**   | √    |      |      |        |

访问修饰符可以修饰类和类中的方法和属性。

类只能用默认或public来修饰。



# 包

包实际上就是创建不同的目录来保存文件。包的三大作用：

- 区分相同名字的类
- 当项目庞大时，提高管理效率
- 控制访问范围

用package关键字声明文件所在的包。

## package特性及细节

- package声明需要放在类的最上方

- 一个类中最多只能由一句package声明

- 包名只能包含数字，字母和下划线，不能用关键字和保留字
- 一般用小写字母 + 小圆点来命名包

``` java
package mypackage;
package com.company.project.module; //项目体系庞大时用多级包来管理代码
```

## 常用包

```java
java.lang.*; //基本包，默认引入，不需要再显示引入
java.util.*; //系统提供的工具包
java.net.*;  //网络包，网络开发
java.awt.*;  //界面开发，GUI
```

## 引入包 - import

用import关键字引入包，由两种方法，一种是只引入目标类，还有一种是引入某包中所有的类。通常只需要引入需要用的类

```java
import java.util.Scanner; //引入java.util包中的Scanner类
import java.util.*; //包名后加星号代表引入该包的所有类
```

import指令需要放在类定义的前面，如果有包的声明，则需要放在package语句后。



# 封装

**封装的实现方法：**

1. 将属性设为private
2. 提供一个公共的set方法用于赋值属性
3. 提供一个公共的get方法获取属性的值

```java
class Person{
    private String name; //属性私有化
    //getter方法需要返回属性值，方法名是get+属性名
    public String getName(){
        return name;
    }
    //setter方法给属性赋值，方法名是set+属性名
    public void setName(String name){
        this.name = name; //this.name是当前对象的属性，name是局部变量
    }
}
```

可以将构造器和set方法结合，在构造器中通过调用setter来给完成初始化：

```java
public class Main{
    public static void main(String[] args){
        Person person = new Person(12);
        System.out.println(person.getName()); //输出12
    }
}

class Person{
	private int age; //定义属性
	//构造器 constructor
    public Person(int age){
        setAge(age); //调用set方法，将传进来的实参赋值给对象的age属性
    }
    //getter
    public int getAge(){
        return age;
    }
    //setter
    public void setAge(int age){
        this.age = age; 
    }
}
```





# 继承

## 重写/覆盖

## this和super关键字

在创建对象时，虚拟机会给每个对象分配一个this。哪个对象调用，this就代表哪个对象

### this关键字的特性及细节

- this关键字可以用来访问本类的属性、方法和构造器
- this用于区分当前类的属性和局部变量
- this可以访问构造器，但只能在一个构造器中访问另一个构造器，而且必须放在第一条语句
- this只能在类定义的方法中使用

```java
public class Main{
	//编写main方法
    public static void main(String[] args){
        Person ted = new Person(); //用无参构造器创建新对象
        Person shahi = new Person("shahi", 12); //用有参构造器给对象属性传初始值
    	System.out.println("name: " + name + "age: " + age); //输出shahi和12   
    }
}
class Person{
    //定义属性
    public String name;
    public int age;
    public String job;
    //无参构造器
    public Person(){ 
        this("shahi", 12); //在构造器中访问另一个构造器（必须放在构造器的第一条语句）
        this.job = "engineer"; //访问类的属性
    }
    //有参构造器
    public Person(String name, int age){
        this.name = name; //this.name是当前对象的属性（这里当前对象是shahi），name是局部变量
        this.age = age; //this.age是当前对象的属性，age是局部变量
    }    
}
```







# 多态



# 代码块



# 内部类



# final关键字



# 抽象类



# 接口

