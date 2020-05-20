[TOC]
> 原文：https://shimo.im/docs/hRQv86cQpxWTPV9P/ 《第四章 面向对象(上)》
# 第四章 面向对象(上)
## 4.4 类的成员之二：方法
### 类中方法的声明和使用
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
**练习1**

* 创建一个Person类，其定义如下：

![图片](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91cGxvYWRlci5zaGltby5pbS9mL3h2eVN2WkQ0Z21VV3VZRGoucG5nIXRodW1ibmFpbA?x-oss-process=image/format,png#pic_center)

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
 **练习2**

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
**练习3**

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
**练习四**

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
**练习四优化**

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
### 理解“万事万物皆对象”
```java
/* 1.在Java语言范畴中，我们都将功能、结构等封装到类中，通过类的实例化，来调用具体的功能结构。
 * 		》Scanner,String等
 * 		》文件：File
 * 		》网络资源：URL
 * 2.涉及到Java语言与前端html、后端的数据库交互时，前后端的结构在Java层面交互时，都体现为类、对象。
 */
```
### 对象数组的内存解析
```java
/*引用类型的变量，只可能存储量两类值：null或地址值（含变量类型）*/
Student[] stus= newStudent[5];
stus[0] = new Student();
sysout(stus[0].state);//1
sysout(stus[1]);//null
sysout(stus[1].number);//异常
stus[1] = new Student();
sysout(stus[1].number);//0

class Student{
  int number;//学号
  int state = 1;//年级
  int score;//成绩
}
```
![图片](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91cGxvYWRlci5zaGltby5pbS9mLzhSOFlsT0taSFB4c2hza1YucG5nIXRodW1ibmFpbA?x-oss-process=image/format,png)
### 匿名对象的使用
```java
/* 
 * 三、匿名对象的使用
 * 1.理解:我们创建的对象，没有显示的赋值给一个变量名。即为匿名对象。
 * 2.特征：匿名对象只能调用一次。
 * 3.使用:如下
 */
public class InstanceTest {
	public static void main(String[] args) {
		Phone p = new Phone();
//		p = null;
		System.out.println(p);
		
		p.sendEmail();
		p.playGame();
		
		//匿名对象
//		new Phone().sendEmail();
//		new Phone().playGame();
		
		new Phone().price = 1999;
		new Phone().showPrice();	//0.0
		
		//*******************************
		PhoneMall mall = new PhoneMall();
//		mall.show(p);
		//匿名对象的使用
		mall.show(new Phone());	
	}
}

class PhoneMall{
	
	public void show(Phone phone){
		phone.sendEmail();
		phone.playGame();
	}
}

class Phone{
	double price;	//价格
	
	public void sendEmail(){
		System.out.println("发邮件");
	}
	public void playGame(){
		System.out.println("打游戏");
	}
	public void showPrice(){
		System.out.println("手机价格为:" + price);
	}
}
```
### 自定义数组的工具类
**工具类**

```java
/*
 * 自定义数组工具类
 */
public class ArrayUtil {

	// 求数组的最大值
	public int getMax(int[] arr) {
		int maxValue = arr[0];
		for (int i = 1; i < arr.length; i++) {
			if (maxValue < arr[i]) {
				maxValue = arr[i];
			}
		}
		return maxValue;
	}

	// 求数组的最小值
	public int getMin(int[] arr) {
		int minValue = arr[0];
		for (int i = 1; i < arr.length; i++) {
			if (minValue > arr[i]) {
				minValue = arr[i];
			}
		}
		return minValue;
	}

	// 求数组总和
	public int getSum(int[] arr) {
		int sum = 0;
		for (int i = 0; i < arr.length; i++) {
			sum += arr[i];
		}
		return sum;
	}

	// 求数组平均值
	public int getAvg(int[] arr) {
		int avgValue = getSum(arr) / arr.length;
		return avgValue;
	}

	// 反转数组
	public void reverse(int[] arr) {
		for (int i = 0; i < arr.length / 2; i++) {
			int temp = arr[i];
			arr[i] = arr[arr.length - i - 1];
			arr[arr.length - i - 1] = temp;
		}
	}

	// 复制数组
	public int[] copy(int[] arr) {
		int[] arr1 = new int[arr.length];
		for (int i = 0; i < arr1.length; i++) {
			arr1[i] = arr[i];
		}
		return null;
	}

	// 数组排序
	public void sort(int[] arr) {
		for (int i = 0; i < arr.length - 1; i++) {
			for (int j = 0; j < arr.length - 1 - i; j++) {
				if (arr[j] > arr[j + 1]) {
					int temp = arr[j];
					arr[j] = arr[j + 1];
					arr[j + 1] = temp;
				}
			}
		}
	}

	// 遍历数组
	public void print(int[] arr) {
		System.out.print("[");
		for (int i = 0; i < arr.length; i++) {
			System.out.print(arr[i] + ",");
		}
		System.out.println("]");
	}

	// 查找指定元素
	public int getIndex(int[] arr, int dest) {
		//线性查找
		for (int i = 0; i < arr.length; i++) {
			if (dest==arr[i]) {
				return i;
			}
		}
		return -1;
	}
}
```
**测试类**

```java
/**
  * @Description 测试类
  * @author subei Email:subei@163.com
  * @version
  * @date 2020年4月19日下午3:17:48
  *
 */
public class ArrayUtilTest {


	public static void main(String[] args) {
		ArrayUtil util = new ArrayUtil();
		int[] arr = new int[]{32,5,26,74,0,96,14,-98,25};
		int max = util.getMax(arr);
		System.out.println("最大值为:" + max);
		
//		System.out.print("排序前:");
//		util.print(arr);
//		
//		util.sort(arr);
//		System.out.print("排序后:");
//		util.print(arr);
		
		System.out.println("查找:");
		int index = util.getIndex(arr, 5);
		if(index > 0){
			System.out.println("找到了，索引地址:" + index);
		}else{
			System.out.println("没找到");
		}
	}
}
```
## 4.5 再谈方法
### 方法的重载(overload)

```java
/*
 * 方法的重载(overload)loading...
 * 
 * 1.定义:在同一个类中，允许存在一个以上的同名方法，只要它们的参数个数或者参数类型不同即可。
 * 	
 * 		“两同一不同”:同一个类、相同方法名
 * 				  参数列表不同：参数个数不同，参数类型不同
 * 
 * 2.举例:
 * 		Arrays类中重载的sort() / binarySearch()
 * 
 * 3.判断是否重载
 * 		与方法的返回值类型、权限修饰符、形参变量名、方法体都无关。
 * 
 * 4.在通过对象调用方法时，如何确定某一个指定的方法：
 * 		方法名---》参数列表
 */
public class OverLoadTest {
	
	public static void main(String[] args) {
		OverLoadTest test = new OverLoadTest();
		test.getSum(1, 2);	//调用的第一个，输出1
	}

	//如下的四个方法构成了重载
	public void getSum(int i,int j){
		System.out.println("1");
	}
	public void getSum(double d1,double d2){
		System.out.println("2");
	}
	public void getSum(String s,int i){
		System.out.println("3");
	}
	
	public void getSum(int i,String s){
		
	}
	
	//以下3个是错误的重载
//	public int getSum(int i,int j){
//		return 0;
//	}
	
//	public void getSum(int m,int n){
//		
//	}
	
//	private void getSum(int i,int j){
//		
//	}
}
```
**举例**

```java
1.判断：
与void show(int a,char b,double c){}构成重载的有：
a)void show(int x,char y,double z){} // no
b)intshow(int a,double c,charb){} // yes
c) void show(int a,double c,char b){} // yes
d) booleanshow(int c,char b){} // yes
e) void show(double c){} // yes 
f) double show(int x,char y,double z){} // no
g) void shows(){double c} // no
```
**编程**

```java
/*
 * 1.编写程序，定义三个重载方法并调用。方法名为mOL。
 * 三个方法分别接收一个int参数、两个int参数、一个字符串参数。
 * 分别执行平方运算并输出结果，相乘并输出结果，输出字符串信息。
 * 在主类的main ()方法中分别用参数区别调用三个方法。
 * 2.定义三个重载方法max()，
 * 第一个方法求两个int值中的最大值，
 * 第二个方法求两个double值中的最大值，
 * 第三个方法求三个double值中的最大值，并分别调用三个方法。
 * 
 */
public class OverLoadever {
	
	public static void main(String[] args) {
		OverLoadever test = new OverLoadever();
		//1.调用3个方法
		test.mOL(5);
		test.mOL(6, 4);
		test.mOL("fg");
		
		//2.调用3个方法
		int num1 = test.max(18, 452);
		System.out.println(num1);
		double num2 = test.max(5.6, -78.6);
		System.out.println(num2);
		double num3 = test.max(15, 52, 42);
		System.out.println(num3);
	}

	//1.如下三个方法构成重载
	public void mOL(int i){
		System.out.println(i*i);
	}
	public void mOL(int i,int j){
		System.out.println(i*j);
	}
	public void mOL(String s){
		System.out.println(s);
	}
	
	//2.如下三个方法构成重载
	public int max(int i,int j){
		return (i > j) ? i : j;
	}
	public double max(double i,double j){
		return (i > j) ? i : j;
	}
	public double max(double d1,double d2,double d3){
		double max = (d1 > d2) ? d1 : d2;
		return (max > d3) ? max : d3;
	}
}
```
### 可变个数的形参
> JavaSE 5.0 中提供了Varargs(variable number of arguments)机制，允许`直接定义能和多个实参相匹配的形参`。从而，可以用一种更简单的方式，来传递个数可变的实参。

```java
/*
 * 可变个数形参的方法
 * 1.jdk 5.0新增的内容
 * 2.具体使用：
 * 	2.1 可变个数形参的格式：数据类型 ... 变量名
 * 	2.2 当调用可变个数形参的方法时，传入的参数的个数可以是：0个，1个，2个...
 * 	2.3可变个数形参的方法与本类中方法名相同，形参不同的方法之间构成重载。
 *  2.4可变个数形参的方法与本类中方法名相同，形参类型也相同的数组之间不构成重载。即二者不可共存。
 *  2.5可变个数形参在方法中的形参中,必须声明在末尾。
 *  2.6可变个数形参在方法中的形参中，最多只能声明一个可变形参。
 */
public class MethodArgs {

	public static void main(String[] args) {
		MethodArgs test = new MethodArgs();
		test.show(12);
		// test.show("hell0");
		// test.show("hello","world");
		// test.show();

		test.show(new String[] { "AA", "BB", "CC" });
	}

	public void show(int i) {

	}

	// public void show(String s){
	// System.out.println("show(String)");
	// }
	public void show(String... strs) {
		System.out.println("show(String ...strs)");


		for (int i = 0; i < strs.length; i++) {
			System.out.println(strs[i]);
		}
	}

	// 此方法与上一方法不可共存
	// public void show(String[] strs){
	//
	// }

	public void show(int i, String... strs) {

	}

	//The variable argument type String of the method show must be the last parameter
//	public void show(String... strs,int i,) {
//
//	}
}
```
### 方法参数的值传递机制(重点！！！)
```java
/*
 * 关于变量的赋值
 * 
 * 	如果变量是基本数据类型，此时赋值的是变量所保存的数据值。
 * 	如果变量是引用数据类型，此时赋值的是变量所保存的数据的地址值。
 * 
 */
public class ValueTransferTest {

	public static void main(String[] args) {
		
		System.out.println("**********基本数据类型：***********");
		int m = 10;
		int n = m;
		
		System.out.println("m = " + m + ", n = " + n);
		
		n = 20;
		
		System.out.println("m = " + m + ", n = " + n);

		System.out.println("***********引用数据类型:********");
		
		Order o1 = new Order();
		o1.orderId = 1001;
		
		Order o2 = o1;	//赋值后，o1和o2的地址值相同，都指向了堆空间中同一个对象实体
		System.out.println("o1.orderId = " + o1.orderId + ",o2.orderId = " + o2.orderId);
		
		o2.orderId = 1002;
		System.out.println("o1.orderId = " + o1.orderId + ",o2.orderId = " + o2.orderId);
		
	}
}

class Order{
	int orderId;
}
```
**针对基本数据类型**
```java
/*
 * 方法的形参的传递机制：值传递
 * 
 * 1.形参：方法定义时，声明的小括号内的参数
 *   实参：方法调用时，实际传递给形参的数据
 * 
 * 2.值传递机制：
 *  如果参数是基本数据类型，此时实参赋值给形参的是实参真是存储的数据值。
 */
public class ValueTransferTest1 {

	public static void main(String[] args) {
		
		int m = 10;
		int n = 20;
		
		System.out.println("m = " + m + ", n = " + n);
		//交换两个变量的值的操作
//		int temp = m;
//		m = n;
//		n = temp;
		
		ValueTransferTest1 test = new ValueTransferTest1();
		test.swap(m, n);
		
		System.out.println("m = " + m + ", n = " + n);
		
	}
	
	public void swap(int m,int n){
		int temp = m;
		m = n;
		n = temp;
	}
}
```
![图片](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91cGxvYWRlci5zaGltby5pbS9mL041cDgxNGlIekxoM0JtVkQucG5nIXRodW1ibmFpbA?x-oss-process=image/format,png#pic_center)

**针对引用数据类型**

```java
/*
 *  如果参数是引用数据类型，此时实参赋值给形参的是实参存储数据的地址值。
 */
public class ValueTransferTest2 {

	public static void main(String[] args) {
		Data data = new Data();
		
		data.m = 10;
		data.n = 20;
		
		System.out.println("m = " + data.m + ", n = " + data.n);

		//交换m和n的值
//		int temp = data.m;
//		data.m = data.n;
//		data.n = temp;

		ValueTransferTest2 test = new ValueTransferTest2();
		test.swap(data);
		
		System.out.println("m = " + data.m + ", n = " + data.n);

	}
	
	public void swap(Data data){
		int temp = data.m;
		data.m = data.n;
		data.n = temp;
	}
}


class Data{
	
	int m;
	int n;
}
```
![图片](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91cGxvYWRlci5zaGltby5pbS9mL2RNYnlJd01sdHlRcWxVU3MucG5nIXRodW1ibmFpbA?x-oss-process=image/format,png#pic_center)

**练习1**

```java
public class TransferTest3{
	public static void main(String args[]){
		TransferTest3 test=new TransferTest3();
		test.first();
	}
	
	public void first(){
		int i=5;
		Value v=new Value();
		v.i=25;
		second(v,i);
		System.out.println(v.i);
	}
	
	public void second(Value v,int i){
		i=0;
		v.i=20;
		Value val=new Value();
		v=val;
		System.out.println(v.i+" "+i);
		
	}
}
class Value {
	int i= 15;
}
```

![图片](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91cGxvYWRlci5zaGltby5pbS9mL2FobDZ2Q1p2SzJ3SWRmclYucG5nIXRodW1ibmFpbA?x-oss-process=image/format,png#pic_center)

**练习2**
![图片](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91cGxvYWRlci5zaGltby5pbS9mL0hZQlF5WUxxcHJJcUxTUGMucG5nIXRodW1ibmFpbA?x-oss-process=image/format,png#pic_center)

```java
public static void method(int a,int b){
	a = a * 10;
	b = b * 20;
	System.out.println(a);
	System.out.println(b);
	System.exit(0);
}
```
**练习3**

```java
/*
 * 微软：
 * 定义一个int型的数组：int[] arr = new int[]{12,3,3,34,56,77,432};
 * 让数组的每个位置上的值去除以首位置的元素，得到的结果，作为该位置上的新值。遍历新的数组。 
 */
 
//错误写法
for(int i= 0;i < arr.length;i++){
	arr[i] = arr[i] / arr[0];
}

//正确写法1
for(int i = arr.length –1;i >= 0;i--){
	arr[i] = arr[i] / arr[0];
}
//正确写法2
int temp = arr[0];
for(int i= 0;i < arr.length;i++){
	arr[i] = arr[i] / temp;
}
```
**练习4**

```java
/*
 * int[] arr = new int[10];
 * System.out.println(arr);//地址值?
 * 
 * char[] arr1 = new char[10];
 * System.out.println(arr1);//地址值?
 */
public class ArrayPrint {

	public static void main(String[] args) {
		int[] arr = new int[]{1,2,3};
		System.out.println(arr);//地址值
		
		char[] arr1 = new char[]{'a','b','c'};
		System.out.println(arr1);//abc
	}
}
```
**练习5：将对象作为参数传递给方法**

```java
/*
 * 练习5：将对象作为参数传递给方法
 * (1)定义一个Circle类，包含一个double型的radius属性代表圆的半径，一个findArea()方法返回圆的面积。
 * 
 * (2)定义一个类PassObject，在类中定义一个方法printAreas()，该方法的定义如下：
 * public void printAreas(Circle c,int time)
 * 在printAreas方法中打印输出1到time之间的每个整数半径值，以及对应的面积。
 * 例如，times为5，则输出半径1，2，3，4，5，以及对应的圆面积。
 * 
 * (3)在main方法中调用printAreas()方法，调用完毕后输出当前半径值。
 *
 */
public class Circle {

	double radius;	//半径
	
	//返回圆的面积
	public double findArea(){
		return radius * radius * Math.PI;
	}
}
```
**PassObject类**

```java
public class PassObject {
	
	public static void main(String[] args) {
		PassObject test = new PassObject();
		
		Circle c = new Circle();
		
		test.printAreas(c, 5);
		
		System.out.println("no radius is:" + c.radius);
	}
	
	public void printAreas(Circle c,int time){
		
		System.out.println("Radius\t\tAreas");
		
		//设置圆的半径
		for(int i = 1;i <= time ;i++){
			c.radius = i;
			System.out.println(c.radius + "\t\t" + c.findArea());
		}
		
		//重新赋值
		c.radius = time + 1;
	}
}
```
### 递归(recursion)方法

```java
/*
 * 递归方法的使用(了解)
 * 1.递归方法：一个方法体内调用它自身。
 * 2.方法递归包含了一种隐式的循环，它会重复执行某段代码，但这种重复执行无须循环控制。
 * 
 * 3.递归一定要向已知方向递归，否则这种递归就变成了无穷递归，类似于死循环。
 * 
 */
public class RecursionTest {

	public static void main(String[] args) {

		// 例1:计算1-100之间所有自然数的和
		// 方法1:
		int sum = 0;
		for (int i = 1; i <= 100; i++) {
			sum += i;
		}
		System.out.println("sum = " + sum);

		// 方法2:
		RecursionTest test = new RecursionTest();
		int sum1 = test.getSum(100);
		System.out.println("sum1 = " + sum1);
	}

	// 例1:计算1-n之间所有自然数的和
	public int getSum(int n) {

		if (n == 1) {
			return 1;
		} else {
			return n + getSum(n - 1);
		}
	}

	// 例2:计算1-n之间所有自然数的乘积
	//归求阶乘(n!)的算法
	public int getSum1(int n) {


		if (n == 1) {
			return 1;
		} else {
			return n * getSum1(n - 1);
		}
	}
}
```
**练习1**

```java
public class RecursionTest {

	public static void main(String[] args) {

		int value = test.f(10);
		System.out.println(value);
	}

	//例3:已知有一个数列：f(0) = 1,f(1) = 4,f(n+2)=2*f(n+1) + f(n),
	//其中n是大于0的整数，求f(10)的值。
	public int f(int n){
		if(n == 0){
			return 1;
		}else if(n == 1){
			return 4;
		}else{
			return 2*f(n-1) + f(n-2);
		}
	}
	
	//例4:已知一个数列：f(20) = 1,f(21) = 4,f(n+2) = 2*f(n+1)+f(n),
	//其中n是大于0的整数，求f(10)的值。
	public int f1(int n){
		if(n == 20){
			return 1;
		}else if(n == 21){
			return 4;
		}else{
			return 2*f1(n-1) + f1(n-2);
		}
	}
}
```
**练习2**

```java
/*
 * 输入一个数据n，计算斐波那契数列(Fibonacci)的第n个值
 * 1  1  2  3  5  8  13  21  34  55
 * 规律：一个数等于前两个数之和
 * 要求：计算斐波那契数列(Fibonacci)的第n个值，并将整个数列打印出来
 * 
 */
public class Recursion2 {

	public static void main(String[] args) {
		
		Recursion2 test = new Recursion2();
		int value = test.f(10);
		System.out.println(value);
	}
	
	public int f(int n) {

		if (n == 1 || n == 2) {
			return 1;
		} else {
			return f(n - 1) + f(n - 2);
		}
	}
}
```
> 整个Java全栈系列都是笔者自己敲的笔记。写作不易，如果可以，点个赞呗！✌
