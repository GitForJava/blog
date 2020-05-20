[TOC]
> 原文：https://shimo.im/docs/hRQv86cQpxWTPV9P/ 《第四章 面向对象(上)》
# 第四章 面向对象(上)
## 4.6 面向对象特征之一：封装与隐藏
> 封装性的引入与体现
为什么需要封装？封装的作用和含义？
我要用洗衣机，只需要按一下开关和洗涤模式就可以了。有必要了解洗衣机内部的结构吗？有必要碰电动机吗？
我要开车，...

> 我们程序设计追求“高内聚，低耦合”。
高内聚：类的内部数据操作细节自己完成，不允许外部干涉；
低耦合：仅对外暴露少量的方法用于使用。

> 隐藏对象内部的复杂性，只对外公开简单的接口。便于外界调用，从而提高系统的可扩展性、可维护性。通俗的说，`把该隐藏的隐藏起来，该暴露的暴露出来。这就是封装性的设计思想`。

```java
/*
 * 面向对象的特征一:封装与隐藏
 * 一、问题的引入：
 *    当我们创建一个类的对象以后，我们可以通过"对象.属性"的方式，对对象的属性进行赋值。这里，赋值操作要受到
 *    属性的数据类型和存储范围的制约。但除此之外，没有其他制约条件。但是，实际问题中，我们往往需要给属性赋值
 *    加入额外限制条件。这个条件就不能在属性声明时体现，我们只能通过方法进行条件的添加。比如说，setLegs
 *    同时，我们需要避免用户再使用“对象.属性”的方式对属性进行赋值。则需要将属性声明为私有的(private)
 *    --》此时，针对于属性就体现了封装性。
 *    
 * 二、封装性的体现：
 *    我们将类的属性私有化(private),同时,提供公共的(public)方法来获取(getXxx)和设置(setXxx)
 *    
 *    拓展：封装性的体现：① 如上 ② 单例模式 ③ 不对外暴露的私有方法
 *
 */
public class AnimalTest {

	public static void main(String[] args) {
		Animal a = new Animal();
		a.name = "大黄";
//		a.age = 1;
//		a.legs = 4;//The field Animal.legs is not visible
		
		a.show();
		
//		a.legs = -4;
//		a.setLegs(6);
		a.setLegs(-6);
		
//		a.legs = -4;//The field Animal.legs is not visible
		a.show();
		
		System.out.println(a.name);
		System.out.println(a.getLegs());
	}
}
class Animal{
	
	String name;
	private int age;
	private int legs; //腿的个数
	
	//对于属性的设置
	public void setLegs(int l){
		if(l >= 0 && l % 2 == 0){
			legs = l;
		}else{
			legs = 0;
		}
	}
	
	//对于属性的获取
	public int getLegs(){
		return legs;
	}
	
	public void eat(){
		System.out.println("动物进食");
	}
	
	public void show(){
		System.out.println("name = " + name + ",age = " + age + ",legs = " + legs);
	}
	
	//提供关于属性 age 的 get 和 set 方法
	public int getAge(){
		return age;
	}
	
	public void setAge(int a){
		age = a;
	}
}
```
### 四种权限修饰符的理解与测试
> Java 权限修饰符 public、protected、(缺省)、private 置于类的成员定义前，用来限定对象对该类成员的访问权限。

