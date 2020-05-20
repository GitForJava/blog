[TOC]
> 原文：https://shimo.im/docs/jp3PJHPJkRGWxVXJ/ 《第2章Java基本语法(下)：程序流程控制》
# 第2章Java基本语法(下)：程序流程控制
## 2.5  程序流程控制
### 2.5.2 分支语句1：if-else结构
![图片](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91cGxvYWRlci5zaGltby5pbS9mL3BqS2FwakRuWDBnQ2lUZUQucG5nIXRodW1ibmFpbA?x-oss-process=image/format,png)

![图片](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91cGxvYWRlci5zaGltby5pbS9mL1JPZmNjQ3l5NExja2pxZVIucG5nIXRodW1ibmFpbA?x-oss-process=image/format,png)

if-else使用说明：

* 条件表达式必须是布尔表达式（关系表达式或逻辑表达式）、布尔变量；
* 语句块只有一条执行语句时，一对{}可以省略，但建议保留；
* if-else语句结构，根据需要可以嵌套使用；
* 当if-else结构是“多选一”时，最后的else是可选的，根据需要可以省略；
* 当多个条件是“互斥”关系时，条件判断语句及执行语句间顺序无所谓当多个条件是“包含”关系时，“小上大下/ 子上父下”。

练习

```
/*
分支结构中的if-else（条件判断结构）
一、三种结构
第一种：
if(条件表达式){
	执行表达式
}
第二种：
if(条件表达式){
	执行表达式1
}else{
	执行表达式2
}
第三种：
if(条件表达式){
	执行表达式1
}else if{
	执行表达式2
}else if(条件表达式){
	执行表达式3
}
...
else{
	执行表达式n
}

*/
class IfTest{
	public static void main(String[] args){
		//举例1
		int heartBeats = 75;
		if(heartBeats < 60 || heartBeats > 100){
			System.out.println("需要进一步做检查");
		}
		System.out.println("检查结束");

		//举例2
		int age = 23;
		if(age < 18){
			System.out.println("你还可以看动画片");
		}else{
			System.out.println("你可以看科技电影了");
		}

		//举例3
		if(age < 0){
			System.out.println("你输入的数据不合适");
		}else if(age < 18){
			System.out.println("你还是个青少年");
		}else if(age < 35){
			System.out.println("你还是个青壮年");
		}else if(age < 60){
			System.out.println("你还是个中年");
		}else if(age < 120){
			System.out.println("你进入老年了");
		}else{
			System.out.println("你成仙了");
		}
	}
}
```
### 输入语句
```
/*
如何从键盘获取不同类型的变量，需要使用Scanner类

具体步骤：
1.导包：import java.util.Scanner;
2.Scanner的实例化;
3.调用Scanner类的相关方法，来获取指定的变量。
*/
import java.util.Scanner;

class IFTest{
	public static void main(String[] args){
		//声明一个Scanner
		Scanner scan = new Scanner(System.in);

		int num = scan.nextInt();

		System.out.println(num);
	}
}
```
```
/*
如何从键盘获取不同类型的变量，需要使用Scanner类

具体步骤：
1.导包：import java.util.Scanner;
2.Scanner的实例化;
3.调用Scanner类的相关方法，来获取指定的变量。
*/
import java.util.Scanner;

class IFTest{
	public static void main(String[] args){
		//Scanner实例化
		Scanner scan = new Scanner(System.in);

		System.out.println("请输入你的姓名：");
		String name = scan.next();
		System.out.println(name);

		System.out.println("请输入你的年龄：");
		int age = scan.nextInt();
		System.out.println(age);

		System.out.println("请输入你的体重：");
		double weight = scan.nextDouble();
		System.out.println(weight);

		System.out.println("你是否单身？(true/false)");
		boolean isLive = scan.nextBoolean();
		System.out.println(isLive);

		//char型的获取，Scanner没有提供相关方法，只能获取一个字符串
		System.out.println("请输入你的性别：(男/女)");
		String TF = scan.next();
		char TFChar = TF.charAt(0);
		System.out.println(TFChar);
	}
}
```
练习1
```
/*
岳小鹏参加Java考试，他和父亲岳不群达成承诺：
如果：成绩为100分时，奖励一辆BMW；
成绩为(80，99]时，奖励一台iphone xs max；
当成绩为[60,80]时，奖励一个iPad；
其它时，什么奖励也没有。
请从键盘输入岳小鹏的期末成绩，并加以判断

说明：
1.else结构是可选的。
2.针对于条件表达式：
	① 如果多个条件表达式之间的关系是“互斥”关系(或没有交集的关系),哪个判断和执行语句声明在上面还是下面，无所谓；
	② 如果多个条件表达式之间是有交集的关系，需要根据实际情况，需要考虑实际情况，考虑清楚应该将哪个结构声明在上面。
	③ 如果多个条件表达式之间有包含的关系，通常情况下，需要将范围小的声明在范围大的上面。否则，范围小的就没机会运行。
*/
import java.util.Scanner;
class IFTest02{
	public static void main(String[] args){
		Scanner scan = new Scanner(System.in);
		System.out.println("请输入岳小鹏的成绩：");
		int score = scan.nextInt();

		if(score == 100){
			System.out.println("奖励一辆BMW");
		}else if(score >80 && score <=99){
			System.out.println("奖励一台iphone xs max");
		}else if(score >= 60 && score <= 80){
			System.out.println("奖励一个iPad");
		}else{
			System.out.println("奖励？学习去！！！");
		}
	}
}
```
练习2
```
/*
编写程序：由键盘输入三个整数分别存入变量num1、num2、num3，
对它们进行排序(使用if-else if-else),并且从小到大输出。

*/
import java.util.Scanner;

class Sorting{
	public static void main(String[] args){
		//Scanner实例化
		Scanner scan = new Scanner(System.in);
		System.out.println("请输入第一个整数：");
		int num1 = scan.nextInt();
		System.out.println("请输入第二个整数：");
		int num2 = scan.nextInt();
		System.out.println("请输入第三个整数：");
		int num3 = scan.nextInt();

		int MaxNumber = 0;
		if(num1 >= num2 ){
			if(num3 >= num1){
				System.out.println(num2 + "," + num1 + "," + num3);
			}else if(num3 <= num2){
				System.out.println(num3 + "," + num2 + "," + num1);
			}else{
				System.out.println(num2 + "," + num3 + "," + num1);
			}
		}else{
			if(num3 >= num2){
				System.out.println(num1 + "," + num2 + "," + num3);
			}else if(num3 <= num1){
				System.out.println(num3 + "," + num1 + "," + num2);
			}else{
				System.out.println(num1 + "," + num3 + "," + num2);
			}
		}
	}
}
```
练习3
```
/*
我家的狗5岁了，5岁的狗相当于人类多大呢？
其实，狗的前两年每一年相当于人类的10.5岁，之后每增加一年就增加四岁。
那么5岁的狗相当于人类多少年龄呢？应该是：10.5 + 10.5 + 4 + 4 + 4 = 33岁。
如果用户输入负数，请显示一个提示信息。

*/
import java.util.Scanner;

class DogYear{
	public static void main(String[] args) {
		Scanner scan = new Scanner(System.in);
		System.out.println("请输入狗的年龄：");
		double Dyear = scan.nextDouble();
		if(Dyear <= 2 &&  Dyear > 0){
			System.out.println("狗的年龄等同于人的：" + Dyear * 10.5);
		}else if(Dyear <= 0){
			System.out.println("你输入的不正确。");
		}else{
			double number = 2 * 10.5 + (Dyear - 2) * 4;
			System.out.println("狗的年龄等同于人的：" + number);
		}		
	}
}
```
练习4
```
/*
假设你想开发一个玩彩票的游戏，程序随机地产生一个两位数的彩票，
提示用户输入一个两位数，然后按照下面的规则判定用户是否能赢。
1)如果用户输入的数匹配彩票的实际顺序，奖金10 000美元。
2)如果用户输入的所有数字匹配彩票的所有数字，但顺序不一致，奖金3 000美元。
3)如果用户输入的一个数字仅满足顺序情况下匹配彩票的一个数字，奖金1 000美元。
4)如果用户输入的一个数字仅满足非顺序情况下匹配彩票的一个数字，奖金500美元。
5)如果用户输入的数字没有匹配任何一个数字，则彩票作废。
提示：使用(int)(Math.random() * 90  + 10)产生随机数。
Math.random() : [0,1)  * 90 [0,90) + 10 [10,100)[10,99]

*/
import java.util.Scanner;

class CaiTest{
	public static void main(String[] args){
		//1、随机产生一个两位数
		//System.out.println(Math.random());//产生[0,1)
		int number = (int)(Math.random()*90 + 10);//得到[10,99]，即[10,100)
		//System.out.println(number);
		
		int numberShi = number/10;
		int numberGe = number%10;
		
		//2、用户输入一个两位数
		Scanner input = new Scanner(System.in);
		System.out.print("请输入一个两位数：");
		int guess = input.nextInt();
		
		int guessShi = guess/10;
		int guessGe = guess%10;
		
		if(number == guess){
			System.out.println("奖金10 000美元");
		}else if(numberShi == guessGe && numberGe == guessShi){
			System.out.println("奖金3 000美元");
		}else if(numberShi==guessShi || numberGe == guessGe){
			System.out.println("奖金1 000美元");
		}else if(numberShi==guessGe || numberGe == guessShi){
			System.out.println("奖金500美元");
		}else{
			System.out.println("没中奖");
		}
		
		System.out.println("中奖号码是：" + number);
	}
}
```
练习5
```
/*
大家都知道，男大当婚，女大当嫁。
那么女方家长要嫁女儿，当然要提出一定的条件：高：180cm以上；
富：财富1千万以上；帅：是。如果这三个条件同时满足，则：“我一定要嫁给他!!!”
如果三个条件有为真的情况，则：“嫁吧，比上不足，比下有余。”
如果三个条件都不满足，则：“不嫁！”

*/
import java.util.Scanner;

class GaoFuTest{
	public static void main(String[] args){
		Scanner scan = new Scanner(System.in);

		System.out.println("请输入你的身高：(cm)");
		int height = scan.nextInt();
		System.out.println("请输入你的财富：(千万)");
		double weight = scan.nextDouble();
//		System.out.println("请输入你是否帅：(true/false)");
//		boolean isHandSome = scan.nextBoolean();

//		if(height >= 180 && weight >= 1 && isHandSome){
//			System.out.println("我一定要嫁给他!!!");
//		}else if(height >= 180 || weight >= 1 || isHandSome){
//			System.out.println("嫁吧，比上不足，比下有余。");
//		}else{
//			System.out.println("不嫁！");
//		}

		//方式二
		System.out.println("请输入你是否帅: (是or否)");
		String isHandsome = scan.next();

		if(height >= 100 && weight >= 1 && isHandsome.equals("是")){
			System.out.println("我一定要嫁给他!!!");
		}else if(height >= 180 || weight >= 1 || isHandsome.equals("是")){
			System.out.println("嫁吧，比上不足，比下有余。");
		}else{
			System.out.println("不嫁！");
		}
	}
}
```
### 2.5.3 分支语句2：switch-case结构
![图片](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91cGxvYWRlci5zaGltby5pbS9mL0lRU2JTbGRISm9ZNkZUMkQucG5nIXRodW1ibmFpbA?x-oss-process=image/format,png)

