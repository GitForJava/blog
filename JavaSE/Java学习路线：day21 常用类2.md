@[TOC]
> 全部源码：https://github.com/name365/JavaSE-30Day
# 第9章Java常用类
## JDK 8之前的日期时间API(`这节给我整蒙了！！！`)

### SimpleDateFormat的使用

- Date类的API不易于国际化，大部分被废弃了，java.text.SimpleDateFormat类是一个不与语言环境有关的方式来格式化和解析日期的具体类。
- 它允许进行
  - 格式化：日期--->文本
  - 解析：文本--->日期

```java
import org.junit.Test;

import java.text.ParseException;
import java.text.SimpleDateFormat;
import java.util.Date;

/**
 * jdk 8 之前的日期时间的API测试
 * 1.System类中currentTimeMillis();
 * 2.java.util.Date和字类java.sql.Date
 * 3.SimpleDateFormat
 * 4.Calendar
 *
 * @author subei
 * @create 2020-05-10 16:13
 */
public class DateTime {
    /**
     * SimpleDateFormat的使用：SimpleDateFormat对日期Date类的格式化和解析
     * 1.两个操作
     * 1.1格式化：日期---》字符串
     * 1.2解析：格式化的逆过程，字符串---》日期
     *
     * 2.SimpleDateFormat的实例化
     */
    @Test
    public void testSimpleDateFormat() throws ParseException {
        //实例化SimpleDateFormat
        SimpleDateFormat sdf = new SimpleDateFormat();

        //格式化：日期---》字符串
        Date date = new Date();
        System.out.println(date);   //Sun May 10 16:34:30 CST 2020

        String format = sdf.format(date);
        System.out.println(format); //20-5-10 下午4:34

        //解析：格式化的逆过程，字符串---》日期
        String str = "19-12-18 上午11:43";
        Date date1 = sdf.parse(str);
        System.out.println(date1);  //Wed Dec 18 11:43:00 CST 2019

        //*************按照指定的方式格式化和解析：调用带参的构造器*****************
//        SimpleDateFormat sdf1 = new SimpleDateFormat("yyyyy.MMMMM.dd GGG hh:mm aaa");
        SimpleDateFormat sdf1 = new SimpleDateFormat("yyyyy.MMMMM.dd GGG hh:mm aaa");
        //格式化
        String format1 = sdf1.format(date);
        System.out.println(format1);    //02020.五月.10 公元 04:32 下午
        //解析:要求字符串必须是符合SimpleDateFormat识别的格式(通过构造器参数体现),
        //否则，抛异常
        Date date2 = sdf1.parse("02020.五月.10 公元 04:32 下午");
        System.out.println(date2);  //Sun May 10 16:32:00 CST 2020
    }
}
```

### SimpleDateFormat的练习

- 练习1

```java
import org.junit.Test;

import java.text.ParseException;
import java.text.SimpleDateFormat;
import java.util.Date;

/**
 * jdk 8 之前的日期时间的API测试
 * 1.System类中currentTimeMillis();
 * 2.java.util.Date和字类java.sql.Date
 * 3.SimpleDateFormat
 * 4.Calendar
 *
 * @author subei
 * @create 2020-05-10 16:13
 */
public class DateTime {

    /**
     * 练习1：字符串"2020-09-08"转换为java.sql.Date
     *
     */
    @Test
    public void testExer() throws ParseException {
        String birth = "2020-09-08";

        SimpleDateFormat sdf1 = new SimpleDateFormat("yyyy-MM-dd");
        Date date = sdf1.parse(birth);
//        System.out.println(date);

        java.sql.Date birthDate = new java.sql.Date(date.getTime());
        System.out.println(birthDate);
    }
}
```

- 练习2

```java
    /**
     * 练习二："三天打渔两天晒网"   1990-01-01  xxxx-xx-xx 打渔？晒网？
     *
     *     举例：2020-09-08 ？ 总天数
     *
     *     总天数 % 5 == 1,2,3 : 打渔
     *     总天数 % 5 == 4,0 : 晒网
     *
     *     总天数的计算？
     *     方式一：( date2.getTime() - date1.getTime()) / (1000 * 60 * 60 * 24) + 1
     *     方式二：1990-01-01  --> 2019-12-31  +  2020-01-01 -->2020-09-08
     *
     */
```

