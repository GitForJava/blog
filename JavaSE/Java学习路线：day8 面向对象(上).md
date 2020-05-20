[TOC]
> 原文：https://shimo.im/docs/hRQv86cQpxWTPV9P/ 《第四章 面向对象(上)》
# 第四章 面向对象(上)
## 4.1 面向过程与面向对象
>何谓“面向对象”的编程思想？
>首先解释一下“思想”。
>先问你个问题：你想做个怎样的人？
>可能你会回答：我想做个好人，孝敬父母，尊重长辈，关爱亲朋......
>你看，这就是思想。这是你做人的思想，或者说，是你做人的原则。做人有做人的原则，编程也有编程的原则。这些编程的原则呢，就是编程思想。
* 面向过程(POP) 与面向对象(OOP)
>面向对象：Object Oriented Programming 
>面向过程：Procedure Oriented Programming
```java
/*
 * 一、学习面向对象内容的三条主线
 * 1.Java 类及类的成员：属性、方法、构造器、代码块、内部类
 * 2.面向对象的三大特征：封装、继承、多态性、(抽象性)
 * 3.其它关键字：this、super、static、final、abstract、interface、package、import 等
 * 
 * 二、人把大象装进冰箱
 * 1.面向过程:强调的是功能行为，以函数为最小单位，考虑怎么做。
 * 
 * ① 打开冰箱
 * ② 把大象装进冰箱
 * ③ 把冰箱门关住 
 * 
 * 2.面向对象:强调具备了功能的对象，以类/对象为最小单位，考虑谁来做。
 * 人{
 * 		打开(冰箱){
 * 			冰箱.开门();
 * 		}操作(大象){
 * 			大象.进入(冰箱);
 * 		}关闭(冰箱){
 * 			 冰箱.关门();     
 * 		}
 * }
 * 
 * 冰箱{
 * 		开门(){
 * 		}  
 * 		关门(){
 * 		}
 * }
 * 
 * 大象{
 * 		进入(冰箱){
 * 		}
 * }
 */
```
面向对象的思想概述
* 程序员从面向过程的执行者转化成了面向对象的指挥者
* 面向对象分析方法分析问题的思路和步骤：
  * 根据问题需要，选择问题所针对的现实世界中的实体。
  * 从实体中寻找解决问题相关的属性和功能，这些属性和功能就形成了概念世界中的类。
  * 把抽象的实体用计算机语言进行描述，形成计算机世界中类的定义。即借助某种程序语言，把类构造成计算机能够识别和处理的数据结构。
  * 将类实例化成计算机世界中的对象。对象是计算机世界中解决问题的最终工具。
## 4.2 类和对象
```
/* 
 * 三、面向对象的两个要素：
 * 类:对一类事物的描述，是抽象的、概念上的定义
 * 对象:是实际存在的该类事物的每个个体，因而也称为实例(instance)。
 * 可以理解为：类= 抽象概念的人；对象= 实实在在的某个人
 * 面向对象程序设计的重点是类的设计；
 * 设计类，其实就是设计类的成员。
 */
```
### Java 类及类的成员
* 现实世界的生物体，大到鲸鱼，小到蚂蚁，都是由最基本的细胞构成的。同理，Java 代码世界是由诸多个不同功能的类构成的。
* 现实生物世界中的细胞又是由什么构成的呢？细胞核、细胞质、... 那么，Java 中用类 class 来描述事物也是如此。常见的类的成员有：
>属性：对应类中的成员变量
>行为：对应类中的成员方法

![图片](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91cGxvYWRlci5zaGltby5pbS9mL2Z6bFlSRUZsOEJ3bE1LNU0ucG5nIXRodW1ibmFpbA?x-oss-process=image/format,png)

