@[TOC]
> 全部源码：https://github.com/name365/JavaSE-30Day
# 第3章 数组
## 3.1 数组的概述
```java
/*
 * 一、数组的概述
 * 1.数组的理解：数组(Array)，是多个相同类型数据按一定顺序排列的集合，
 * 并使用一个名字命名，并通过编号的方式对这些数据进行统一管理。
 * 
 * 2.数组的相关概念：
 * >数组名
 * >元素
 * >角标、下标、索引
 * >数组的长度：元素的个数
 * 
 * 3.数组的特点：
 * 1)数组属于引用类型的变量。数组的元素，既可以是基本数据类型，也可以是引用数据类型。
 * 2)创建数组对象会在内存中开辟一整块连续的空间；
 * 3)数组的长度一旦确定，就不能修改;
 * 4)数组是有序排列的。
 * 
 * 4.数组的分类：
 * 	① 按照维数：一维数组、二维数组、三维数组……
 *  ② 按照数组元素类型：基本数据类型元素的数组、引用类型元素的数组
 *  
 */
```
## 3.2 一维数组的使用
```java
/*
 * 	① 一维数组的声明和初始化
 *  ② 如何调用数组的指定位置的元素
 *  ③ 如何获取数组的长度
 *  ④ 如何遍历数组
 *  ⑤ 数组元素的默认初始化值：见ArrayTest1.java
 *  ⑥ 数组的内存解析：见ArrayTest1.java
 */
```
代码案例1——ArrayTest.java
```java
public class ArrayTest {
	public static void main(String[] args) {
		
		//1. 一维数组的声明和初始化
		int num;	//声明
		num = 10;	//初始化
		int id = 1001;	//声明 + 初始化
		
		int[] ids;	//声明
		//1.1静态初始化:数组的初始化和数组元素的赋值操作同时进行
		ids = new int[]{1001,1002,1003,1004};	
		//1.2动态初始化:数组的初始化和数组元素的赋值操作分开进行
		String[] names = new String[5]; 
		
		//错误的写法：
//		int[] arr1 = new int[];	//未赋值、未指明长度
//		int[5] arr2 = new int[5];
//		int[] arr3 = new int[3]{1,2,3};
		
		//也是正确的写法：
		int[] arr7 = {1,2,3,5,4};//类型推断
		
		/*总结：数组一旦初始化完成，其长度就确定了。
		*/
		
		//2.如何调用数组的指定位置的元素：通过角标的方式调用。
		//数组的角标(或索引)从0开始的，到数组的长度-1结束
		names[0] = "张郃";
		names[1] = "王陵";
		names[2] = "张学良";
		names[3] = "王传志";	//charAt(0)
		names[4] = "李峰";
//		names[5] = "周礼";	//如果数组超过角标会通过编译，运行失败。
		
		//3.如何获取数组的长度
		//属性：length
		System.out.println(names.length);	//5
		System.out.println(ids.length);	//4
		
		//4.如何遍历数组
//		System.out.println(names[0]);
//		System.out.println(names[1]);
//		System.out.println(names[2]);
//		System.out.println(names[3]);
//		System.out.println(names[4]);
		
		for(int i = 0;i < names.length;i++){
			System.out.println(names[i]);
		}
		
	}
}
```
代码案例2——ArrayTest1.java
```java
/*
 * ⑤ 数组元素的默认初始化值
 * 		> 数组元素是整形：0
 * 		> 数组元素是浮点型：0.0
 * 		> 数组元素是char型：0或'\u0000'，而非'0'
 * 		> 数组元素是boolean型:false
 * 
 * 		> 数组元素是引用数据类型：null 
 */
public class ArrayTest1 {
	public static void main(String[] args) {
		//5.数组元素的默认初始化值
		int[] arr = new int[4];
		for(int i = 0;i < arr.length;i++){
			System.out.println(arr[i]);
		}
		System.out.println("*****************");
		
		short[] arr1 = new short[4];
		for(int i = 0;i < arr1.length;i++){
			System.out.println(arr1[i]);
		}
		System.out.println("*****************");
		
		float[] arr2 = new float[5]; 
		for(int i = 0;i < arr2.length;i++){
			System.out.println(arr2[i]);
		}
		System.out.println("*****************");
		
		char[] arr3 = new char[5]; 
		for(int i = 0;i < arr3.length;i++){
			System.out.println("----" + arr3[i] + "****");
		}
		
		if(arr3[0] == 0){
			System.out.println("你好！");
		}
		System.out.println("*****************");
		
		boolean[] arr4 = new boolean[5];
		System.out.println(arr4[0]);
		
		System.out.println("*****************");
		String[] arr5 = new String[5];
		System.out.println(arr5[0]);
		//验证
		if(arr5[0] == null){
			System.out.println("北京天气好差！");
		}
		
	}
}
```
### 内存的简化结构
![图片](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91cGxvYWRlci5zaGltby5pbS9mL3FPRGZza0JkMkdVbnh1WEMucG5nIXRodW1ibmFpbA?x-oss-process=image/format,png)