### Calendar日历类的使用

- Calendar是一个抽象基类，主用用于完成日期字段之间相互操作的功能。
- 获取Calendar实例的方法
  - 使用Calendar.getInstance()方法
  - 调用它的子类GregorianCalendar的构造器。
- 一个Calendar的实例是系统时间的抽象表示，通过get(intfield)方法来取得想要的时间信息。比如YEAR、MONTH、DAY_OF_WEEK、HOUR_OF_DAY 、MINUTE、SECOND
  - public void set(intfield,intvalue)
  - public void add(intfield,intamount)
  - public final Date getTime()
  - public final void setTime(Date date)
- 注意:
  - 获取月份时：一月是0，二月是1，以此类推，12月是11
  - 获取星期时：周日是1，周二是2，。。。。周六是7

```java
import java.util.Calendar;
import java.util.Date;

import org.junit.Test;

/**
 * jdk 8 之前的日期时间的API测试
 * 1.System类中currentTimeMillis();
 * 2.java.util.Date和字类java.sql.Date
 * 3.SimpleDateFormat
 * 4.Calendar
 *
 * @author subei
 * @create 2020-05-10 16:13
 */
public class DateTime {

    /**
     * Calendar日历类的使用
     */
    @Test
    public void testCalendar(){
        //1.实例化
        //方式一：创建其子类（GregorianCalendar）的对象
        //方式二：调用其静态方法getInstance()
        Calendar calendar = Calendar.getInstance();

//        System.out.println(calendar.getClass());    //class java.util.GregorianCalendar

        //2.常用方法
        //get()
        int days = calendar.get(Calendar.DAY_OF_MONTH);
        System.out.println(days);   //10
        System.out.println(calendar.get(Calendar.DAY_OF_YEAR)); //131,今天是这一年的131天

        //set()
        //calendar可变性
        calendar.set(Calendar.DAY_OF_MONTH,22);
        days = calendar.get(Calendar.DAY_OF_MONTH);
        System.out.println(days);   //22

        //add()
        calendar.add(Calendar.DAY_OF_MONTH,-3);
        days = calendar.get(Calendar.DAY_OF_MONTH);
        System.out.println(days);   //22-3 --》19

        //getTime():日历类---> Date
        Date date = calendar.getTime();
        System.out.println(date);   //Tue May 19 17:12:06 CST 2020

        //setTime():Date ---> 日历类
        Date date1 = new Date();
        calendar.setTime(date1);
        days = calendar.get(Calendar.DAY_OF_MONTH);
        System.out.println(days);   //10
    }
}
```

## JDK8中日期时间API的介绍

- 新日期时间API出现的背景

> 如果我们可以跟别人说：“我们在1502643933071见面，别晚了！”那么就再简单不过了。但是我们希望时间与昼夜和四季有关，于是事情就变复杂了。JDK 1.0中包含了一个java.util.Date类，但是它的大多数方法已经在JDK 1.1引入Calendar类之后被弃用了。而Calendar并不比Date好多少。它们面临的问题是：
>
>>可变性：像日期和时间这样的类应该是不可变的。
>
>> 偏移性：Date中的年份是从1900开始的，而月份都从0开始。
>
>> 格式化：格式化只对Date有用，Calendar则不行。
>
>> 此外，它们也不是线程安全的；不能处理闰秒等。
>
> 总结：对日期和时间的操作一直是Java程序员最痛苦的地方之一。

```java
import org.junit.Test;
import java.util.Date;

/**
 * jdk 8中日期时间API的测试
 *
 * @author subei
 * @create 2020-05-10 17:19
 */
public class JDK8DateTimeTest {

    @Test
    public void testDate(){
        //偏移量
        Date date1 = new Date(2020,9,8);
        System.out.println(date1);  //Fri Oct 08 00:00:00 CST 3920

        Date date2 = new Date(2020 - 1900,9 - 1,8);
        System.out.println(date2); //Tue Sep 08 00:00:00 CST 2020
    }
}
```