![图片: https://uploader.shimo.im/f/BnOxeu6anBqhLyCW.png](https://img-blog.csdnimg.cn/20200421122703178.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzQ2MTUzOTQ5,size_16,color_FFFFFF,t_70#pic_center)

> 对于 class 的权限修饰只可以用 public 和 default(缺省)。
》public 类可以在任意地方被访问。
》default 类只可以被同一个包内部的类访问。

**Order 类**

```java
/*
 * 三、封装性的体现，需要权限修饰符来配合。
 *   1.Java 规定的 4 种权限：(从小到大排序)private、缺省、protected、public
 *   2.4 种权限用来修饰类及类的内部结构：属性、方法、构造器、内部类
 *   3.具体的，4 种权限都可以用来修饰类的内部结构：属性、方法、构造器、内部类
 * 		 修饰类的话，只能使用：缺省、public
 *  总结封装性：Java 提供了 4 中权限修饰符来修饰类积累的内部结构，体现类及类的内部结构的可见性的方法。
 * 
 */
public class Order {

	private int orderPrivate;
	int orderDefault;
	public int orderPublic;
	
	private void methodPrivate(){
		orderPrivate = 1;
		orderDefault = 2;
		orderPublic = 3;
	}
	
	void methodDefault(){
		orderPrivate = 1;
		orderDefault = 2;
		orderPublic = 3;
	}
	
	public void methodPublic(){
		orderPrivate = 1;
		orderDefault = 2;
		orderPublic = 3;
	}
}
```
**OrderTest 类**

```java
public class OrderTest {

	public static void main(String[] args) {
		
		Order order = new Order();
		
		order.orderDefault = 1;
		order.orderPublic = 2;
		//出了 Order 类之后，私有的结构就不可调用了
//		order.orderPrivate = 3;//The field Order.orderPrivate is not visible
		
		order.methodDefault();
		order.methodPublic();
		//出了 Order 类之后，私有的结构就不可调用了
//		order.methodPrivate();//The method methodPrivate() from the type Order is not visible
	}
}
```
**相同项目不同包的 OrderTest 类**

```java
import github.Order;

public class OrderTest {

	public static void main(String[] args) {
		Order order = new Order();
		
		order.orderPublic = 2;
		//出了 Order 类之后，私有的结构、缺省的声明结构就不可调用了
//		order.orderDefault = 1;
//		order.orderPrivate = 3;//The field Order.orderPrivate is not visible
		
		order.methodPublic();
		//出了 Order 类之后，私有的结构、缺省的声明结构就不可调用了
//		order.methodDefault();
//		order.methodPrivate();//The method methodPrivate() from the type Order is not visible
	}
}
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200421124007546.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzQ2MTUzOTQ5,size_16,color_FFFFFF,t_70#pic_center)
### 封装性的练习
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200421124043193.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzQ2MTUzOTQ5,size_16,color_FFFFFF,t_70#pic_center)
```java
/*
 * 1.创建程序,在其中定义两个类：Person 和 PersonTest 类。
 * 定义如下：用 setAge()设置人的合法年龄(0~130)，用 getAge()返回人的年龄。
 * 
 */
public class Person {

	private int age;
	
	public void setAge(int a){
		if(a < 0 || a > 130){
//			throw new RuntimeException("传入的数据据非法");
			System.out.println("传入的数据据非法");
			return;
		}
		
		age = a;
		
	}
	
	public int getAge(){
		return age;
	}
	
	//绝对不能这样写！！！
	public int doAge(int a){
		age = a;
		return age;
	}
}
```
**测试类**
```java
/*
 *  在 PersonTest 类中实例化 Person 类的对象 b，
 *  调用 setAge()和 getAge()方法，体会 Java 的封装性。
 */
public class PersonTest {

	public static void main(String[] args) {
		Person p1 = new Person();
//		p1.age = 1;	//编译不通过
		
		p1.setAge(12);
		
		System.out.println("年龄为:" + p1.getAge());
	}
}
```
## 4.7 构造器(构造方法)
### 构造器的理解
```java
/*
 * 类的结构之三:构造器(构造方法、constructor)的使用
 * constructor:
 * 
 * 一、构造器的作用:
 * 1.创建对象
 * 2.初始化对象的属性
 * 
 * 二、说明
 * 1.如果没有显示的定义类的构造器的话，则系统默认提供一个空参的构造器。
 * 2.定义构造器的格式:
 * 			权限修饰符  类名(形参列表) { }
 * 3.一个类中定义的多个构造器，彼此构成重载。
 * 4.一旦显示的定义了类的构造器之后，系统不再提供默认的空参构造器。
 * 5.一个类中，至少会有一个构造器		
 */
public class PersonTest {

	public static void main(String[] args) {
		//创建类的对象:new + 构造器
		Person p = new Person();	//Person()这就是构造器
		
		p.eat();
		
		Person p1 = new Person("Tom");
		System.out.println(p1.name);
	}
}
class Person{
	//属性
	String name;
	int age;
	
	//构造器
	public Person(){
		System.out.println("Person()......");
	}
	
	public Person(String n){
		name = n;
	}
	
	public Person(String n,int a){
		name = n;
		age = a;
	}
	
	//方法
	public void eat(){
		System.out.println("人吃饭");
	}
	
	public void study(){
		System.out.println("人学习");
	}
}
```
**练习 1**

```java
/* 2.在前面定义的 Person 类中添加构造器，
 * 利用构造器设置所有人的 age 属性初始值都为 18。
 * 
 */
public class Person {

	private int age;
	
	public Person(){
		age = 18;
	}
}

public class PersonTest {

	public static void main(String[] args) {
		Person p1 = new Person();

		System.out.println("年龄为:" + p1.getAge());
	}
}
```
**练习 2**

```java
/* 3.修改上题中类和构造器，增加 name 属性,
 *   使得每次创建 Person 对象的同时初始化对象的 age 属性值和 name 属性值。
 */
public class Person {

	private int age;
	private String name;
	
	public Person(){
		age = 18;
	}
	
	public Person(String n,int a){
		name = n;
		age = a;
	}
	
	public void setName(String n){
		name = n;
	}
	
	public String getName(){
		return name;
	}
	
	public void setAge(int a){
		if(a < 0 || a > 130){
//			throw new RuntimeException("传入的数据据非法");
			System.out.println("传入的数据据非法");
			return;
		}
		
		age = a;
		
	}
	
	public int getAge(){
		return age;
	}
}

public class PersonTest {

	public static void main(String[] args) {
		
		Person p2 = new Person("Tom",21);
		
		System.out.println("name = " + p2.getName() + ",age = " + p2.getAge());
	}
}
```
**练习 3**

```java
/*
 * 编写两个类，TriAngle 和 TriAngleTest，
 * 其中 TriAngle 类中声明私有的底边长 base 和高 height，同时声明公共方法访问私有变量。
 * 此外，提供类必要的构造器。另一个类中使用这些公共方法，计算三角形的面积。
 * 
 */
public class TriAngle {

	private double base;//底边长
	private double height;//高
	
	public TriAngle(){
		
	}
	
	public TriAngle(double b,double h){
		base = b;
		height = h;
	}
	
	public void setBase(double b){
		base = b;
	}
	
	public double getBase(){
		return base;
	}
	
	public void setHeight(double h){
		height = h;
	}
	
	public double getHeight(){
		return height;
	}
}

public class TriAngleTest {

	public static void main(String[] args) {
		
		TriAngle t1 = new TriAngle();
		t1.setBase(2.0);
		t1.setHeight(2.5);
//		t1.base = 2.5;//The field TriAngle.base is not visible
//		t1.height = 4.3;		
		System.out.println("base : " + t1.getBase() + ",height : " + t1.getHeight());
		
		TriAngle t2 = new TriAngle(5.1,5.6);
		System.out.println("面积 : " + t2.getBase() * t2.getHeight() / 2);

	}
}
```
### 总结属性赋值的过程

```java
/*
 * 总结:属性赋值的先后顺序
 * 
 * ① 默认初始化值
 * ② 显式初始化
 * ③ 构造器中赋值
 * ④ 通过"对象.方法" 或 “对象.属性”的方式，赋值
 * 
 * 以上操作的先后顺序:① - ② - ③ - ④
 * 
 */
public class UserTest {

	public static void main(String[] args) {
		User u = new User();
		
		System.out.println(u.age);
		
		User u1 = new User(2);
		
		u1.setAge(3);
		
		System.out.println(u1.age);
	}
}
class User{
	String name;
	int age = 1;
	
	public User(){
		
	}
	
	public User(int a){
		age = a;
	}
	
	public void setAge(int a){
		age = a;
	}
}
```
### JavaBean 的使用

```java
/*
 * JavaBean 是一种 Java 语言写成的可重用组件。
 * 所谓 javaBean，是指符合如下标准的 Java 类：
 * 		> 类是公共的
 * 		> 有一个无参的公共的构造器
 * 		> 有属性，且有对应的 get、set 方法
 * 
 */
public class Customer {
	
	private int id;
	private String name;

	public Customer(){
		
	}
	
	public void setId(int i){
		id = i;
	}
	
	public int getId(){
		return id;
	}
	
	public void setName(String n){
		name = n;
	}
	
	public String getName(){
		return name;
	}
}
```
### UML 类图(`了解！！！`)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200421125301730.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzQ2MTUzOTQ5,size_16,color_FFFFFF,t_70)

 > 1.+ 表示 public 类型，-表示 private 类型，#表示 protected 类型
2.方法的写法: 方法的类型(+、-)  方法名(参数名：参数类型)：返回值类型

## 4.8 关键字：this 的使用
### this 调用属性、方法、构造器

```java
/*
 * this 关键字的使用
 * 1.this 用来修饰、调用：属性、方法、构造器
 * 
 * 2.this 修饰属性和方法:
 * 		this 理解为：当前对象,或当前正在创建的对象。
 * 	 
 *  2.1 在类的方法中，我们可以使用"this.属性"或"this.方法"的方式，调用当前对象属性和方法。
 *  	通常情况下，我们都选择省略“this.”。特殊情况下，如果方法的形参和类的属性同名，我们必须显式
 *  	的使用"this.变量"的方式，表明此变量是属性，而非形参。
 * 
 *  2.2 在类的构造器中，我们可以使用"this.属性"或"this.方法"的方式，调用正在创建的对象属性和方法。
 *  	但是，通常情况下，我们都选择省略“this.”。特殊情况下，如果构造器的形参和类的属性同名，我们必须显式
 *  	的使用"this.变量"的方式，表明此变量是属性，而非形参。
 *  
 *  3.this 调用构造器
 *  	① 我们可以在类的构造器中，显式的使用"this(形参列表)"的方式，调用本类中重载的其他的构造器！
 *  	② 构造器中不能通过"this(形参列表)"的方式调用自己。
 *  	③ 如果一个类中声明了n个构造器，则最多有n -1个构造器中使用了"this(形参列表)"。
 *  	④ "this(形参列表)"必须声明在类的构造器的首行！
 *  	⑤ 在类的一个构造器中，最多只能声明一个"this(形参列表)"。
 */
public class PersonTest {

	public static void main(String[] args) {
		Person p1 = new Person();
		
		p1.setAge(1);
		System.out.println(p1.getAge());
		
		p1.eat();
		System.out.println();
		
		Person p2 = new Person("jerry" ,20);
		System.out.println(p2.getAge());
	}
}
class Person{
	
	private String name;
	private int age;
	
	public Person(){
		this.eat();
		String info = "Person 初始化时，需要考虑如下的 1,2,3,4...(共 40 行代码)";
		System.out.println(info);
	}
	
	public Person(String name){
		this();
		this.name = name;
	}
	
	public Person(int age){
		this();
		this.age = age;
	}
	
	public Person(String name,int age){
		this(age);	//调用构造器的一种方式
		this.name = name;
//		this.age = age;
	}
	
	public void setNmea(String name){
		this.name = name;
	}
	
	public String getName(){
		return this.name;
	}
	
	public void setAge(int age){
		this.age = age;
	}
	
	public int getAge(){
		return this.age;
	}
	
	public void eat(){
		System.out.println("人吃饭");
		this.study();
	}
	
	public void study(){
		System.out.println("学习");
	}
}
```
### this 的练习
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200421125402269.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzQ2MTUzOTQ5,size_16,color_FFFFFF,t_70)

**Boy 类**
```java
public class Boy {

	private String name;
	private int age;
	
	public void setName(String name){
		this.name = name;
	}
	
	public String getName(){
		return name;
	}
	
	public void setAge(int ahe){
		this.age = age;
	}
	
	public int getAge(){
		return age;
	}
	
	public Boy(String name, int age) {
		this.name = name;
		this.age = age;
	}


	public void marry(Girl girl){
		System.out.println("我想娶" + girl.getName());
	}
	
	public void shout(){
		if(this.age >= 22){
			System.out.println("可以考虑结婚");
		}else{
			System.out.println("好好学习");
		}
	}
}
```
**Girl 类**

```java
public class Girl {

	private String name;
	private int age;
	
	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}
	
	public Girl(){
		
	}
	public Girl(String name, int age) {
		this.name = name;
		this.age = age;
	}
	
	public void marry(Boy boy){
		System.out.println("我想嫁给" + boy.getName());
	}
	/**
	  * 
	  * @Description 比较两个对象的大小
	  * @author subei
	  * @date 2020 年 4 月 21 日上午 9:17:35
	  * @param girl
	  * @return
	 */
	public int compare(Girl girl){
//		if(this.age >girl.age){
//			return 1;
//		}else if(this.age < girl.age){
//			return -1;
//		}else{
//			return 0;
//		}
		
		return this.age - girl.age;
	}
	
}
```
**测试类**

```java
public class BoyGirlTest {