### 类与对象的创建及使用
```java
/*
 * 一、设计类、其实就是设计类的成员
 * Field = 属性 = 成员变量 = 域、字段
 * Method = (成员)方法 = 函数 
 * 
 * 创建类 = 类的实例化 = 实例化类
 * 
 * 二.类和对象的使用(面向对象思想落地的实现)
 * 1.创建类，设计类的成员
 * 2.创建类的对象
 * 3.通过“对象.属性”或“对象.方法”调用对象的结构
 * 三、如果创建类一个类的多个对象，则每个对象都独立的拥有一套类的属性。(非 static 的)
 * 	  意味着:如果我们修改一个对象的属性 a，则不影响另外一个对象属性 a 的值。
 */
//测试类
public class PersonTest {
	public static void main(String[] args) {
		//2.创建 Person 类的对象
		//创建对象语法：类名对象名= new 类名();
		Person p1 = new Person();
		//Scanner scan = new Scanner(System.in);
		
		//调用类的结构：属性、方法
		//调用属性:“对象.属性”
		p1.name = "Tom";
		p1.age = 25;
		p1.isMale = true;
		System.out.println(p1.name);
		
		//调用方法:“对象.方法”
		p1.eat();
		p1.sleep();
		p1.talk("chinese");
		//**********************
		Person p2 = new Person();
		System.out.println(p2.name); //null
		System.out.println(p2.isMale);
		//**********************
		//将 p1 变量保存的对象地址值赋给 p3,导致 p1 和 p3 指向了堆空间中的一个对象实体。
		Person p3 = p1;
		System.out.println(p3.name);
		
		p3.age = 10;
		System.out.println(p1.age); //10
	}
}
/*
 * 类的语法格式：
 * 修饰符 class 类名{
 * 		属性声明;
 * 		方法声明;
 * }
 * 说明：修饰符 public：类可以被任意访问类的正文要用{  }括起来
 */
//1.创建类，设计类的成员
class Person{
	
	//属性:对应类中的成员变量
	String name;
	int age;
	boolean isMale;
	
	//方法:对应类中的成员方法
	public void eat(){
		System.out.println("吃饭");
	}
	
	public void sleep(){
		System.out.println("睡觉");
	}
	
	public void talk(String language){
		System.out.println("人可以说话，使用的是：" + language);
	}
}
```
### 对象的创建和使用：内存解析
![图片](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91cGxvYWRlci5zaGltby5pbS9mLzRRdFZMalNuRDFPWkwzcm4ucG5nIXRodW1ibmFpbA?x-oss-process=image/format,png)

* 堆（Heap），此内存区域的唯一目的就是存放对象实例，几乎所有的对象实例都在这里分配内存。这一点在 Java 虚拟机规范中的描述是：所有的对象实例以及数组都要在堆上分配。
* 通常所说的栈（Stack），是指虚拟机栈。虚拟机栈用于存储局部变量等。局部变量表存放了编译期可知长度的各种基本数据类型（boolean、byte、char、short、int、float、long、double）、对象引用（reference 类型，它不等同于对象本身，是对象在堆内存的首地址）。方法执行完，自动释放。
* 方法区（MethodArea），用于存储已被虚拟机加载的类信息、常量、静态变量、即时编译器编译后的代码等数据。

案例 1

```java
Person p1= newPerson();
p1.name = "Tom";
p1.isMale = true;
Person p2 = new Person();
sysout(p2.name);//null
Person p3 = p1;
p3.age = 10;
```
![图片](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91cGxvYWRlci5zaGltby5pbS9mL0F3bHRVNXYwQ05rSE43MHEucG5nIXRodW1ibmFpbA?x-oss-process=image/format,png)

案例 2

```java
Person p1= newPerson();
p1.name = "胡利民";
p1.age = 23;
Person p2 = new Person();
p2.age = 10;
```
![图片](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91cGxvYWRlci5zaGltby5pbS9mL3pKQzNYQzFveUl3MUNWR0oucG5nIXRodW1ibmFpbA?x-oss-process=image/format,png)