- 第三次引入的API是成功的，并且Java 8中引入的java.time API 已经纠正了过去的缺陷，将来很长一段时间内它都会为我们服务。
- Java 8 吸收了Joda-Time 的精华，以一个新的开始为Java 创建优秀的API。新的java.time 中包含了所有关于**本地日期（LocalDate）、本地时间（LocalTime）、本地日期时间（LocalDateTime）、时区（ZonedDateTime）和持续时间（Duration）的类**。历史悠久的Date 类新增了toInstant() 方法，用于把Date 转换成新的表示形式。这些新增的本地化时间日期API 大大简化了日期时间和本地化的管理。

```java
java.time–包含值对象的基础包
java.time.chrono–提供对不同的日历系统的访问java.time.format–格式化和解析时间和日期java.time.temporal–包括底层框架和扩展特性java.time.zone–包含时区支持的类

说明：大多数开发者只会用到基础包和format包，也可能会用到temporal包。因此，尽管有68个新的公开类型，大多数开发者，大概将只会用到其中的三分之一。
```

### LocalDate、LocalTime、LocalDateTime的使用

- LocalDate、LocalTime、LocalDateTime 类是其中较重要的几个类，它们的实例是**不可变的对象**，分别表示使用ISO-8601日历系统的日期、时间、日期和时间。它们提供了简单的本地日期或时间，并不包含当前的时间信息，也不包含与时区相关的信息。
  - LocalDate代表IOS格式（yyyy-MM-dd）的日期,可以存储生日、纪念日等日期。
  - LocalTime表示一个时间，而不是日期。
  - LocalDateTime是用来表示日期和时间的，**这是一个最常用的类之一**。

- 注：ISO-8601日历系统是国际标准化组织制定的现代公民的日期和时间的表示法，也就是公历。

```java
import org.junit.Test;

import java.time.LocalDate;
import java.time.LocalDateTime;
import java.time.LocalTime;

/**
 * jdk 8中日期时间API的测试
 *
 * @author subei
 * @create 2020-05-10 17:19
 */
public class JDK8DateTimeTest {

    /**
     * LocalDate、LocalTime、LocalDateTime的使用
     *
     */
    @Test
    public void test1(){
        //now():获取当前的日期、时间、日期+时间
        LocalDate localDate = LocalDate.now();
        LocalTime localTime = LocalTime.now();
        LocalDateTime localDateTime = LocalDateTime.now();

        System.out.println(localDate);
        System.out.println(localTime);
        System.out.println(localDateTime);

        //of():设置指定的年、月、日、时、分、秒。没有偏移量
        LocalDateTime localDateTime1 = LocalDateTime.of(2020, 10, 6, 13, 23, 43);
        System.out.println(localDateTime1);

        //getXxx()：获取相关的属性
        System.out.println(localDateTime.getDayOfMonth());
        System.out.println(localDateTime.getDayOfWeek());
        System.out.println(localDateTime.getMonth());
        System.out.println(localDateTime.getMonthValue());
        System.out.println(localDateTime.getMinute());

        //体现不可变性
        //withXxx():设置相关的属性
        LocalDate localDate1 = localDate.withDayOfMonth(22);
        System.out.println(localDate);
        System.out.println(localDate1);

        LocalDateTime localDateTime2 = localDateTime.withHour(4);
        System.out.println(localDateTime);
        System.out.println(localDateTime2);

        //不可变性
        LocalDateTime localDateTime3 = localDateTime.plusMonths(3);
        System.out.println(localDateTime);
        System.out.println(localDateTime3);

        LocalDateTime localDateTime4 = localDateTime.minusDays(6);
        System.out.println(localDateTime);
        System.out.println(localDateTime4);
    }
}
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200510201214592.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzQ2MTUzOTQ5,size_16,color_FFFFFF,t_70#pic_center)
### Instant类的使用

- Instant：时间线上的一个瞬时点。这可能被用来记录应用程序中的事件时间戳。
- 在处理时间和日期的时候，我们通常会想到年,月,日,时,分,秒。然而，这只是时间的一个模型，是面向人类的。第二种通用模型是面向机器的，或者说是连续的。在此模型中，时间线中的一个点表示为一个很大的数，这有利于计算机处理。在UNIX中，这个数从1970年开始，以秒为的单位；同样的，在Java中，也是从1970年开始，但以毫秒为单位。
- java.time包通过值类型Instant提供机器视图，不提供处理人类意义上的时间单位。Instant表示时间线上的一点，而不需要任何上下文信息，例如，时区。概念上讲，它只是简单的表示自1970年1月1日0时0分0秒（UTC）开始的秒数。因为java.time包是基于纳秒计算的，所以Instant的精度可以达到纳秒级。
- (1 ns = 10-9s)   1秒= 1000毫秒=10^6微秒=10^9纳秒
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200510201227440.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzQ2MTUzOTQ5,size_16,color_FFFFFF,t_70#pic_center)

- 时间戳是指格林威治时间1970年01月01日00时00分00秒(北京时间1970年01月01日08时00分00秒)起至现在的总秒数。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200510201243770.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzQ2MTUzOTQ5,size_16,color_FFFFFF,t_70#pic_center)

```java
import org.junit.Test;

