[TOC]
> 原文：https://shimo.im/docs/jp3PJHPJkRGWxVXJ/ 《第2章Java基本语法(下)：程序流程控制》
# 第2章Java基本语法(下)：程序流程控制
## 2.5  程序流程控制
### 2.5.4  程序流程控制：循环结构
* 循环结构
  * 在某些条件满足的情况下，反复执行特定代码的功能
* 循环语句分类
  * for 循环
  * while 循环
  * do-while 循环

![图片](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91cGxvYWRlci5zaGltby5pbS9mL1h6Z2pTTDRLUWJJUEVVZTQucG5nIXRodW1ibmFpbA?x-oss-process=image/format,png)

循环结构1：for循环

```
语法格式
for(①初始化部分;②循环条件部分;④迭代部分)｛
            ③循环体部分;
｝


执行过程：①-②-③-④-②-③-④-②-③-④-.....-②


说明：
②循环条件部分为boolean类型表达式，当值为false时，退出循环
①初始化部分可以声明多个变量，但必须是同一个类型，用逗号分隔
④可以有多个变量更新，用逗号分隔
```
![图片](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91cGxvYWRlci5zaGltby5pbS9mL3E1TXhGNTlRR2hZbTE5WnYucG5nIXRodW1ibmFpbA?x-oss-process=image/format,png)

```
/*
For循环结构的使用
一、循环结构的四个要素
① 初始化条件
② 循环条件
③ 循环体
④ 迭代条件

二、for循环的结构
for(①;②;④){
	③
}
*/
class ForTest{
	public static void main(String[] args){
		for(int i=1;i <= 5 ;i++){
			System.out.println("Hello World!");
		}

		//练习：
		int num = 1;
		for(System.out.print('a');num <= 3;System.out.print('c'),num++){
			System.out.print('b');
		}

		//遍历100以内的偶数,获取所有偶数的和,输出偶数的个数
		int sum = 0;	//记录所有偶数的和
		int count = 0;
		for(int i = 1;i <= 100;i++){
			if(i %2 == 0){
				System.out.println(i);
				sum += i;
				count++;
			}
		}
		System.out.println("100以内的偶数的和：" + sum);
		System.out.println("个数为：" + count);
	}
}
```
练习1
```
/*
编写程序从1循环到150，并在每行打印一个值，
另外在每个3的倍数行上打印出“foo”,
在每个5的倍数行上打印“biz”,
在每个7的倍数行上打印输出“baz”。

*/
class ForTest1{
	public static void main(String[] args){
		
		for(int i = 1;i <= 150;i++ ){
			System.out.print(i + " ");
			if(i % 3 == 0){
				System.out.print("foo ");
			}
			if(i % 5 == 0){
				System.out.print("biz ");
			}
			if(i % 7 == 0){
				System.out.print("baz ");
			}

			//换行
			System.out.println();
		}
	}
}
```
练习2
```
/*
输入两个正整数m和n，求其最大公约数和最小公倍数。
比如：12和20的最大公约数是4，最小公倍数是60。说明：break关键字的使用

*/
import java.util.Scanner;
class GnumberTest{
	public static void main(String[] args){
		Scanner scan = new Scanner(System.in);
		System.out.println("请输入m:");
		int m = scan.nextInt();
		System.out.println("请输入n:");
		int n = scan.nextInt();
		//获取m和n的较大值
		int max = (m > n) ? m : n;
		//获取m和n的最小值
		int min = (m < n) ? m : n;
		
		//求最大公约数
		for(int i = min;i >= 1;i--){
			if(m % i == 0 && n % i == 0){
				System.out.println("m和n的最大公约数：" + i);
				break;
			}
		}

		//求最小公倍数
		for(int i = max;i <= m * n;i++){
			if( i % m == 0 && i % n == 0){
				System.out.println("m和n的最小公倍数是：" + i);
				break;
			}
		}
	}
}
```
练习3
```
/*
输出所有的水仙花数，所谓水仙花数是指一个3位数，其各个位上数字立方和等于其本身。
例如：153 = 1*1*1 + 3*3*3 + 5*5*5

*/
class ForTest2{
	public static void main(String[] args){
		for(int i = 100;i <= 999;i++){
			int a = i / 100;	//获取百位
			int b = i % 100 /10;	//获取十位
			int c = i % 10;	//获取个位
			if(a*a*a + b*b*b + c*c*c == i){
				System.out.println("此数值为满足条件的水仙花数:" + i);
			}
		}
	}
}
```
### 2.5.5  程序流程控制：循环结构之while循环
* 语法格式
```
①初始化部分
while(②循环条件部分)｛
    ③循环体部分;
    ④迭代部分;
}
```
* 执行过程：①-②-③-④-②-③-④-②-③-④-...-②
* 说明：
  * 注意不要忘记声明④迭代部分。否则，循环将不能结束，变成死循环。
  * for循环和while循环可以相互转换。