## 4.3类的成员之一：属性
```java
/*
 * 类中属性的使用
 * 
 * 属性(成员变量)	vs	局部变量
 * 1.相同点:
 * 		1.1 定义变量的格式:数据类型 变量名 = 变量值
 * 		1.2 先声明，后使用
 * 		1.3 变量都有其对应的作用域
 * 				
 * 2.不同点:
 * 		2.1 在类中声明的位置不同
 * 		属性:直接定义在类的一对{}内
 * 		局部变量:声明在方法内、方法形参、构造器形参、构造器内部的变量
 * 
 * 		2.2 关于权限修饰符的不同
 * 		属性:可以在声明属性时，指明其权限，使用权限修饰符。
 * 			常用的权限修饰符:private、public、缺省、protected
 * 			目前声明属性时，都使用缺省即可。
 * 		局部变量:不可以使用权限修饰符。
 * 
 * 		2.3 默认初始化值的情况:
 * 		属性:类的属性，根据其类型，都有默认初始化值。
 * 			整型(byte、short、int、long):0
 * 			浮点型(float、double):0.0
 * 			字符型(char):0(或‘\u0000’)
 * 			布尔型(boolean):false
 * 
 * 			引用数据类型(类、数组、接口):null
 * 
 * 		局部变量:没有默认初始化值
 * 			意味着:在调用局部变量之前，一定要显式赋值。
 * 			特别地:形参在调用时,赋值即可。例，45 行
 * 
 * 		2.4 在内存中加载的位置，亦各不相同。
 * 		属性:加载到堆空间中(非 static)
 * 		局部变量:加载到栈空间
 */
public class UserTest {
	public static void main(String[] args) {
		User u1 = new User();
		System.out.println(u1.name);
		System.out.println(u1.age);
		System.out.println(u1.isMale);
		
		u1.talk("俄语");
	}
}
class User{
	//属性(或成员变量)
	String name;	//不加 private 即为缺省
	public int age;	//不加 public 即为缺省
	boolean isMale;
	
	public void talk(String language){//language:形参，也是局部变量
		System.out.println("我们使用" + language + "进行交流。");
	}
	
	public void eat(){
		String food = "石头饼";	//石头饼:局部变量
		System.out.println("北方人喜欢吃:" + food);
	}
}
```
练习1
```java
编写教师类和学生类，并通过测试类创建对象进行测试
Student类
属性:
name:String age:int major:String interests:String
方法:say() 返回学生的个人信息
Teacher类
属性:
name:String age:int teachAge:int course:String
方法:say() 输出教师的个人信息
```
EG:
```java
public class School {
	public static void main(String[] args) {
		Student stu = new Student();
        stu.name = "小明";
        stu.age = 16;
		
		Teacher tea = new Teacher();
		tea.name = "王老师";
        tea.age = 27;
        
        tea.say(stu.name,stu.age);
        stu.say(tea.name, tea.age);
	}	
}
class Student{
	String name;
	int age;
	String major;
	String interests;
	
	void say(String name, int age){
		System.out.println("这个学生是："+name+"年龄是："+age);	}
}
class Teacher{
	String name;
	int age;
	String teachAge;
	String course;
	
	void say(String name, int age){
		System.out.println("这个老师是："+name+"年龄是："+age);
	}
}
```
## 4.4 类的成员之二：方法
```java
/*
 * 类中方法的声明和使用
 * 
 * 方法：描述类应该具有的功能。
 * 比如：Math类：sqrt()\random() \...
 *     Scanner类：nextXxx() ...
 *     Arrays类：sort() \ binarySearch() \ toString() \ equals() \ ...
 * 
 * 1.举例：
 * public void eat(){}
 * public void sleep(int hour){}
 * public String getName(){}
 * public String getNation(String nation){}
 * 
 * 2. 方法的声明：权限修饰符  返回值类型  方法名(形参列表){
 * 					方法体
 * 			  }
 *   注意：static、final、abstract 来修饰的方法，后面再讲。
 *   
 * 3. 说明：
 * 		3.1 关于权限修饰符：默认方法的权限修饰符先都使用public
 * 			Java规定的4种权限修饰符：private、public、缺省、protected  -->封装性再细说
 * 
 * 		3.2 返回值类型： 有返回值  vs 没有返回值
 * 			3.2.1  如果方法有返回值，则必须在方法声明时，指定返回值的类型。同时，方法中，需要使用
 *                return关键字来返回指定类型的变量或常量：“return 数据”。
 * 				  如果方法没有返回值，则方法声明时，使用void来表示。通常，没有返回值的方法中，就不需要
 *               使用return.但是，如果使用的话，只能“return;”表示结束此方法的意思。
 * 
 * 			3.2.2 我们定义方法该不该有返回值？
 * 				① 题目要求
 * 				② 凭经验：具体问题具体分析
 * 
 *      3.3 方法名：属于标识符，遵循标识符的规则和规范，“见名知意”
 *      3.4 形参列表:方法名可以声明0个、1个，或多个形参。
 *      	3.4.1 格式:数据类型1 形参1，数据类型2 形参2,...
 *      
 *      	3.4.2 我们定义方法时，该不该定义形参？
 *      		① 题目要求
 *      		② 凭经验，具体问题具体分析
 *      3.5 方法体:方法功能的体现。
 *  4. return关键字的使用：
 *  	1.使用范围:使用在方法体中
 *  	2.作业:① 结束方法
 *  		  ② 针对于有返回值类型的方法，使用"return 数据"方法返回所要的数据。
 *  	3.注意点:return关键字后不可声明执行语句。
 *  5. 方法的使用中，可以调用当前类的属性或方法。
 *  		特殊的:方法A中又调用了方法A:递归方法。
 *  	方法中不能定义其他方法。
 */
public class CustomerTest {
	public static void main(String[] args) {
		
		Customer cust1 = new Customer();
		
		cust1.eat();
		
		//测试形参是否需要设置的问题
//		int[] arr = new int[]{3,4,5,2,5};
//		cust1.sort();
		
		cust1.sleep(8);
		
	}
}
//客户类
class Customer{
	
	//属性
	String name;
	int age;
	boolean isMale;
	
	//方法
	public void eat(){
		System.out.println("客户吃饭");
		return;
		//return后不可以声明表达式
//		System.out.println("hello");
	}
	
	public void sleep(int hour){
		System.out.println("休息了" + hour + "个小时");
		
		eat();
//		sleep(10);
	}
	
	public String getName(){
		
		if(age > 18){
			return name;
			
		}else{
			return "Tom";
		}
	}
	
	public String getNation(String nation){
		String info = "我的国籍是：" + nation;
		return info;
	}
	
	//体会形参是否需要设置的问题
//	public void sort(int[] arr){
//		
//	}
//	public void sort(){
//		int[] arr = new int[]{3,4,5,2,5,63,2,5};
//		//。。。。
//	}
	
	public void info(){
		//错误的
//		public void swim(){
//			
//		}
		
	}
}
```
练习1
* 创建一个Person类，其定义如下：