import java.time.*;

/**
 * jdk 8中日期时间API的测试
 *
 * @author subei
 * @create 2020-05-10 17:19
 */
public class JDK8DateTimeTest {

    /**
     * Instant的使用
     */
    @Test
    public void test2(){
        //now():获取本初子午线对应的标准时间
        Instant instant = Instant.now();
        System.out.println(instant);    //2020-05-10T09:55:55.561Z

        //添加时间的偏移量
        OffsetDateTime offsetDateTime = instant.atOffset(ZoneOffset.ofHours(8));//东八区
        System.out.println(offsetDateTime); //2020-05-10T18:00:00.641+08:00

        //toEpochMilli():获取自1970年1月1日0时0分0秒（UTC）开始的毫秒数  ---> Date类的getTime()
        long milli = instant.toEpochMilli();
        System.out.println(milli);  //1589104867591

        //ofEpochMilli():通过给定的毫秒数，获取Instant实例  -->Date(long millis)
        Instant instant1 = Instant.ofEpochMilli(1550475314878L);
        System.out.println(instant1);   //2019-02-18T07:35:14.878Z
    }
}
```

### DateTimeFormatter的使用

> java.time.format.DateTimeFormatter 类：该类提供了三种格式化方法：

- 预定义的标准格式。如：**ISO_LOCAL_DATE_TIME;ISO_LOCAL_DATE;ISO_LOCAL_TIME**
- 本地化相关的格式。如：ofLocalizedDateTime(FormatStyle.LONG)
- **自定义的格式。如：ofPattern(“yyyy-MM-dd hh:mm:ss”)**

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200510201255924.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzQ2MTUzOTQ5,size_16,color_FFFFFF,t_70#pic_center)

```java
import org.junit.Test;

import java.time.*;
import java.time.format.DateTimeFormatter;
import java.time.format.FormatStyle;
import java.time.temporal.TemporalAccessor;

/**
 * jdk 8中日期时间API的测试
 *
 * @author subei
 * @create 2020-05-10 17:19
 */
public class JDK8DateTimeTest {