### 一维数组的内存解析
```java
int[] arr = new int[]{1,2,3};
String[] arr1 = new String[4];
arr1[1] = “刘德华”;
arr1[2] = “张学友”;
arr1 = new String[3];
System.out.println(arr1[1]);//null
```
![图片](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91cGxvYWRlci5zaGltby5pbS9mL2tZNWc3c0hjem9LTEcwUjUucG5nIXRodW1ibmFpbA?x-oss-process=image/format,png)

* 按照图中步骤，最后数组内存解析完成，数组内部值为null。

### 练习1

```java
/*
 * 升景坊单间短期出租4个月，550元/月（水电煤公摊，网费35元/月），空调、卫生间、厨房齐全。
 * 屋内均是IT行业人士，喜欢安静。所以要求来租者最好是同行或者刚毕业的年轻人，爱干净、安静。
 * eclipse代码一键格式规范化：Ctrl+Shift+F
 */
public class ArrayDemo {
	public static void main(String[] args) {
		int[] arr = new int[] { 8, 2, 1, 0, 3 };
		int[] index = new int[] { 2, 0, 3, 2, 4, 0, 1, 3, 2, 3, 3 };
		String tel = "";
		for (int i = 0; i < index.length; i++) {
			tel += arr[index[i]];
		}
		System.out.println("联系方式：" + tel);
	}
}
```
练习2
```java
/*
 * 2. 从键盘读入学生成绩，找出最高分，并输出学生成绩等级。
 * 成绩>=最高分-10    等级为’A’   
 * 成绩>=最高分-20    等级为’B’
 * 成绩>=最高分-30    等级为’C’   
 * 其余等级为’D’
 * 提示：先读入学生人数，根据人数创建int数组，存放学生成绩。
 */
import java.util.Scanner;
public class ArrayDemo2 {
	public static void main(String[] args) {
		//1.使用Scanner，读取学生的个数
		Scanner scan = new Scanner(System.in);
		System.out.print("请输入学生人数：");
		int num = scan.nextInt();
		
		//2.创建数组，存储学生成绩，动态初始化
		int[] str = new int[num];
		System.out.println("请输入" + num + "个学生成绩");
				
		//3.给数组中的元素赋值
		int maxnum = 0;
		for(int i = 0;i < str.length;i++){
			str[i] = scan.nextInt();
			//4.获取数组元素中的最大值：最高分
			if(maxnum < str[i]){
				maxnum = str[i];
			}
		}
		
		//5.根据每个学生成绩与最高分的差值，得到每个学生的等级，并输出等级和成绩	
		char Grade;	//成绩等级
		for(int i = 0;i < str.length;i++){
			if(maxnum - str[i] <= 10){
				Grade = 'A';
			}else if(maxnum - str[i] <= 20){
				Grade = 'B';
			}else if(maxnum - str[i] <= 30){
				Grade = 'C';
			}else{
				Grade = 'D';
			}
			
			System.out.println("student " + i + "score is" + str[i] + 
					" grade is " + Grade);
		}
	}
}
```
## 3.3 多维数组的使用
* Java 语言里提供了支持多维数组的语法。
* 如果说可以把一维数组当成几何中的线性图形，那么二维数组就相当于是一个表格，像下图Excel中的表格一样。

![图片](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91cGxvYWRlci5zaGltby5pbS9mL3I2VmNjOUhGZ1NBZVVBd2gucG5nIXRodW1ibmFpbA?x-oss-process=image/format,png)

### 二位数组
代码案例——ArrayTest2.java