```
/*
分支结构之二：switch-case

1.格式
switch(表达式){
case 常量1:
	执行语句1;
	//break;
case 常量2:
	执行语句2;
	//break;

...

default:
	执行语句n:
	//break;
}

2.说明:
① 根据switch表达式中的值，依次匹配各个case中的常量。一旦匹配成功，进入相应case结构中，执行相关语句。
  当调用完执行语句后，则仍然继续向下执行其他case语句，直到遇到break关键字或末尾结束为止。

② break, 可以使用switch-case结构中，表示一旦执行到此关键字，就跳出switch-case结构。

③ switch结构中的表达式，只能是如下的六种数据类型之一：byte、short、char、int、枚举类型(JDK5.0)、String类型(JDK7.0)
④ case 之后之能声明常量。不能声明范围。

⑤ break关键字是可选的。
⑥ default：相当于if-else结构中的else。
			default 结构是可选的，而且位置是灵活的。
*/

class SwitchTest{
	public static void main(String[] args){

		int number = 2;
		switch(number){
		case 0:
			System.out.println("zero");
			break;
		case 1:
			System.out.println("one");
			break;
		case 2:
			System.out.println("twe");
			break;
		case 3:
			System.out.println("three");
			break;
		default:
			System.out.println("other");
			break;
		}

		//*********************************
		//运行报错，不能运行boolean类型
/*		boolean isHandSome = true;
		switch(isHandSome){
		case true:
			System.out.println("可乐吗？？");
			break;
		case false:
			System.out.println("薯条吗？？");
			break;
		default:
			System.out.println("输入有误！！！");
		}
*/
		//*********************************
		String season= "summer";
		switch(season) {
		case"spring":
			System.out.println("春暖花开");
			break;
		case"summer":
			System.out.println("夏日炎炎");
			break;
		case"autumn":
			System.out.println("秋高气爽");
			break;
		case"winter":
			System.out.println("冬雪皑皑");
			break;
		default:
			System.out.println("季节输入有误");
			break;
		}

		//**************************************
		//运行报错
/*		int age = 10;
		switch(age){			
		case age > 18:
			System.out.println("成年了");
			break;
		default:
			System.out.println("未成年");
		}	*/
	}
}
```
练习1
```
/*
使用switch 把小写类型的char型转为大写。只转换a, b, c, d, e. 其它的输出“other”。
提示：String word = scan.next();  char c = word.charAt(0); switch(c){}
*/
import java.util.Scanner;
class  SwitchCaseTest1{
	public static void main(String[] args) {
		Scanner scan = new Scanner(System.in);
		String word = scan.next();  
		char c = word.charAt(0); 
		switch(c){
		case 'a':
			System.out.println("A");
			break;
		case 'b':
			System.out.println("B");
			break;
		case 'c':
			System.out.println("C");
			break;
		case 'd':
			System.out.println("D");
			break;
		case 'e':
			System.out.println("E");
			break;
		default:
			System.out.println("other");
		}
	}
}
```
练习2
```
/*
对学生成绩大于60分的，输出“合格”。低于60分的，输出“不合格”。

说明：如果switch-case语句中多个相同语句，可以进行合并。
*/
class  SwitchTest1{
	public static void main(String[] args){
		int score = 78;
		//方案一
		switch(score / 10){
		case 0:
		case 1:
		case 2:
		case 3:
		case 4:
		case 5:
			System.out.println("不合格");
			break;
		case 6:
		case 7:
		case 8:
		case 9:
		case 10:
			System.out.println("合格");
			break;
		}

		//更优的解法
		switch(score /60){
		case 0:
			System.out.println("不及格");
			break;
		case 1:
			System.out.println("合格");
			break;
		}
	}
}
```
练习3
```
/*
根据用于指定月份，打印该月份所属的季节。
3,4,5 春季6,7,8 夏季9,10,11 秋季12, 1, 2 冬季

*/
class MonthTest{
	public static void main(String[] args){
		int month = 6;
		switch(month){
		case 12:
		case 1:
		case 2:
			System.out.println("冬季");
			break;
		case 3:
		case 4:
		case 5:
			System.out.println("春季");
			break;
		case 6:
		case 7:
		case 8:
			System.out.println("夏季");
			break;
		case 9:
		case 10:
		case 11:
			System.out.println("秋季");
			break;
		}
	}
}
```
练习4
```
/*
编写程序：从键盘上输入2020年的“month”和“day”，
要求通过程序输出输入的日期为2019年的第几天。
2 15 : 31 + 15

5 7: 31 + 28 +31 +30 + 7
...
说明：break在switch-case中是可选的。
*/
import java.util.Scanner;
class DayTest{
	public static void main(String[] args) {
		Scanner scan = new Scanner(System.in);
		System.out.println("请输入2020年的month");
		int month = scan.nextInt();
		System.out.println("请输入2020年的day");
		int day = scan.nextInt();

		//定义一个变量来保存天数
		int sumDays = 0;
		switch(month){
		case 12:
			sumDays += 30;
		case 11:
			sumDays += 31;
		case 10:
			sumDays += 30;
		case 9:
			sumDays += 31;
		case 8:
			sumDays += 31;
		case 7:
			sumDays += 30;
		case 6:
			sumDays += 31;
		case 5:
			sumDays += 30;
		case 4:
			sumDays += 31;
		case 3:
			sumDays += 29;
		case 2:
			sumDays += 31;
		case 1:
			sumDays += day;
		}

		System.out.println("2020年" + month + "月" + day + "日是当年的第" + sumDays + "天");
	}
}
```
练习5
```
/*
从键盘分别输入年、月、日，判断这一天是当年的第几天注：判断一年是否是闰年的标准：
1）可以被4整除，但不可被100整除或
2）可以被400整除

说明:
1凡是可以使用switch-case的结构,都可以转换为if-else。反之,不成立。
2.我们写分支结构时,当发现既可以使用switch-case,〔(同时,switch中表达式的取值情况不太多),
又可以使用，我们优先选择使用switch-case。原因:switch-case执行效率稍高。

*/
import java.util.Scanner;
class YearDayTest{
	public static void main(String[] args) {
		Scanner scan = new Scanner(System.in);
		System.out.println("请输入year");
		int year = scan.nextInt();
		System.out.println("请输入month");
		int month = scan.nextInt();
		System.out.println("请输入day");
		int day = scan.nextInt();

		//定义一个变量来保存天数
		int sumDays = 0;
		switch(month){
		case 12:
			sumDays += 30;
		case 11:
			sumDays += 31;
		case 10:
			sumDays += 30;
		case 9:
			sumDays += 31;
		case 8:
			sumDays += 31;
		case 7:
			sumDays += 30;
		case 6:
			sumDays += 31;
		case 5:
			sumDays += 30;
		case 4:
			sumDays += 31;
		case 3:
			//判断是否为闰年
			if((year % 4 == 0 && year % 100 != 0) || year %400 == 0){
				sumDays += 29;
			}else{
				sumDays += 28;
			}
		case 2:
			sumDays += 31;
		case 1:
			sumDays += day;
		}

		System.out.println(year + "年" + month + "月" + day + "日是当年的第" + sumDays + "天");
	}
}
```
练习六
```
/*
编写一个程序，为一个给定的年份找出其对应的中国生肖。
中国的生肖基于12年一个周期，每年用一个动物代表：
rat、ox、tiger、rabbit、dragon、snake、horse、sheep、monkey、rooster、dog、pig。
提示：2019年：猪2019 % 12 == 3
*/
import java.util.Scanner;
class ZodiacSignTest{
	public static void main(String[] args){
		Scanner scan = new Scanner(System.in);
		System.out.println("请输入年份：");
		int year = scan.nextInt();
		switch (year % 12){
		case 1:
			System.out.println("rooster");
			break;
		case 2:
			System.out.println("dog");
			break;
		case 3:
			System.out.println("pig");
			break;
		case 4:
			System.out.println("rat");
			break;
		case 5:
			System.out.println("ox");
			break;
		case 6:
			System.out.println("tiger");
			break;
		case 7:
			System.out.println("rabbit");
			break;
		case 8:
			System.out.println("dragon");
			break;
		case 9:
			System.out.println("snake");
			break;
		case 10:
			System.out.println("horse");
			break;
		case 11:
			System.out.println("sheep");
			break;
		case 12:
			System.out.println("monkey");
			break;
		}
	}
}
```
> 整个Java全栈系列都是笔者自己敲的笔记。写作不易，如果可以，点个赞呗！✌