```
public class WhileLoop {
    public static void main(String args[]) {
        int result = 0;
        int i= 1;
        while(i<= 100) {
            result += i;
            i++;
        }
        System.out.println("result="+ result);
    }
}
```
练习
```
/*
While循环结构的使用
一、循环结构的四个要素
① 初始化条件
② 循环条件
③ 循环体
④ 迭代条件

二、while循环的结构
①初始化部分
while(②循环条件部分)｛
    ③循环体部分;
    ④迭代部分;
}

执行过程： ① - ② - ③ - ④ - ② -  ③ - ④ - ... - ② 

说明：
1.写while循环千万要小心不要丢了迭代条件。一旦丢了，就可能导致死循环！
2.写程序要避免死循环。
3.能用while循环的，可以用for循环，反之亦然。二者可以相互转换。
区别：for循环和while循环的初始化条件部分的作用范围不同。

算法：有限性。
*/
class WhileTest{
	public static void main(String[] args){
		//遍历100以内的所有偶数
		int i = 1;
		while(i <= 100){
			if(i % 2 == 0){
				System.out.println(i);
			}
			i++;
		}
	}
}
```
### 2.5.6  程序流程控制：循环结构之do-while循环
```
do-while循环结构的使用
一、循环结构的四个要素
① 初始化条件
② 循环条件 --->是boolean类型
③ 循环体
④ 迭代条件

二、do-while循环的结构
①
do{
	③;
	④;
}while(②);

执行过程：① - ③ - ④ - ② - ① - ③ - ④ - ... - ②
 
说明：do-while循环至少执行一次循环体。
```
练习1
```
class DoWhileTest{
	public static void main(String[] args){
		//遍历100以内的所有偶数,并计算所有偶数的和和偶数的个数
		int number = 1;
		int sum = 0;	//记录总和
		int count = 0;	//记录个数
		do{
			if(number % 2 == 0){
				System.out.println(number);
				sum += number;
				count++;
			}
			number++;
		}while(number <= 100);

		System.out.println("总和为：" + sum);
		System.out.println("个数为：" + count);

		//*********************************
		int numb = 10;
		while(numb > 10){
			System.out.println("hello:while");
			numb--;
		}

		int numb2 = 10;
		do{
			System.out.println("hello：do-while");
			numb2--;
		}while(numb2 > 10);
	}
}
```
练习2
```
/*
从键盘读入个数不确定的整数，并判断读入的正数和负数的个数，输入为0时结束程序。

说明：
1.不在循环条件部分限制次数的结构：while(true) , for(true)
2.结束循环的几种方式：
	方式一：循环条件部分返回false;
	方式二：在循环体中，执行break;
*/
import java.util.Scanner;
class XunTest{
	public static void main(String[] args) {
		Scanner scan = new Scanner(System.in);
		int Positive = 0;	//正数个数
		int Negative = 0;	//负数个数
		while(true){
			int number = scan.nextInt();
			if(number > 0){
				Positive++;
			}else if(number < 0){
				Negative++;
			}else{
				//一旦执行，跳出循环。
				break;
			}	
		}

		System.out.println("正数的个数：" + Positive);
		System.out.println("负数的个数：" + Negative);
	}
}
```
### 2.5.7  程序流程控制：嵌套循环结构
* 嵌套循环(多重循环)
  * 将一个循环放在另一个循环体内，就形成了嵌套循环。其中，for ,while ,do...while均可以作为外层循环或内层循环。
  * 实质上，嵌套循环就是把内层循环当成外层循环的循环体。当只有内层循环的循环条件为false时，才会完全跳出内层循环，才可结束外层的当次循环，开始下一次的循环。
  * 设外层循环次数为m次，内层为n次，则内层循环体实际上需要执行m*n次。