```java
/*
 * 二维数组的使用
 * 
 * 1.理解
 * 对于二维数组的理解，我们可以看成是一维数组array1又作为另一个一维数组array2的元素而存在。
 * 其实，从数组底层的运行机制来看，其实没有多维数组。
 * 
 * 2.二维数组的使用：
 * 	① 二位数组的初始化
 *  ② 如何调用数组的指定位置的元素
 *  ③ 如何获取数组的长度
 *  ④ 如何遍历数组
 *  ⑤ 数组元素的默认初始化值:见ArrayTest3.java
 *  ⑥ 数组的内存解析:见ArrayTest3.java
 * 
 */
public class ArrayTest2 {
	public static void main(String[] args) {
		//1.二维数组的声明和初始化
		int[] arr = new int[]{1,2,3};
		//静态初始化
		int[][] arr1 = new int[][]{{1,2,3},{4,5,6},{7,8,9}};
		//动态初始化1
		String[][] arr2 = new String[3][2];
		//动态初始化2
		String[][] arr3 = new String[3][];
		
		//错误的情况
//		String[][] arr4 = new String[][];
//		String[][] arr5 = new String[][4];
//		String[][] arr6 = new String[4][3]{{1,2,3},{4,5,6},{7,8,9}};
		
		//正确的情况：
		int arr4[][] = new int[][]{{1,2,3},{4,5,12,6},{7,8,9}};
		int[] arr5[] = new int[][]{{1,2,3},{4,5,6},{7,8,9}};
		int[][] arr6 = {{1,2,3},{4,5,6},{7,8,9}};		
		
		//2.如何调用数组的指定位置的元素
		System.out.println(arr1[0][1]);	//2
		System.out.println(arr2[1][1]);	//null
		
		arr3[1] = new String[4];	//定义arr3的[1]为长度为4的字符数组
		System.out.println(arr3[1][0]);	//没有上句，会报错
		
		//3.获取数组的长度
		System.out.println(arr4.length);	//3
		System.out.println(arr4[0].length);	//3
		System.out.println(arr4[1].length);	//4
		
		//4.如何遍历二维数组
		for(int i = 0;i < arr4.length;i++){
			for(int j = 0;j < arr4[i].length;j++){
				System.out.print(arr4[i][j] + " ");
			}
			System.out.println();
		}
	}
}
```
代码案例——ArrayTest3.java
```java
/*
 * 二维数组的使用：
 * 	规定：二维数组分为外层数组的元素，内层数组的元素
 * 	int[][] arr = new int[4][3]; 
 *  外层元素:arr[0],arr[1]等
 *  内层元素:arr[0][0],arr[1][2]等
 *  
 * 	⑤ 数组元素的默认初始化值
 * 	针对于初始化方式一：比如：int[][] arr = new int[4][3];
 * 		外层元素的初始化值为：地址值
 * 		内层元素的初始化值为：与一维数组初始化情况相同
 * 	
 * 针对于初始化方式而：比如：int[][] arr = new int[4][];
 * 		外层元素的初始化值为：null
 * 		内层元素的初始化值为：不能调用，否则报错。
 * 
 * 	⑥ 数组的内存解析
 */
public class ArrayTest3 {
	public static void main(String[] args) {
		
		int[][] arr = new int[4][3];
		System.out.println(arr[0]);	//[I@15db9742
		System.out.println(arr[0][0]);	//0
		
//		System.out.println(arr);	//ArrayTest3.java
		
		System.out.println("***********************");
		float[][] arr1 = new float[4][3];
		System.out.println(arr1[0]);	//地址值
		System.out.println(arr1[0][0]);	//0.0
		
		System.out.println("***********************");
		
		String[][] arr2 = new String[4][2];
		System.out.println(arr2[1]);	//地址值
		System.out.println(arr2[1][1]);	//null
		
		System.out.println("*********************");
		double[][] arr3 = new double[4][];
		System.out.println(arr3[1]);	//null
//		System.out.println(arr3[1][0]);	//报错
	}
}
```
### 二维数组的内存解析
 * 案例1

```java
int[][] arr1 = new int[4][];
arr1[1] = new int[]{1,2,3};
arr1[2] = new int[4];
arr1[2][1] = 30;
```
![图片](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91cGxvYWRlci5zaGltby5pbS9mL2xiZjhRZjdoRXNqTGtmWHoucG5nIXRodW1ibmFpbA?x-oss-process=image/format,png)

 - 案例2

```java
int[][] arr4= newint[3][];
System.out.println(arr4[0]);//null
System.out.println(arr4[0][0]);//报错
arr4[0] = new int[3];
arr4[0][1] = 5;
arr4[1] = new int[]{1,2};
```
![图片](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91cGxvYWRlci5zaGltby5pbS9mL3N3am9xWTJjTjMwZk9aRE0ucG5nIXRodW1ibmFpbA?x-oss-process=image/format,png)

- 案例3