	public static void main(String[] args) {
		
		Boy boy = new Boy("罗密欧",21);
		boy.shout();
		
		Girl girl = new Girl("朱丽叶", 18);
		girl.marry(boy);
		
		Girl girl1 = new Girl("祝英台", 19);
		int compare = girl.compare(girl1);
		if(compare > 0){
			System.out.println(girl.getName() + "大");
		}else if(compare < 0){
			System.out.println(girl1.getName() + "大");
		}else{
			System.out.println("一样的");
		}
	}
}
```
### [实验1：Account_Customer.pdf](https://www.yuque.com/nizhegechouloudetuboshu/library/rc1889)
**Account 类**

```java
public class Account {

	private int id; // 账号
	private double balance; // 余额
	private double annualInterestRate; // 年利率

	public void setId(int id) {

	}

	public double getBalance() {
		return balance;
	}

	public void setBalance(double balance) {
		this.balance = balance;
	}

	public double getAnnualInterestRate() {
		return annualInterestRate;
	}

	public void setAnnualInterestRate(double annualInterestRate) {
		this.annualInterestRate = annualInterestRate;
	}

	public int getId() {
		return id;
	}

	public void withdraw(double amount) { // 取钱
		if(balance < amount){
			System.out.println("余额不足，取款失败");
			return;
		}
		balance -= amount;
		System.out.println("成功取出" + amount);
	}