* 例题：
  1. 九九乘法表
  2. 100以内的所有质数

练习1

```
/*
嵌套循环的使用
1.嵌套循环：将一个循环结构A声明在另一个循环结构B的循环体中，就构成了嵌套循环

2.
外层循环：循环结构B
内层循环：循环结构A
3.说明
① 内层循环遍历一遍，只相当于外层循环循环体执行了一次
② 假设外层循环需要执行m次，内层循环需要执行n次。此时内层循环的循环体一共执行了m * n次

4.技巧
外层循环控制行数，内层循环控制列数
*/
class  ForForTest{
	public static void main(String[] args) {
		//******
		for(int i = 1;i <= 6;i++){
			System.out.print("*");
		}
		System.out.println();//换行

		/*
		******
		******
		******
		******
		*/
		for(int i = 1;i <= 4;i++){  
			for(int j = 1;j <= 6;j++){  
				System.out.print('*');
			}
			System.out.println();	//换行
		}
		/*
		*
		**
		***
		****
		*****
		*/
		for(int i = 1;i <= 5;i++){  //控制行数
			for(int j = 1;j <= i;j++){  //控制列数
				System.out.print("*");
			}
			System.out.println();
		}
		/*
		*****
		****
		***
		**
		*
		*/
		for(int i = 1;i <= 6;i++){
			for(int j = 1;j <= 6-i;j++){
				System.out.print("*");
			}
			System.out.println();
		}

		/*
		*
		**
		***
		****
		*****
		****
		***
		**
		*
		*/
		for(int i = 1;i <= 5;i++){
			for(int j = 1;j <= i;j++){
				System.out.print("*");
			}
			System.out.println();
		}

		for(int i = 1;i <= 5;i++){
			for(int j = 1;j <= 5-i;j++){
				System.out.print("*");
			}
			System.out.println();
		}

		//九九乘法表
		for(int i = 1;i <= 9;i++){
			for(int j = 1;j <= i;j++){
				System.out.print(i + "*" + j + "=" + i*j + " ");
			}
			System.out.println();	//换行
		}

	}
}
```
练习2
```
/*
100以内的所有质数
质数：素数，只能被1和它本身整除的自然数。

最小的质数是：2
*/
class PrimeNuberTest{
	public static void main(String[] args){
		boolean isFlag = true;	//标识是否被除尽，一旦除尽，修改其值。

		for(int i = 2;i <= 100;i++){	//遍历100以内的自然数
			for(int j =2;j < i;j++){	//j:被i去除
				if(i % j == 0){	//i被j除尽
					isFlag = false;
				}
			}
			if(isFlag == true){
				System.out.println(i);
			}

			//重置isFlag
			isFlag = true;
		}
	}
}
```
练习2的优化
```
/*
100000以内的所有质数
质数：素数，只能被1和它本身整除的自然数。

最小的质数是：2
*/

class PrimeNuberTest{
	public static void main(String[] args){
		boolean isFlag = true;	//标识是否被除尽，一旦除尽，修改其值。
		int count = 0;	//记录质数的个数

		//获取当前时间举例1970-01-01 00:00:00 的毫秒数
		long start = System.currentTimeMillis();

		for(int i = 2;i <= 100000;i++){	//遍历100以内的自然数
			//优化2：对本身是质数的自然数有效 5447---> 11
		//	for(int j =2;j < i;j++){	//j:被i去除
			for(int j =2;j <= Math.sqrt(i);j++){	//j:被i去除
				if(i % j == 0){	//i被j除尽
					isFlag = false;
					break;	//优化一：只对本身非质数的自然数是有效的。
				}
			}
			if(isFlag == true){
			//	System.out.println(i);
				count++;
			}

			//重置isFlag
			isFlag = true;
		}

		//获取当前时间举例1970-01-01 00:00:00 的毫秒数
		long end = System.currentTimeMillis();


		System.out.println("质数的个数:" + count);
		System.out.println("所花费的时间为:" + (end - start));	//16843 --> 5447	优化一
	}
}
```
### 2.5.8  程序流程控制：break、continue的使用
break的使用