    /**
     * DateTimeFormatter:格式化或解析日期、时间
     *     类似于SimpleDateFormat
     */
    @Test
    public void test3(){
        //方式一：预定义的标准格式。如：ISO_LOCAL_DATE_TIME;ISO_LOCAL_DATE;ISO_LOCAL_TIME
        DateTimeFormatter formatter = DateTimeFormatter.ISO_LOCAL_DATE_TIME;
        //格式化:日期-->字符串
        LocalDateTime localDateTime = LocalDateTime.now();
        String str1 = formatter.format(localDateTime);
        System.out.println(localDateTime);
        System.out.println(str1);//2020-05-10T18:26:40.234

        //解析：字符串 -->日期
        TemporalAccessor parse = formatter.parse("2020-05-10T18:26:40.234");
        System.out.println(parse);

        //方式二：
        //本地化相关的格式。如：ofLocalizedDateTime()
        //FormatStyle.LONG / FormatStyle.MEDIUM / FormatStyle.SHORT :适用于LocalDateTime
        DateTimeFormatter formatter1 = DateTimeFormatter.ofLocalizedDateTime(FormatStyle.LONG);
        //格式化
        String str2 = formatter1.format(localDateTime);
        System.out.println(str2);//2020年5月10日 下午06时26分40秒

        //本地化相关的格式。如：ofLocalizedDate()
        //FormatStyle.FULL / FormatStyle.LONG / FormatStyle.MEDIUM / FormatStyle.SHORT : 适用于LocalDate
        DateTimeFormatter formatter2 = DateTimeFormatter.ofLocalizedDate(FormatStyle.MEDIUM);
        //格式化
        String str3 = formatter2.format(LocalDate.now());
        System.out.println(str3);//2020-5-10


       //重点： 方式三：自定义的格式。如：ofPattern(“yyyy-MM-dd hh:mm:ss”)
        DateTimeFormatter formatter3 = DateTimeFormatter.ofPattern("yyyy-MM-dd hh:mm:ss");
        //格式化
        String str4 = formatter3.format(LocalDateTime.now());
        System.out.println(str4);//2020-05-10 06:26:40

        //解析
        TemporalAccessor accessor = formatter3.parse("2020-05-10 06:26:40");
        System.out.println(accessor);

    }
}
```

### 其它日期时间相关API的使用

- ZoneId：该类中包含了所有的时区信息，一个时区的ID，如Europe/Paris
- ZonedDateTime：一个在ISO-8601日历系统时区的日期时间，如2007-12-03T10:15:30+01:00Europe/Paris。
  - 其中每个时区都对应着ID，地区ID都为“{区域}/{城市}”的格式，例如：Asia/Shanghai等

```java
import org.junit.Test;

import java.time.*;
import java.util.Set;

/**
 * jdk 8中日期时间API的测试
 *
 * @author subei
 * @create 2020-05-10 17:19
 */
public class JDK8DateTimeTest {
	
	@Test
	public void test1(){
		//ZoneId:类中包含了所有的时区信息
		// ZoneId的getAvailableZoneIds():获取所有的ZoneId
		Set<String> zoneIds= ZoneId.getAvailableZoneIds();
		for(String s: zoneIds) {
			System.out.println(s);
		}
		// ZoneId的of():获取指定时区的时间
		LocalDateTime localDateTime= LocalDateTime.now(ZoneId.of("Asia/Tokyo"));
		System.out.println(localDateTime);
		
		//ZonedDateTime:带时区的日期时间
		// ZonedDateTime的now():获取本时区的ZonedDateTime对象
		ZonedDateTime zonedDateTime= ZonedDateTime.now();
		System.out.println(zonedDateTime);
		// ZonedDateTime的now(ZoneId id):获取指定时区的ZonedDateTime对象
		ZonedDateTime zonedDateTime1= ZonedDateTime.now(ZoneId.of("Asia/Tokyo"));
		System.out.println(zonedDateTime1);
	}
}
```

- Clock：使用时区提供对当前即时、日期和时间的访问的时钟。
- 持续时间：Duration，用于计算两个“时间”间隔
- 日期间隔：Period，用于计算两个“日期”间隔
- TemporalAdjuster : 时间校正器。有时我们可能需要获取例如：将日期调整到“下一个工作日”等操作。
- TemporalAdjusters : 该类通过静态方法(firstDayOfXxx()/lastDayOfXxx()/nextXxx())提供了大量的常用TemporalAdjuster 的实现。

```java
import java.time.Duration;
import java.time.LocalDateTime;
import java.time.LocalTime;

import org.junit.Test;

public class JDK8APITest {
	
	@Test
	public void test2(){
		//Duration:用于计算两个“时间”间隔，以秒和纳秒为基准
		LocalTime localTime= LocalTime.now();
		LocalTime localTime1= LocalTime.of(15, 23, 32);
		//between():静态方法，返回Duration对象，表示两个时间的间隔
		Duration duration= Duration.between(localTime1, localTime);
		System.out.println(duration);
		
		System.out.println(duration.getSeconds());
		System.out.println(duration.getNano());
		
		LocalDateTime localDateTime= LocalDateTime.of(2016, 6, 12, 15, 23, 32);
		LocalDateTime localDateTime1= LocalDateTime.of(2017, 6, 12, 15, 23, 32);
		
		Duration duration1= Duration.between(localDateTime1, localDateTime);
		System.out.println(duration1.toDays());
	}
}
```

```java
import java.time.Period;
import org.junit.Test;

public class JDK8APITest {
	