	public void deposit(double amount) { // 存钱
		if(amount > 0){
			balance += amount;
			System.out.println("成功存入" + amount);
		}
	}

	public Account(int id, double balance, double annualInterestRate) {
		this.id = id;
		this.balance = balance;
		this.annualInterestRate = annualInterestRate;
	}
	
	
}
```

**Customer 类**
```java
public class Customer {

	private String firstName;
	private String lastName;
	private Account account;

	public Customer(String f, String l) {
		this.firstName = f;
		this.lastName = l;
	}

	public String getFirstName() {
		return firstName;
	}

	public String getLastName() {
		return lastName;
	}

	public Account getAccount() {
		return account;
	}

	public void setAccount(Account account) {
		this.account = account;
	}
	
}
```
**CustomerTest 类**
```java
/*
 * 写一个测试程序。
 * （1）创建一个 Customer，名字叫 Jane Smith, 他有一个账号为 1000，
 * 余额为 2000 元，年利率为 1.23％的账户。
 * （2）对 Jane Smith 操作。存入 100 元，再取出 960 元。再取出 2000 元。
 * 打印出 Jane Smith 的基本信息
 * 
 * 成功存入：100.0
 * 成功取出：960.0
 * 余额不足，取款失败
 * Customer  [Smith,  Jane]  has  a  account:  id  is 1000, 
 *  annualInterestRate  is 1.23％,  balance  is 1140.0
 *  
 */