* break 语句
  * break语句用于终止某个语句块的执行
```
{    
	......
	break;
	......
}
```
  * break语句出现在多层嵌套的语句块中时，可以通过标签指明要终止的是哪一层语句块
```
label1:	{	......
label2:		{	......
label3:			{	......
					break label2;
					......
				}
			}
		}
```
continue的使用
* continue 语句
  * continue只能使用在循环结构中
  * continue语句用于跳过其所在循环语句块的一次执行，继续下一次循环
  * continue语句出现在多层嵌套的循环语句体中时，可以通过标签指明要跳过的是哪一层循环

return的使用

* return：并非专门用于结束循环的，它的功能是结束一个方法。当一个方法执行到一个return语句时，这个方法将被结束。
* 与break和continue不同的是，return直接结束整个方法，不管这个return处于多少层循环之内。

特殊流程控制语句说明

* break只能用于switch语句和循环语句中。
* continue 只能用于循环语句中。
* 二者功能类似，但continue是终止本次循环，break是终止本层循环。
* break、continue之后不能有其他的语句，因为程序永远不会执行其后的语句。
* 标号语句必须紧接在循环的头部。标号语句不能用在非循环语句的前面。
* 很多语言都有goto语句，goto语句可以随意将控制转移到程序中的任意一条语句上，然后执行它。但使程序容易出错。Java中的break和continue是不同于goto的。

练习1