	@Test
	public void test3(){
		//Period:用于计算两个“日期”间隔，以年、月、日衡量
		LocalDate localDate= LocalDate.now();
		LocalDate localDate1= LocalDate.of(2028, 3, 18);
		
		Period period= Period.between(localDate, localDate1);
		System.out.println(period);System.out.println(period.getYears());
		
		System.out.println(period.getMonths());
		System.out.println(period.getDays());
		
		Period period1= period.withYears(2);
		System.out.println(period1);
	}
}
```

#### 参考：与传统日期处理的转换
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200510201318692.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzQ2MTUzOTQ5,size_16,color_FFFFFF,t_70#pic_center)
## Java比较器

### 概述

> ```java
> /**
> * 一、说明：Java中的对象，正常情况下，只能进行比较：==  或  != 。不能使用 > 或 < 的
> *          但是在开发场景中，我们需要对多个对象进行排序，言外之意，就需要比较对象的大小。
> *          如何实现？使用两个接口中的任何一个：Comparable 或 Comparator
> */
> ```

- Java实现对象排序的方式有两种：
  - 自然排序：java.lang.Comparable
  - 定制排序：java.util.Comparator

### Comparable自然排序举例

```java
import org.junit.Test;
import java.util.Arrays;

public class CompareTest {

    /**
     * Comparable接口的使用举例：  自然排序
     * 1.像String、包装类等实现了Comparable接口，重写了compareTo(obj)方法，给出了比较两个对象大小的方式。
     * 2.像String、包装类重写compareTo()方法以后，进行了从小到大的排列
     * 3. 重写compareTo(obj)的规则：
     *    如果当前对象this大于形参对象obj，则返回正整数，
     *    如果当前对象this小于形参对象obj，则返回负整数，
     *    如果当前对象this等于形参对象obj，则返回零。
     *
     */
    @Test
    public void test1(){
        String[] arr = new String[]{"AA","CC","KK","MM","GG","JJ","DD"};

        Arrays.sort(arr);

        System.out.println(Arrays.toString(arr));
    }

}
```

### 自定义类实现Comparable自然排序

```java
import org.junit.Test;
import java.util.Arrays;

public class CompareTest {

    /**
     * 4.对于自定义类来说，如果需要排序，我们可以让自定义类实现Comparable接口，重写compareTo(obj)方法。
     *   在compareTo(obj)方法中指明如何排序
     */
    @Test
    public void test2(){
        Goods[] arr = new Goods[5];
        arr[0] = new Goods("lenovoMouse",34);
        arr[1] = new Goods("dellMouse",43);
        arr[2] = new Goods("xiaomiMouse",12);
        arr[3] = new Goods("huaweiMouse",65);
        arr[4] = new Goods("microsoftMouse",43);

        Arrays.sort(arr);

        System.out.println(Arrays.toString(arr));
    }

}
```

- Goods类

```java
/**
 * 商品类
 *
 * @author subei
 * @create 2020-05-10 19:20
 */
public class Goods implements Comparable{

    private String name;
    private double price;

    public Goods() {
    }

    public Goods(String name, double price) {
        this.name = name;
        this.price = price;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public double getPrice() {
        return price;
    }

    public void setPrice(double price) {
        this.price = price;
    }

    @Override
    public String toString() {
        return "Goods{" +
                "name='" + name + '\'' +
                ", price=" + price +
                '}';
    }

    //指明商品比较大小的方式:按照价格从低到高排序,再按照产品名称从高到低排序
    @Override
    public int compareTo(Object o) {
//        System.out.println("**************");
        if(o instanceof Goods){
            Goods goods = (Goods)o;
            //方式一：
            if(this.price > goods.price){
                return 1;
            }else if(this.price < goods.price){
                return -1;
            }else{
//                return 0;
                return -this.name.compareTo(goods.name);
            }
            //方式二：
//           return Double.compare(this.price,goods.price);
        }
//        return 0;
        throw new RuntimeException("传入的数据类型不一致！");
    }
}
```

### 使用Comparator实现定制排序

```java
import org.junit.Test;
import java.util.Arrays;
import java.util.Comparator;

/**
 * 一、说明：Java中的对象，正常情况下，只能进行比较：==  或  != 。不能使用 > 或 < 的
 *          但是在开发场景中，我们需要对多个对象进行排序，言外之意，就需要比较对象的大小。
 *          如何实现？使用两个接口中的任何一个：Comparable 或 Comparator
 *
 * 二、Comparable接口与Comparator的使用的对比：
 *    Comparable接口的方式一旦一定，保证Comparable接口实现类的对象在任何位置都可以比较大小。
 *    Comparator接口属于临时性的比较。
 *
 * @author subei
 * @create 2020-05-10 19:11
 */
public class CompareTest {