public class CustomerTest {

	public static void main(String[] args) {
		Customer cust = new Customer("Jane" , "Smith");
		
		Account acct = new Account(1000,2000,0.0123);
		
		cust.setAccount(acct);
		
		cust.getAccount().deposit(100); //存入 100
		cust.getAccount().withdraw(960); //取钱 960
		cust.getAccount().withdraw(2000); //取钱 2000
		
		System.out.println("Customer[" + cust.getLastName() + cust.getFirstName() + "]  has  a  account:  id  is "
				+ cust.getAccount().getId() + ",annualInterestRate  is " + cust.getAccount().getAnnualInterestRate() * 100 + "%,  balance  is "
				+ cust.getAccount().getBalance());
	}
}
```
### [实验2：Account_Cust...Bank.pdf](https://www.yuque.com/nizhegechouloudetuboshu/library/rc1889)
**Account 类**
```java
public class Account {

	private double balance;

	public double getBalance() {
		return balance;
	}

	public Account(double init_balance){
		this.balance = init_balance;
	}
	
	//存钱操作
	public void deposit(double amt){
		if(amt > 0){
			balance += amt;
			System.out.println("存钱成功");
		}
	}
	
	//取钱操作
	public void withdraw(double amt){
		if(balance >= amt){
			balance -= amt;
			System.out.println("取钱成功");
		}else{
			System.out.println("余额不足");
		}
	}
}
```
**Customer 类**
```java
public class Customer {

	private String firstName;
	private String lastName;
	private Account account;
	
	public String getFirstName() {
		return firstName;
	}
	public String getLastName() {
		return lastName;
	}
	public Account getAccount() {
		return account;
	}
	public void setAccount(Account account) {
		this.account = account;
	}
	public Customer(String f, String l) {
		this.firstName = f;
		this.lastName = l;
	}	
}
```
**Bank 类**
```java
public class Bank {

	private int numberOfCustomers;	//记录客户的个数
	private Customer[] customers;	//存放多个客户的数组
	
	public Bank(){
		customers = new Customer[10];
	}
	