```java
int[][] arr = new int[3][];
arr[1] = new int[]{1,2,3};
arr[2] = new int[3];
System.out.println(arr[0]);//null
System.out.println(arr[0][0]);//报异常
```
![图片](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91cGxvYWRlci5zaGltby5pbS9mL1JkQnVPN1YydXRRZ0lCd1MucG5nIXRodW1ibmFpbA?x-oss-process=image/format,png)

- 案例4

```java
int[][] arr1= newint[4][];
arr1[0] = new int[3];
arr1[1] = new int[]{1,2,3};
arr1[0][2] = 5;
arr1 = new int[2][];
```
![图片](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91cGxvYWRlci5zaGltby5pbS9mL1g1Y2tvMG5DUVo4SlprRkcucG5nIXRodW1ibmFpbA?x-oss-process=image/format,png)
### 练习
![图片](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91cGxvYWRlci5zaGltby5pbS9mLzQ4R2VmaGpDNE13MGhWcU8ucG5nIXRodW1ibmFpbA?x-oss-process=image/format,png)

```java
public class ArrayEver1 {
	public static void main(String[] args) {
		int[][] arr = new int[][]{{3,5,8},{12,9},{7,0,6,4}};
		int sum = 0;	//记录总和
		for(int i = 0;i < arr.length;i++){
			for(int j = 0;j < arr[i].length;j++){
				sum += arr[i][j];
			}
		}
		System.out.println(sum);
	}
}
```
练习 2
![图片](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91cGxvYWRlci5zaGltby5pbS9mL0c2MU1Pc3E3WHpJR1FzQTIucG5nIXRodW1ibmFpbA?x-oss-process=image/format,png)

练习 3

* 使用二维数组打印一个 10 行杨辉三角。
```java
/*
 * 【提示】
 * 1. 第一行有 1 个元素, 第 n 行有 n 个元素
 * 2. 每一行的第一个元素和最后一个元素都是 1
 * 3. 从第三行开始, 对于非第一个元素和最后一个元素的元素。
 * 即：yanghui[i][j] = yanghui[i-1][j-1] + yanghui[i-1][j];
 */
public class ArrayEver2 {
	public static void main(String[] args) {
		//1.声明并初始化二维数组
		int[][] arr = new int[10][];
		
		//2.给数组的元素赋值，遍历二维数组
		for(int i = 0;i < arr.length;i++){
			arr[i] = new int[i+1];
			
			//2.1 给首末元素赋值
			arr[i][0]=arr[i][i]=1;
			//2.2 给每行的非首末元素赋值
		//	if(i > 1){
			for(int j = 1;j < arr[i].length-1;j++){
					arr[i][j] = arr[i-1][j-1] + arr[i-1][j];
				}
		//	}
	
		}
		
	//	3.遍历数组
		for(int i = 0;i < arr.length;i++){
			for(int j = 0;j <arr[i].length;j++){
				System.out.print(arr[i][j] + " ");
			}
			System.out.println();
		}
		
	}
}
```
### 面试题目
* 创建一个长度为 6 的 int 型数组，要求取值为 1-30，同时元素值各不相同
```java
//此题只做了解，初学不必精通。
public class ArrayEver3 {
	public static void main(String[] args) {
		// 方式一：
//		int[] arr = new int[6];
//		for (int i = 0; i < arr.length; i++) {// [0,1) [0,30) [1,31)
//			arr[i] = (int) (Math.random() * 30) + 1;
//
//			boolean flag = false;
//			while (true) {
//				for (int j = 0; j < i; j++) {
//					if (arr[i] == arr[j]) {
//						flag = true;
//						break;
//					}
//				}
//				if (flag) {
//					arr[i] = (int) (Math.random() * 30) + 1;
//					flag = false;
//					continue;
//				}
//				break;
//			}
//		}
//
//		for (int i = 0; i < arr.length; i++) {
//			System.out.println(arr[i]);
//		}
		// 方式二：
		int[] arr2 = new int[6];
		for (int i = 0; i < arr2.length; i++) {// [0,1) [0,30) [1,31)
			arr2[i] = (int) (Math.random() * 30) + 1;

			for (int j = 0; j < i; j++) {
				if (arr2[i] == arr2[j]) {
					i--;
					break;
				}
			}
		}

		for (int i = 0; i < arr2.length; i++) {
			System.out.println(arr2[i]);
		}
	}
}    
```
> 整个Java全栈系列都是笔者自己敲的笔记。写作不易，如果可以，点个赞呗！✌