    /**
     * Comparator接口的使用：定制排序
     *     1.背景：
     *     当元素的类型没有实现java.lang.Comparable接口而又不方便修改代码，
     *     或者实现了java.lang.Comparable接口的排序规则不适合当前的操作，
     *     那么可以考虑使用 Comparator 的对象来排序
     *     2.重写compare(Object o1,Object o2)方法，比较o1和o2的大小：
     *     如果方法返回正整数，则表示o1大于o2；
     *     如果返回0，表示相等；
     *     返回负整数，表示o1小于o2。
     */
    @Test
    public void test3(){
        String[] arr = new String[]{"AA","CC","KK","MM","GG","JJ","DD"};
        Arrays.sort(arr,new Comparator(){

            //按照字符串从大到小的顺序排列
            @Override
            public int compare(Object o1, Object o2) {
                if(o1 instanceof String && o2 instanceof  String){
                    String s1 = (String) o1;
                    String s2 = (String) o2;
                    return -s1.compareTo(s2);
                }
//                return 0;
                throw new RuntimeException("输入的数据类型不一致");
            }
        });
        System.out.println(Arrays.toString(arr));
    }

    @Test
    public void test4(){
        Goods[] arr = new Goods[6];
        arr[0] = new Goods("lenovoMouse",34);
        arr[1] = new Goods("dellMouse",43);
        arr[2] = new Goods("xiaomiMouse",12);
        arr[3] = new Goods("huaweiMouse",65);
        arr[4] = new Goods("huaweiMouse",224);
        arr[5] = new Goods("microsoftMouse",43);

        Arrays.sort(arr, new Comparator() {
            //指明商品比较大小的方式:按照产品名称从低到高排序,再按照价格从高到低排序
            @Override
            public int compare(Object o1, Object o2) {
                if(o1 instanceof Goods && o2 instanceof Goods){
                    Goods g1 = (Goods)o1;
                    Goods g2 = (Goods)o2;
                    if(g1.getName().equals(g2.getName())){
                        return -Double.compare(g1.getPrice(),g2.getPrice());
                    }else{
                        return g1.getName().compareTo(g2.getName());
                    }
                }
                throw new RuntimeException("输入的数据类型不一致");
            }
        });

        System.out.println(Arrays.toString(arr));
    }

```

-  **二、Comparable接口与Comparator的使用的对比**：
  -  Comparable接口的方式一旦一定，保证Comparable接口实现类的对象在任何位置都可以比较大小。
  -  Comparator接口属于临时性的比较。


## System类、Math类、BigInteger与BigDecimal

### System类

- System类代表系统，系统级的很多属性和控制方法都放置在该类的内部。该类位于java.lang包。
- 由于该类的构造器是private的，所以无法创建该类的对象，也就是无法实例化该类。其内部的成员变量和成员方法都是static的，所以也可以很方便的进行调用。

- 成员变量

  - System类内部包含in、out和err三个成员变量，分别代表标准输入流(键盘输入)，标准输出流(显示器)和标准错误输出流(显示器)。

- 成员方法

  - native long currentTimeMillis()：

    > 该方法的作用是返回当前的计算机时间，时间的表达格式为当前计算机时间和GMT时间(格林威治时间)1970年1月1号0时0分0秒所差的毫秒数。

  - void exit(int status)：

    > 该方法的作用是退出程序。其中status的值为0代表正常退出，非零代表异常退出。使用该方法可以在图形界面编程中实现程序的退出功能等。

  - void gc()：

    > 该方法的作用是请求系统进行垃圾回收。至于系统是否立刻回收，则取决于系统中垃圾回收算法的实现以及系统执行时的情况。String 

  - getProperty(String key)：

    > 该方法的作用是获得系统中属性名为key的属性对应的值。系统中常见的属性名以及属性的作用如下表所示：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200510201347258.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzQ2MTUzOTQ5,size_16,color_FFFFFF,t_70#pic_center)

```java
import org.junit.Test;

/**
 * 其他常用类的使用
 * 1.System
 * 2.Math
 * 3.BigInteger 和 BigDecimal
 *
 * @author subei
 * @create 2020-05-10 19:43
 */
public class OtherClassTest {