	//添加客户
	public void addCustomer(String f,String l){
		Customer cust = new Customer(f,l);
//		customers[numberOfCustomers] = cust;
//		numberOfCustomers++;
		customers[numberOfCustomers++] = cust;
	}

	//获取客户的个数
	public int getNumberOfCustomers() {
		return numberOfCustomers;
	}

	//获取指定位置上的客户
	public Customer getCustomers(int index) {
//		return customers;	//可能报异常
		if(index >= 0 && index < numberOfCustomers){
			return customers[index];
		}
		
		return null;
	}	
	
}
```
**BankTest 类**
```java
public class BankTest {

	public static void main(String[] args) {
		
		Bank bank = new Bank();
		
		bank.addCustomer("Jane", "Smith");	
		
		bank.getCustomers(0).setAccount(new Account(2000));
		
		bank.getCustomers(0).getAccount().withdraw(500);
		
		double balance = bank.getCustomers(0).getAccount().getBalance();
		
		System.out.println("客户: " + bank.getCustomers(0).getFirstName() + "的账户余额为：" + balance);
		
		System.out.println("***************************");
		bank.addCustomer("万里", "杨");
		
		System.out.println("银行客户的个数为: " + bank.getNumberOfCustomers());
		
	}
}
```
## 4.9 关键字：package、import 的使用
### 关键字—package

```java
/*
 * 一、package 关键字的使用
 * 1.为了更好的实现项目中类的管理，提供包的概念
 * 2.使用 package 声明类或接口所属的包，生命在源文件的首行
 * 3.包，属于标识符，遵循标识符的命名规则、规范"见名知意"
 * 4.每“.”一次,就代表一层文件目录。
 * 
 * 补充:同一个包下，不能命名同名接口或同名类
 *     不同包下，可以命名同名的接口、类。
 *
 */
public class PackageImportTest {

}
```
**JDK 中主要的包介绍**

```java
1.java.lang----包含一些 Java 语言的核心类，如 String、Math、Integer、System 和 Thread，提供常用功能
2.java.net----包含执行与网络相关的操作的类和接口。
3.java.io----包含能提供多种输入/输出功能的类。
4.java.util----包含一些实用工具类，如定义系统特性、接口的集合框架类、使用与日期日历相关的函数。
5.java.text----包含了一些 java 格式化相关的类
6.java.sql----包含了 java 进行 JDBC 数据库编程的相关类/接口
7.java.awt----包含了构成抽象窗口工具集（abstractwindowtoolkits）的多个类，这些类被用来构建和管理应用程序的图形用户界面(GUI)。B/S  C/S
```
### MVC 设计模式
> MVC 是常用的设计模式之一，将整个程序分为三个层次：视图模型层，控制器层，与数据模型层。这种将程序输入输出、数据处理，以及数据的展示分离开来的设计模式使程序结构变的灵活而且清晰，同时也描述了程序各个对象间的通信方式，降低了程序的耦合性。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200421130119662.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzQ2MTUzOTQ5,size_16,color_FFFFFF,t_70#pic_center)
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020042113013870.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzQ2MTUzOTQ5,size_16,color_FFFFFF,t_70#pic_center)
### 关键字—import

```java
import java.util.*;

import account2.Bank;

/*
 * 二、import关键字的使用
 * import:导入
 * 1.在源文件中显式的使用import结构导入指定包下的类、接口
 * 2.声明在包的声明和类的声明之间
 * 3.如果需要导入多个结构，则并列写出即可
 * 4.可以使用"xxx.*"的方式,表示可以导入xxx包下的所有结构。
 * 5.如果导入的类或接口是java.lang包下的，或者是当前包下的，则可以省略此import语句。
 * 6.如果在代码中使用不同包下的同名的类。那么就需要使用类的全类名的方式指明调用的是哪个类。
 * 7.如果已经导入java.a包下的类。那么如果需要使用a包的子包下的类的话，仍然需要导入。
 * 8.import static组合的使用：调用指定类或接口下的静态的属性或方法.
 * 
 */
public class PackageImportTest {

	public static void main(String[] args) {
		String info = Arrays.toString(new int[]{1,2,3});
		
		Bank bank = new Bank();
		
		ArrayList list = new ArrayList();
		HashMap map = new HashMap();
		
		Scanner s = null;	
		
		System.out.println("hello");
		
		UserTest us = new UserTest();
		
	}
}
```
> 整个Java全栈系列都是笔者自己敲的笔记。写作不易，如果可以，点个赞呗！✌