```
/*
break和countinue关键字的使用
				使用范围			循环中使用的作用(不同点)	相同点
break:			switch-case			结束当前循环				关键字后面不能声明执行语句
				循环结构中


countinue:		循环结构中			结束当次循环				关键字后面不能声明执行语句

*/
class BreakContinueTest{
	public static void main(String[] args){
		
		for(int i = 1;i <= 10;i++){
			if(i % 4 == 0){
			//	break;	//1、2、3
				continue;	//1、2、3、5、6、7、9、10
			//	System.out.println("该吃饭了！！！");
			}
		//	System.out.println(i);
		}
		//********************************
		for(int i = 1;i <= 4;i++){
			
				for(int j = 1;j <= 10; j++){
					if(i % 4 == 0){
				//		break;	//默认跳出包裹此关键字最近的一层的循环
						continue;
					}
					System.out.print(j);
				}
				System.out.println();
		}
	}
}
```
## 综合练习项目一：家庭收支记账软件
### 需求说明
[需求说明书.pdf](https://shimo.im/docs/jp3PJHPJkRGWxVXJ)

### 项目仔细实现过程
[项目一详细实现过程.pdf](https://shimo.im/docs/jp3PJHPJkRGWxVXJ)

### 步骤代码：
FamilyAccount.java

```java
class FamilyAccount{
	public static void main(String[] args){
		boolean isFlag = true;

		//用于记录用户的收入和支出的详情
		String details = "收支\t账户金额\t收支金额\t说	明\n";
		//初始金额
		int balance = 10000;

		while(isFlag){
			System.out.println("\n-----------------家庭收支记账软件-----------------\n");
            System.out.println("                   1 收支明细");
            System.out.println("                   2 登记收入");
            System.out.println("                   3 登记支出");
            System.out.println("                   4 退    出\n");
            System.out.print("                   请选择(1-4)：");

			char selection = Utility.readMenuSelection();	//接收用户的选择1-4
			switch(selection){
			
			case '1':
				System.out.println("-----------------当前收支明细记录-----------------");
				System.out.println(details);
                System.out.println("--------------------------------------------------");
                break;
			
			case '2':
		//		System.out.println("2.登记收入");
				System.out.print("本次收入金额：");
                int money = Utility.readNumber();
                System.out.print("本次收入说明：");
                String info = Utility.readString();

				//处理balances
				balance += money;
				
				//处理details
				details += "收入\t" + balance + "\t" + money + "\t" + info + "\n";				
                System.out.println("---------------------登记完成---------------------");

				break;
			
			case '3':
		//		System.out.println("3.登记支出");
				System.out.print("本次支出金额：");
                int money2 = Utility.readNumber();
                System.out.print("本次支出说明：");
                String info2 = Utility.readString();

				//处理balances
				
				if(balance >= money2){
					balance -= money2;
					
					//处理details
					details += "支出\t" + balance + "\t" + money2 + "\t" + info2 + "\n";				
				}else{
					System.out.println("支出超出账户额度，支付失败");
				}
				
                System.out.println("---------------------登记完成---------------------");

				break;
			
			case '4':
			//	System.out.println("4.退出");
				System.out.print("确认是否退出(Y/N)：");
				char isExit = Utility.readConfirmSelection();
				if(isExit == 'Y'){
					isFlag = false;
				}
				break;
			}
		}
	}
}
```
Utility工具类

```java
/**
Utility工具类：
将不同的功能封装为方法，就是可以直接通过调用方法使用它的功能，而无需考虑具体的功能实现细节。

*/
import java.util.Scanner;

class Utility {
	private static Scanner scanner = new Scanner(System.in);

	/**
	用于界面菜单的选择。该方法读取键盘，如果用户键入’1’-’4’中的任意字符，则方法返回。返回值为用户键入字符。
	*/
	public static char readMenuSelection() {
        char c;
        for (; ; ) {
            String str = readKeyBoard(1);
            c = str.charAt(0);
            if (c != '1' && c != '2' && c != '3' && c != '4') {
                System.out.print("选择错误，请重新输入：");
            } else break;
        }
        return c;
    }

	/**
	用于收入和支出金额的输入。该方法从键盘读取一个不超过4位长度的整数，并将其作为方法的返回值。
	*/
    public static int readNumber() {
        int n;
        for (; ; ) {
            String str = readKeyBoard(4);
            try {
                n = Integer.parseInt(str);
                break;
            } catch (NumberFormatException e) {
                System.out.print("数字输入错误，请重新输入：");
            }
        }
        return n;
    }

	/**
	用于收入和支出说明的输入。该方法从键盘读取一个不超过8位长度的字符串，并将其作为方法的返回值。
	*/
    public static String readString() {
        String str = readKeyBoard(8);
        return str;
    }

	/**
	用于确认选择的输入。该方法从键盘读取‘Y’或’N’，并将其作为方法的返回值。
	*/
    public static char readConfirmSelection() {
        char c;
        for (; ; ) {
            String str = readKeyBoard(1).toUpperCase();
            c = str.charAt(0);
            if (c == 'Y' || c == 'N') {
                break;
            } else {
                System.out.print("选择错误，请重新输入：");
            }
        }
        return c;
    }

	private static String readKeyBoard(int limit) {
        String line = "";

        while (scanner.hasNext()) {
            line = scanner.nextLine();
            if (line.length() < 1 || line.length() > limit) {
                System.out.print("输入长度（不大于" + limit + "）错误，请重新输入：");
                continue;
            }
            break;
        }
        return line;
    }
}
```


> 整个Java全栈系列都是笔者自己敲的笔记。写作不易，如果可以，点个赞呗！✌