![图片](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91cGxvYWRlci5zaGltby5pbS9mL3h2eVN2WkQ0Z21VV3VZRGoucG5nIXRodW1ibmFpbA?x-oss-process=image/format,png)

```java
public class Person {
	String name;
	int age;
	/*
	 * sex:1表示为男性
	 * sex:0表示为女性
	 */
	int sex;
	
	public void study(){
		System.out.println("studying");
	}
	
	public void showAge(){
		System.out.println("age:" + age);
	}
	
	public int addAge(int i){
		age += i;
		return age;
	}
}
```
* 测试类
```java
/*
 * 要求:
 * (1)创建Person类的对象，设置该对象的name、age和sex属性，
 * 	调用study方法，输出字符串“studying”，
 * 	调用showAge()方法显示age值，
 * 	调用addAge()方法给对象的age属性值增加2岁。
 * (2)创建第二个对象，执行上述操作，体会同一个类的不同对象之间的关系。
 * 
 */
public class PersonTest {
	public static void main(String[] args) {
		Person p1 = new Person();
		
		p1.name = "Tom";
		p1.age = 18;
		p1.sex = 1;
		
		p1.study();
		
		p1.showAge();
		
		int newAge = p1.addAge(2);
		System.out.println(p1.name + "的年龄为" + newAge);
		
		System.out.println(p1.age);	//20
		
		//*******************************
		Person p2 = new Person();
		p2.showAge();	//0
		p2.addAge(10);
		p2.showAge();	//10
		
		p1.showAge();	//20
	}
}
```
练习2
```java
/*
 * 2.利用面向对象的编程方法，设计类Circle计算圆的面积。
 */
//测试类
public class CircleTest {
	public static void main(String[] args) {
		Circle c1 = new Circle();
		
		c1.radius = 2.1;
		
		//对应方式一:
//		double area = c1.findArea();
//		System.out.println(area);
		
		//对应方式二:
		c1.findArea();
		//错误的调用
		double area = c1.findArea(3.4);
		System.out.println(area);
	}
}
//圆:3.14*r*r
class Circle{
	//属性
	double radius;
	
	//圆的面积方法
	//方法1：
//	public double findArea(){
//		double area = 3.14 * radius * radius;
//		return area;
//	}	
	//方法2：
	public void findArea(){
		double area = Math.PI * radius * radius;
		System.out.println("面积为:" + area);
	}
	//错误情况:
	public double findArea(Double r){
		double area = 3.14 * r * r;
		return area;
	}
}
```
练习3
```java
/*
 * 3.1 编写程序，声明一个method方法，在方法中打印一个10*8的*型矩形，在main方法中调用该方法。
 * 3.2修改上一个程序，在method方法中，除打印一个10*8的*型矩形外，再计算该矩形的面积，
 * 并将其作为方法返回值。在main方法中调用该方法，接收返回的面积值并打印。
 * 
 * 3.3 修改上一个程序，在method方法提供m和n两个参数，方法中打印一个m*n的*型矩形，
 * 并计算该矩形的面积，将其作为方法返回值。在main方法中调用该方法，接收返回的面积值并打印。
 * 
 */
public class ExerTest {
	
	public static void main(String[] args) {
		
		ExerTest esr = new ExerTest();
		//3.1测试
//		esr.method();
		
		//3.2测试
		//方式一：
//		int area = esr.method();
//		System.out.println("面积为:" + area);
		
		//方式二:
//		System.out.println("面积为:" + esr.method());
		
		//3.3测试
		System.out.println("面积为:" + esr.method(6,5));
	}
	//3.1
//	public void method(){
//		for(int i = 0;i < 10;i++){
//			for(int j = 0;j < 8;j++){
//				System.out.print("* ");
//			}
//			System.out.println();
//		}
//	}
	
	//3.2
//	public int method(){
//		for(int i = 0;i < 10;i++){
//			for(int j = 0;j < 8;j++){
//				System.out.print("* ");
//			}
//			System.out.println();
//		}
//		return 10 * 8;
//	}
	
	//3.3
	public int method(int m,int n){
		for(int i = 0;i < m;i++){
			for(int j = 0;j < n;j++){
				System.out.print("* ");
			}
			System.out.println();
		}
		return m * n;
	}
}
```
练习四
```java
/*
 * 4. 对象数组题目：定义类Student，包含三个属性：
 * 学号number(int)，年级state(int)，成绩score(int)。
 * 创建20个学生对象，学号为1到20，年级和成绩都由随机数确定。
 * 问题一：打印出3年级(state值为3）的学生信息。
 * 问题二：使用冒泡排序按学生成绩排序，并遍历所有学生信息
 * 提示：  1) 生成随机数：Math.random()，返回值类型double;  
 * 		2) 四舍五入取整：Math.round(double d)，返回值类型long。
 * 
 */
public class StudentTest {
	public static void main(String[] args) {
		//声明一个Student类型的数组
		Student[] stu = new Student[20];
		
		for(int i = 0;i <stu.length;i++){
			//给数组元素赋值
			stu[i] = new Student();
			//给Student的对象的属性赋值
			stu[i].number = i + 1;
			//年级:[1,6]
			stu[i].state = (int)(Math.random() * (6 - 1 + 1) + 1);
			//成绩:[0,100]
			stu[i].score = (int)(Math.random() * (100 - 0 + 1));
		}
		
		//遍历学生数组
		for(int i = 0;i < stu.length;i++){
//			System.out.println(stu[i].number + "," + stu[i].state 
//				+  "," + stu[i].score);
			
			System.out.println(stu[i].info());
		}
		System.out.println("*********以下是问题1*********");
		
		//问题一：打印出3年级(state值为3）的学生信息。
		for(int i = 0;i < stu.length;i++){
			if(stu[i].state == 3){
				System.out.println(stu[i].info());
			}
		}
		System.out.println("********以下是问题2**********");
		
		//问题二：使用冒泡排序按学生成绩排序，并遍历所有学生信息。
		for(int i = 0;i < stu.length - 1;i++){
			for(int j = 0;j <stu.length - 1 - i;j++){
				if(stu[j].score >stu[j+1].score){
					//如果需要换序，交换的是数组的元素，Student对象！！！
					Student temp = stu[j];
					stu[j] = stu[j+1];
					stu[j+1] = temp;
				}
			}
		}
		
		//遍历学生数组
		for(int i = 0;i < stu.length;i++){
			System.out.println(stu[i].info());
		}
		
	}
}
class Student{
	int number;	//学号
	int state;	//年级
	int score;	//成绩
	
	//显示学生信息的方法
	public String info(){
		return "学号:" + number + ",年级:" + state + ",成绩:" + score;
	}
}
```
练习四优化
```java
/*
 * 4. 对象数组题目：定义类Student，包含三个属性：
 * 学号number(int)，年级state(int)，成绩score(int)。
 * 创建20个学生对象，学号为1到20，年级和成绩都由随机数确定。
 * 问题一：打印出3年级(state值为3）的学生信息。
 * 问题二：使用冒泡排序按学生成绩排序，并遍历所有学生信息
 * 提示：  1) 生成随机数：Math.random()，返回值类型double;  
 * 		2) 四舍五入取整：Math.round(double d)，返回值类型long。
 * 
 * 此代码是对StudentTest.java的改进，将操作数组的功能封装到方法中。
 */
public class StudentTest2 {
	public static void main(String[] args) {
		//声明一个Student类型的数组
		Student2[] stu = new Student2[20];
		
		for(int i = 0;i <stu.length;i++){
			//给数组元素赋值
			stu[i] = new Student2();
			//给Student的对象的属性赋值
			stu[i].number = i + 1;
			//年级:[1,6]
			stu[i].state = (int)(Math.random() * (6 - 1 + 1) + 1);
			//成绩:[0,100]
			stu[i].score = (int)(Math.random() * (100 - 0 + 1));
		}
		
		StudentTest2 test = new StudentTest2();
		
		//遍历学生数组
		test.print(stu);
		
		System.out.println("*********以下是问题1*********");
		
		//问题一：打印出3年级(state值为3）的学生信息。
		test.searchState(stu, 3);
		System.out.println("********以下是问题2**********");
		
		//问题二：使用冒泡排序按学生成绩排序，并遍历所有学生信息。
		test.sort(stu);
		
		//遍历学生数组
		for(int i = 0;i < stu.length;i++){
			System.out.println(stu[i].info());
		}
	}
	
	/**
	  * 
	  * @Description 遍历Student[]数组的操作
	  * @author subei
	  * @date 2020年4月15日下午8:25:36
	  * @param stu
	 */
	public void print(Student2[] stu){
		for(int i = 0;i < stu.length;i++){	
			System.out.println(stu[i].info());
		}
	}
	
	/**
	  * 
	  * @Description 查找Student数组中指定年级的学习信息
	  * @author subei
	  * @date 2020年4月15日下午8:22:34
	  * @param stu
	  * @param state
	 */
	public void searchState(Student2[] stu,int state){
		for(int i = 0;i < stu.length;i++){
			if(stu[i].state == state){
				System.out.println(stu[i].info());
			}
		}
	}
	
	/**
	  * 
	  * @Description 给Student数组排序
	  * @author subei
	  * @date 2020年4月15日下午8:24:33
	  * @param stu
	 */
	public void sort(Student2[] stu){
		for(int i = 0;i < stu.length - 1;i++){
			for(int j = 0;j <stu.length - 1 - i;j++){
				if(stu[j].score >stu[j+1].score){
					//如果需要换序，交换的是数组的元素，Student对象！！！
					Student2 temp = stu[j];
					stu[j] = stu[j+1];
					stu[j+1] = temp;
				}
			}
		}
	}
}
class Student2{
	int number;	//学号
	int state;	//年级
	int score;	//成绩
	
	//显示学生信息的方法
	public String info(){
		return "学号:" + number + ",年级:" + state + ",成绩:" + score;
	}
}
```
> 整个Java全栈系列都是笔者自己敲的笔记。写作不易，如果可以，点个赞呗！✌