    @Test
    public void test1() {
        String javaVersion = System.getProperty("java.version");
        System.out.println("java的version:" + javaVersion);

        String javaHome = System.getProperty("java.home");
        System.out.println("java的home:" + javaHome);

        String osName = System.getProperty("os.name");
        System.out.println("os的name:" + osName);

        String osVersion = System.getProperty("os.version");
        System.out.println("os的version:" + osVersion);

        String userName = System.getProperty("user.name");
        System.out.println("user的name:" + userName);

        String userHome = System.getProperty("user.home");
        System.out.println("user的home:" + userHome);

        String userDir = System.getProperty("user.dir");
        System.out.println("user的dir:" + userDir);

    }
}
```

### Math类

> java.lang.Math提供了一系列静态方法用于科学计算。其方法的参数和返回值类型一般为double型。

> abs     绝对值
>
> acos,asin,atan,cos,sin,tan  三角函数
>
> sqrt     平方根
>
> pow(double a,doble b)     a的b次幂
>
> log    自然对数
>
> exp    e为底指数
>
> max(double a,double b)
>
> min(double a,double b)
>
> random()      返回0.0到1.0的随机数
>
> long round(double a)     double型数据a转换为long型（四舍五入）
>
> toDegrees(double angrad)     弧度—>角度
>
> toRadians(double angdeg)     角度—>弧度

### BigInteger与BigDecimal

- Integer类作为int的包装类，能存储的最大整型值为2^31 -1，Long类也是有限的，最大为2^63 -1。如果要表示再大的整数，不管是基本数据类型还是他们的包装类都无能为力，更不用说进行运算了。
- java.math包的BigInteger可以表示不可变的任意精度的整数。BigInteger 提供所有Java 的基本整数操作符的对应物，并提供java.lang.Math 的所有相关方法。另外，BigInteger 还提供以下运算：模算术、GCD 计算、质数测试、素数生成、位操作以及一些其他操作。
- 构造器
  - BigInteger(String val)：根据字符串构建BigInteger对象

- 常用方法

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200510201540148.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzQ2MTUzOTQ5,size_16,color_FFFFFF,t_70#pic_center)

- 一般的Float类和Double类可以用来做科学计算或工程计算，但**在商业计算中，要求数字精度比较高，故用到java.math.BigDecimal类**。
- BigDecimal类支持不可变的、任意精度的有符号十进制定点数。
- 构造器
  - public BigDecimal(double val)
  - public BigDecimal(String val)
- 常用方法
  - public BigDecimal add(BigDecimal augend)
  - public BigDecimal subtract(BigDecimal subtrahend)
  - public BigDecimal multiply(BigDecimal multiplicand)
  - public BigDecimal divide(BigDecimal divisor, int scale, int roundingMode)

```java
import org.junit.Test;

import java.math.BigDecimal;
import java.math.BigInteger;

/**
 * 其他常用类的使用
 * 1.System
 * 2.Math
 * 3.BigInteger 和 BigDecimal
 *
 * @author subei
 * @create 2020-05-10 19:43
 */
public class OtherClassTest {

    @Test
    public void test2() {
        BigInteger bi = new BigInteger("1243324112234324324325235245346567657653");
        BigDecimal bd = new BigDecimal("12435.351");
        BigDecimal bd2 = new BigDecimal("11");
        System.out.println(bi);
//         System.out.println(bd.divide(bd2));
        System.out.println(bd.divide(bd2, BigDecimal.ROUND_HALF_UP));
        System.out.println(bd.divide(bd2, 25, BigDecimal.ROUND_HALF_UP));

    }
}
```
  > 整个Java全栈系列都是笔者自己敲的笔记。写作不易，如果可以，点个赞呗！✌
