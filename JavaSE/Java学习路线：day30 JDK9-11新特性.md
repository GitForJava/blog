[TOC]

# 第17章 Java9&Java10&Java11新特性

## Java 9 的新特性

### JDK 9 的发布

- 经过4次跳票，历经曲折的Java 9 终于终于在2017年9月21日发布。
- 从Java 9 这个版本开始，Java 的计划发布周期是6 个月，下一个Java 的主版本将于2018 年3 月发布，命名为Java 18.3，紧接着再过六个月将发布Java 18.9。
- 这意味着Java的更新从传统的以特性驱动的发布周期，转变为以时间驱动的（6 个月为周期）发布模式，并逐步的将Oracle JDK 原商业特性进行开源。
- 针对企业客户的需求，Oracle 将以三年为周期发布长期支持版本（long term support）。
- Java 9 提供了超过150项新功能特性，包括备受期待的模块化系统、可交互的REPL 工具：jshell，JDK 编译工具，Java 公共API 和私有代码，以及安全增强、扩展提升、性能管理改善等。可以说Java 9是一个庞大的系统工程，完全做了一个整体改变。

### jdk目录结构的改变

![](F:\MyNut\我的坚果云\JavaSE\img\JDK9-11\Java9.jpg)

- 官方提供的新特性列表：https://docs.oracle.com/javase/9/whatsnew/toc.htm#JSNEW-GUID-C23AFD78-C777-460B-8ACE-58BE5EA681F6
- 或参考OpenJDKhttp://openjdk.java.net/projects/jdk9/
- 在线OracleJDK9Documentationhttps://docs.oracle.com/javase/9/

![JDK8](F:\MyNut\我的坚果云\JavaSE\img\JDK9-11\JDK8.jpg)

|   bin 目录   |      包含命令行开发和调试工具，如javac，jar和javadoc。       |
| :----------: | :----------------------------------------------------------: |
| include目录  |            包含在编译本地代码时使用的C/C++头文件             |
|   lib 目录   | 包含JDK工具的几个JAR和其他类型的文件。它有一个tools.jar文件，其中包含javac编译器的Java类 |
| jre/bin 目录 | 包含基本命令，如java命令。在Windows平台上，它包含系统的运行时动态链接库（DLL）。 |
| jre/lib 目录 | 包含用户可编辑的配置文件，如.properties和.policy文件。包含几个JAR。rt.jar文件包含运行时的Java类和资源文件。 |

![JDK9](F:\MyNut\我的坚果云\JavaSE\img\JDK9-11\JDK9.png)

| 没有名为jre的子目录 |                                                              |
| ------------------- | ------------------------------------------------------------ |
| bin目录             | 包含所有命令。在Windows平台上，它继续包含系统的运行时动态链接库。 |
| conf目录            | 包含用户可编辑的配置文件，例如以前位于jre\lib目录中的.properties和.policy文件 |
| include目录         | 包含要在以前编译本地代码时使用的C/C++头文件。它只存在于JDK中 |
| jmods目录           | 包含JMOD格式的平台模块。创建自定义运行时映像时需要它。它只存在于JDK中 |
| legal目录           | 包含法律声明                                                 |
| lib目录             | 包含非Windows平台上的动态链接本地库。其子目录和文件不应由开发人员直接编辑或使用 |

- 新版本jdk的下载与IDEA开发环境的设置

![image-20200519133602928](F:\MyNut\我的坚果云\JavaSE\img\JDK9-11\02.png)

### java9新特性：模块化系统

- 谈到Java 9 大家往往第一个想到的就是Jigsaw 项目。众所周知，Java 已经发展超过20 年（95 年最初发布），Java 和相关生态在不断丰富的同时也越来越暴露出一些问题：
  - Java 运行环境的膨胀和臃肿。每次JVM启动的时候，至少会有30～60MB的内存加载，主要原因是JVM需要加载rt.jar，不管其中的类是否被classloader加载，第一步整个jar都会被JVM加载到内存当中去（而模块化可以根据模块的需要加载程序运行需要的class）
  - 当代码库越来越大，创建复杂，盘根错节的“意大利面条式代码”的几率呈指数级的增长。不同版本的类库交叉依赖导致让人头疼的问题，这些都阻碍了Java 开发和运行效率的提升。
  - 很难真正地对代码进行封装, 而系统并没有对不同部分（也就是JAR 文件）之间的依赖关系有个明确的概念。每一个公共类都可以被类路径之下任何其它的公共类所访问到，这样就会导致无意中使用了并不想被公开访问的API。

- 本质上讲也就是说，用模块来管理各个package，通过声明某个package暴露，，模块(module)的概念，其实就是package外再裹一层，不声明默认就是隐藏。因此，模块化使得代码组织上更安全，因为它可以指定哪些部分可以暴露，哪些部分隐藏。
- 实现目标
  - 模块化的主要目的在于减少内存的开销
  - 只须必要模块，而非全部jdk模块，可简化各种类库和大型应用的开发和维护
  - 改进Java SE 平台，使其可以适应不同大小的计算设备
  - 改进其安全性，可维护性，提高性能

- 模块将由通常的类和新的模块声明文件（module-info.java）组成。该文件是位于java代码结构的顶层，该模块描述符明确地定义了我们的模块需要什么依赖关系，以及哪些模块被外部使用。在exports子句中未提及的所有包默认情况下将封装在模块中，不能在外部使用。

![image-20200519132441583](F:\MyNut\我的坚果云\JavaSE\img\JDK9-11\01.png)

![image-20200519133840281](F:\MyNut\我的坚果云\JavaSE\img\JDK9-11\03.png)

- 案例结构

![image-20200519134701390](F:\MyNut\我的坚果云\JavaSE\img\JDK9-11\04.png)

- Person类

```java
package git;

/**
 * @author subei
 * @create 2020-05-19 13:26
 */
public class Person {
    private String name;
    private int age;

    public Person() {
    }

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    @Override
    public String toString() {
        return "Person{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }
}
```

- module-info.java——JDK9Test中

```java
/**
 * @author subei
 * @create 2020-05-19 13:37
 */
module JDK9Test {
     exports git;   //exports 包名--》将包暴露使用
}
```

- module-info.java——day13中

```java
/**
 * @author subei
 * @create 2020-05-19 13:34
 */
module day13 {
    requires JDK9Test;  //requires 包名---》接收包
    requires junit;//若要调用JDK9以上版本的测试类，需要引入
    exports github;
}
```

- ModuleTest类

```java
import git.Person;

/**
 * @author subei
 * @create 2020-05-19 13:29
 */
public class ModuleTest {
    public static void main(String[] args) {
        Person p = new Person("Jack",20);
        System.out.println(p);
    }
}
```

![image-20200519135022108](F:\MyNut\我的坚果云\JavaSE\img\JDK9-11\05.png)

### java9新特性：Java的REPL工具：jshell

- 产生背景

  > 像Python和Scala之类的语言早就有交互式编程环境REPL(read-evaluate-print-loop)了，以交互式的方式对语句和表达式进行求值。开发者只需要输入一些代码，就可以在编译前获得对程序的反馈。而之前的Java版本要想执行代码，必须创建文件、声明类、提供测试方法方可实现。

- 设计理念

  - 即写即得、快速运行

- 实现目标

  - Java 9 中终于拥有了REPL工具：jShell。让Java可以像脚本语言一样运行，从控制台启动jShell，利用jShell在没有创建类的情况下直接声明变量，计算表达式，执行语句。即开发时可以在命令行里直接运行Java的代码，而无需创建Java文件，无需跟人解释”public static void main(String[] args)”这句废话。
  - jShell也可以从文件中加载语句或者将语句保存到文件中。
  - jShell也可以是tab键进行自动补全和自动添加分号。

#### JShell相关命令

![image-20200519140008958](F:\MyNut\我的坚果云\JavaSE\img\JDK9-11\06.png)

> 对于这个问题的出现，是由于JDK环境配置未从JDK8转到JDK9及以上版本。解决方法如下：

![image-20200519140212374](F:\MyNut\我的坚果云\JavaSE\img\JDK9-11\07.png)

![image-20200519140322516](F:\MyNut\我的坚果云\JavaSE\img\JDK9-11\08.png)

> 保存确定，重启CMD字符，就会如下：

- 调出jShell：jShell

![image-20200519140448123](F:\MyNut\我的坚果云\JavaSE\img\JDK9-11\09.png)

- 获取帮助： /help intro

![image-20200519140616325](F:\MyNut\我的坚果云\JavaSE\img\JDK9-11\10.png)

- 基本使用：
- 在JShell环境下，语句末尾的“;”是可选的。但推荐还是最好加上。提高代码可读性。

![image-20200519141120103](F:\MyNut\我的坚果云\JavaSE\img\JDK9-11\11.png)

- 导入指定的包： import java.util.*;

![image-20200519141155093](F:\MyNut\我的坚果云\JavaSE\img\JDK9-11\12.png)

- 默认已经导入如下的所有包：(包含java.lang包)：/imports

![image-20200519141305462](F:\MyNut\我的坚果云\JavaSE\img\JDK9-11\13.png)

- 只需按下Tab键，就能自动补全代码：

![image-20200519141451201](F:\MyNut\我的坚果云\JavaSE\img\JDK9-11\14.png)

- 列出当前session里所有有效的代码片段：/list

![image-20200519141531572](F:\MyNut\我的坚果云\JavaSE\img\JDK9-11\15.png)

- 查看当前session下所有创建过的变量：/vars

![image-20200519141611645](F:\MyNut\我的坚果云\JavaSE\img\JDK9-11\16.png)

- 查看当前session下所有创建过的方法：

![image-20200519142706817](F:\MyNut\我的坚果云\JavaSE\img\JDK9-11\17.png)

- 使用外部代码编辑器来编写Java代码：

![image-20200519142813199](F:\MyNut\我的坚果云\JavaSE\img\JDK9-11\18.png)

![image-20200519142954323](F:\MyNut\我的坚果云\JavaSE\img\JDK9-11\19.png)

![image-20200519143036919](F:\MyNut\我的坚果云\JavaSE\img\JDK9-11\20.png)

- 使用/open命令调用：

![image-20200519144530840](F:\MyNut\我的坚果云\JavaSE\img\JDK9-11\21.png)

- 没有受检异常（编译时异常）：

![image-20200519154718175](F:\MyNut\我的坚果云\JavaSE\img\JDK9-11\22.png)

> 说明：本来应该强迫我们捕获一个IOException，但却没有出现。因为jShell在后台为我们隐藏了。

- 退出jShell：/exit

![image-20200519154747472](F:\MyNut\我的坚果云\JavaSE\img\JDK9-11\23.png)

### java.lang.IllegalAccessException: class org.junit.runners.BlockJUnit4ClassRunner (in module junit) cannot access class github2.JDK10Test (in module day13) because module day13 does not export github2 to module junit报错解决

![image-20200520113059068](F:\MyNut\我的坚果云\JavaSE\img\JDK9-11\24.png)

> 对于这个问题，在网上并没有很清楚地解决，经过长期的处理无果，求助网友大佬ZoZBie、◕ ̯͡◕：920698927，帮我远程处理，最后得出结论如下：

![image-20200520113617216](F:\MyNut\我的坚果云\JavaSE\img\JDK9-11\25.png)

![image-20200520113702906](F:\MyNut\我的坚果云\JavaSE\img\JDK9-11\26.png)

> 注意这是关于IDEA2020版本的解决方案！！！目前对于笔者就是如此解决的，如果你有更好的，欢迎交流！！！

### java9新特性：接口中声明私有方法

- Java8中规定接口中的方法除了抽象方法之外，还可以定义静态方法和默认的方法。一定程度上，扩展了接口的功能，此时的接口更像是一个抽象类。

- 在Java9中，接口更加的灵活和强大，**连方法的访问权限修饰符都可以声明为private的了**，此时方法将不会成为你对外暴露的API的一部分。

```java
/**
 * @author subei
 * @create 2020-05-19 14:11
 */
public interface MyInterface {

    //如下的三个方法的权限修饰符都是public
    void methodAbstract();

    static void methodStatic(){
        System.out.println("这是接口中的静态方法");
    }

    default void methodDefault(){
        System.out.println("这是接口中的默认方法");
        methodPrivate();
    }

    //jdk 9中允许接口中定义私有的方法
    private void methodPrivate(){
        System.out.println("这是接口中的私有方法");
    }
}
```

```java
/**
 * @author subei
 * @create 2020-05-19 14:15
 */
public class MyInterfaceImpl implements MyInterface{

    @Override
    public void methodAbstract() {

    }

    @Override
    public void methodDefault() {
        System.out.println("实现类重写了接口中的默认方法");
    }

    public static void main(String[] args) {
        //接口中的静态方法只能由接口自己调用
        MyInterface.methodStatic();
        
        //接口的实现类不能调用接口的静态方法
//        MyInterfaceImpl.methodStatic();

        MyInterfaceImpl impl = new MyInterfaceImpl();
        impl.methodDefault();
        
        //接口的私有方法，不能在接口外部调用
//        impl.methodPrivate();
    }
}
```

### java9新特性：钻石操作符的语法升级

- 我们将能够与匿名实现类共同使用钻石操作符（diamondoperator）在Java8中如下的操作是会报错的：

```java
    //java9特性5：钻石操作符的升级
    @Test
    public void test2(){
        //钻石操作符与匿名内部类在java 8中不能共存。在java9可以。
        Comparator<Object> com = new Comparator<>() {
            @Override
            public int compare(Object o1, Object o2) {
                return 0;
            }
        };

        //jdk7中的新特性：类型推断
        ArrayList<String> list = new ArrayList<>();
    }
```

- 编译报错信息：Cannotuse“<>”with anonymous inner classes.

### java9新特性：try结构的语法升级

```java
import org.junit.Test;

import java.io.IOException;
import java.io.InputStreamReader;
import java.net.MalformedURLException;
import java.net.URL;
import java.util.ArrayList;
import java.util.Comparator;

/**
 * @author subei
 * @create 2020-05-19 14:00
 */
public class Java9Test {

    //java9的特性6：try操作的升级
    public static void main(String[] args) {
        //java 8之前的资源关闭的操作
//        InputStreamReader reader = null;
//        try {
//            reader = new InputStreamReader(System.in);
//            char[] cbuf = new char[20];
//            int len;
//            if((len = reader.read(cbuf) )!= -1){
//                String str = new String(cbuf,0,len);
//                System.out.println(str);
//            }
//        } catch (IOException e) {
//            e.printStackTrace();
//        } finally {
//            if(reader != null){
//                try {
//                    reader.close();
//                } catch (IOException e) {
//                    e.printStackTrace();
//                }
//            }
//        }

        //java 8中资源关闭操作: Java 8 中，可以实现资源的自动关闭
        //要求自动关闭的资源的实例化必须放在try的一对小括号中
//        try(InputStreamReader reader = new InputStreamReader(System.in)){
//            char[] cbuf = new char[20];
//            int len;
//            if((len = reader.read(cbuf) )!= -1){
//                String str = new String(cbuf,0,len);
//                System.out.println(str);
//            }
//        } catch (IOException e) {
//            e.printStackTrace();
//        }

        //java9中资源关闭操作：需要自动关闭的资源的实例化可以放在try的一对小括号外。
        //此时的资源属性是常量，声明为final的，不可修改
        InputStreamReader reader = new InputStreamReader(System.in);
        try (reader) {
            char[] cbuf = new char[20];
            int len;
            if((len = reader.read(cbuf) )!= -1){
                String str = new String(cbuf,0,len);
                System.out.println(str);
            }
//            reader = null;
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

### java9新特性：String底层存储结构的变更

- Motivation

  > The current implementation of the String class stores characters in a char array, using two bytes (sixteen bits) for each character. Data gathered from many different applications indicates that strings are a major component of heap usage and, moreover, that most String objects contain only Latin-1 characters. Such characters require only one byte of storage, hence half of the space in the internal char arrays of such String objects is going unused.

  > String类的当前实现在char数组中存储字符，每个字符使用两个字节(16位)。从许多不同的应用程序收集的数据表明，字符串是堆使用的主要组成部分，而且，大多数字符串对象只包含Latin-1字符。这样的字符只需要一个字节的存储空间，因此这样的字符串对象的内部char数组中的一半空间将不会被使用。

- Description

  > We propose to change the internal representation of the String class from a UTF-16 char array to a byte array plus an encoding-flag field. The new String class will store characters encoded either as ISO-8859-1/Latin-1 (one byte per character), or as UTF-16 (two bytes per character), based upon the contents of the string. The encoding flag will indicate which encoding is used.

  > 我们建议将字符串类的内部表示形式从UTF-16字符数组更改为字节数组加上编码标记字段。新的String类将根据字符串的内容存储编码为ISO-8859-1/Latin-1(每个字符一个字节)或UTF-16(每个字符两个字节)的字符。编码标志将指示使用哪种编码。

- 结论：String再也不用char[]来存储啦，改成了byte[]加上编码标记，节约了一些空间。

  ```java
  public final class String
          implements java.io.Serializable, Comparable<String>, CharSequence {
      @Stableprivate 
      final byte[] value;
  }
  ```

- 那StringBuffer和StringBuilder是否仍无动于衷呢？

  > String-related classes such asAbstractStringBuilder,StringBuilder, andStringBufferwill be updated to use the same representation, as will the HotSpot VM‘s intrinsic(固有的、内置的) string operations.

### java9新特性：集合工厂方法创建只读集合

- 要创建一个只读、不可改变的集合，必须构造和分配它，然后添加元素，最后包装成一个不可修改的集合。

```java
import org.junit.Test;

import java.util.*;

/**
 * @author subei
 * @create 2020-05-19 14:28
 */
public class Java9Test2 {

    //java9新特性八：集合工厂方法：创建只读集合
    //java8中的写法：
    @Test
    public void test() {
        List<String> namesList = new ArrayList<>();
        namesList.add("Joe");
        namesList.add("Bob");
        namesList.add("Bill");
        //返回的namesList是一个只读的集合
        namesList = Collections.unmodifiableList(namesList);
        namesList.add("Franck");

        System.out.println(namesList);
    }

    @Test
    public void  test2(){
        List<String> list = Collections.unmodifiableList(Arrays.asList("a", "b", "c"));
        Set<String> set = Collections.unmodifiableSet(new HashSet<>(Arrays.asList("a", "b", "c")));
        // 如下操作不适用于jdk 8 及之前版本,适用于jdk 9
        Map<String, Integer> map = Collections.unmodifiableMap(new HashMap<>() {
            {
                put("a", 1);
                put("b", 2);
                put("c", 3);
            }
        });
        map.forEach((k, v) -> System.out.println(k + ":" + v));
    }

    @Test
    public void test3() {
        //此时得到的集合list也是一个只读集合。
        List<Integer> list = Arrays.asList(1, 7, 9, 3, 2);
        //报异常
        list.add(6);
    }

    @Test
    public void test4() {
        List<Integer> list1 = List.of(1, 2, 3, 4, 5);
        //不能添加
//        list1.add(6);
        System.out.println(list1);

        Set<Integer> set1 = Set.of(23, 3, 54, 65, 43, 76, 87, 34, 46);
        //不能添加
//        set1.add(4);
        System.out.println(set1);

        Map<String, Integer> map1 = Map.of("Josh", 23, "Jack", 54, "Franck", 12);
        //不能添加
        //map1.put("George",34);

        System.out.println(map1);

        Map<String, Integer> map2 = Map.ofEntries(Map.entry("Josh", 34), Map.entry("Jim", 21));
//        map2.put("George",34);
        System.out.println(map2);
    }
    
}
```

### java9新特性：InputStream中的transferTo()方法

> InputStream 终于有了一个非常有用的方法：transferTo，可以用来将数据直接传输到OutputStream，这是在处理原始数据流时非常常见的一种用法，如下示例。

```java
import org.junit.Test;

import java.io.FileOutputStream;
import java.io.IOException;
import java.io.InputStream;
import java.io.OutputStream;

/**
 * @author subei
 * @create 2020-05-19 14:28
 */
public class Java9Test2 {

    //java9新特性九：InputStream的新方法:tranferTo()
    @Test
    public void test5() {
        ClassLoader cl = this.getClass().getClassLoader();
        try (InputStream is = cl.getResourceAsStream("hello.txt");
             OutputStream os = new FileOutputStream("src\\hello1.txt")) {
            is.transferTo(os); // 把输入流中的所有数据直接自动地复制到输出流中
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
    
}
```

### java9新特性：StreamAPI新增的4个方法

- Java 的Steam API 是java标准库最好的改进之一，让开发者能够快速运算，从而能够有效的利用数据并行计算。Java 8 提供的Steam 能够利用多核架构实现声明式的数据处理。
- 在Java 9 中，Stream API 变得更好，Stream 接口中添加了4 个新的方法：takeWhile, dropWhile, ofNullable，还有个iterate 方法的新重载方法，可以让你提供一个Predicate (判断条件)来指定什么时候结束迭代。
- 除了对Stream 本身的扩展，Optional 和Stream 之间的结合也得到了改进。现在可以通过Optional 的新方法stream() 将一个Optional 对象转换为一个(可能是空的) Stream 对象。

```java
import org.junit.Test;

import java.util.Arrays;
import java.util.List;
import java.util.stream.Stream;

/**
 * @author subei
 * @create 2020-05-19 14:43
 */
public class Java9Test3 {

    //java9新特性十：Stream API的加强
    @Test
    public void test(){
        List<Integer> list = Arrays.asList(23, 43, 45, 55, 61, 54, 32, 2, 45, 89, 7);
        //takeWhile 返回从开头开始的按照指定规则尽量多的元素
//        list.stream().takeWhile(x -> x < 60).forEach(System.out::println);
        //dropWhile():与 takeWhile 相反，返回剩余的元素。
        list.stream().dropWhile(x -> x < 60).forEach(System.out::println);
    }

    @Test
    public void test2(){
        //of()参数中的多个元素，可以包含null值
        Stream<Integer> stream1 = Stream.of(1, 2, 3,null);
        stream1.forEach(System.out::println);
        //of()参数不能存储单个null值。否则，报异常
//        Stream<Object> stream2 = Stream.of(null);
//        stream2.forEach(System.out::println);
        Integer i = 10;
        i = null;
        //ofNullable()：形参变量是可以为null值的单个元素
        Stream<Integer> stream3 = Stream.ofNullable(i);
        long count = stream3.count();
        System.out.println(count);
    }

    @Test
    public void test3(){
        Stream.iterate(0,x -> x + 1).limit(10).forEach(System.out::println);

        //java9中新增的重载的方法
        Stream.iterate(0,x -> x < 100,x -> x + 1).forEach(System.out::println);
    }

}
```

### java9新特性：Optional的新方法stream()

```java
 //java9新特性十一：Optional提供了新的方法stream()
    @Test
    public void test4(){
        List<String> list = new ArrayList<>();
        list.add("Tom");
        list.add("Jerry");
        list.add("Tim");

        Optional<List<String>> optional = Optional.ofNullable(list);
        Stream<List<String>> stream = optional.stream();
//        long count = stream.count();
//        System.out.println(count);
        stream.flatMap(x -> x.stream()).forEach(System.out::println);
    }
```

### java9新特性：升级的Nashorn引擎（在JDK11中取消）

- Nashorn项目在JDK9中得到改进，它为Java提供轻量级的Javascript运行时。Nashorn项目跟随Netscape的Rhino项目，目的是为了在Java中实现一个高性能但轻量级的Javascript运行时。Nashorn项目使得Java应用能够嵌入Javascript。它在JDK8中为Java提供一个Javascript引擎。
- JDK9包含一个用来解析Nashorn的ECMAScript语法树的API。这个API使得IDE和服务端框架不需要依赖Nashorn项目的内部实现类，就能够分析ECMAScript代码。

## Java 10 的新特性

### java10新特性的概述

- 2018年3月21日，Oracle官方宣布Java10正式发布。
- 需要注意的是Java 9 和Java 10 都不是LTS(Long-Term-Support) 版本。和过去的Java 大版本升级不同，这两个只有半年左右的开发和维护期。而未来的Java 11，也就是18.9 LTS，才是Java 8 之后第一个LTS 版本。
- JDK10一共定义了109个新特性，其中包含12个JEP（对于程序员来讲，真正的新特性其实就一个），还有一些新API和JVM规范以及JAVA语言规范上的改动。
- JDK10的12个JEP（JDKEnhancementProposal特性加强提议）参阅官方文档：http://openjdk.java.net/projects/jdk/10/

- JDK10的12个JEP
  - 286:Local-Variable Type Inference 局部变量类型推断
  - 296:Consolidate the JDK Forest into a Single Repository  JDK库的合并
  - 304:Garbage-Collector Interface 统一的垃圾回收接口
  - 307:Parallel Full GC for G1 为G1提供并行的Full GC
  - 310:Application Class-Data Sharing 应用程序类数据（AppCDS）共享
  - 312:Thread-Local Handshakes  ThreadLocal握手交互
  - 313:Remove the Native-Header Generation Tool (javah) 移除JDK中附带的javah工具
  - 314:Additional Unicode Language-Tag Extensions 使用附加的Unicode语言标记扩展
  - 316:Heap Allocation on Alternative Memory Devices 能将堆内存占用分配给用户指定的备用内存设备
  - 317:Experimental Java-Based JIT Compiler 使用基于Java的JIT编译器
  - 319:Root Certificates 根证书
  - 322:Time-Based Release Versioning 基于时间的发布版本

### java10新特性：局部变量类型推断

- 产生背景

  > 开发者经常抱怨Java中引用代码的程度。局部变量的显示类型声明，常常被认为是不必须的，给一个好听的名字经常可以很清楚的表达出下面应该怎样继续。

- 好处：减少了啰嗦和形式的代码，避免了信息冗余，而且对齐了变量名，更容易阅读！

- 举例如下：

  - 场景一：类实例化时

    > 作为Java开发者，在声明一个变量时，我们总是习惯了敲打两次变量类型，第一次用于声明变量类型，第二次用于构造器。

    ```java
    LinkedHashSet<Integer> set= new LinkedHashSet<>();
    ```

    

  - 场景二：返回值类型含复杂泛型结构

    > 变量的声明类型书写复杂且较长，尤其是加上泛型的使用

    ```java
    Iterator<Map.Entry<Integer, Student>> iterator= set.iterator();
    ```

  - 场景三：我们也经常声明一种变量，它只会被使用一次，而且是用在下一行代码中，比如：

    ```java
    URL url= new URL("https://www.waysto.work/");
    URLConnection connection= url.openConnection();
    Reader reader= newBufferedReader(new InputStreamReader(connection.getInputStream()));
    ```

  - 尽管IDE可以帮我们自动完成这些代码，但当变量总是跳来跳去的时候，可读性还是会受到影响，因为变量类型的名称由各种不同长度的字符组成。而且，有时候开发人员会尽力避免声明中间变量，因为太多的类型声明只会分散注意力，不会带来额外的好处。

```java
import org.junit.Test;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.net.URL;
import java.util.ArrayList;
import java.util.List;

/**
 * @author subei
 * @create 2020-05-20 8:57
 */
public class JDK10Test {
    /**
     * java10新特性一：局部变量的类型推断
     */
    @Test
    public void test(){
        //1.声明变量时，根据所附的值，推断变量的类型
        var num = 10;

        var list = new ArrayList<Integer>();
        list.add(123);

        //2.遍历操作
        for (var i : list) {
            System.out.println(i);
            System.out.println(i.getClass());
        }

        //3.普通的遍历操作
        for (var i = 0; i < 100; i++) {
            System.out.println(i);
        }
    }

    @Test
    public void test2(){
        //1.局部变量不赋值，就不能实现类型推断
//        var num ;

        //2.lambda表示式中，左边的函数式接口不能声明为var
//        Supplier<Double> sup = () -> Math.random();

//        var sup = () -> Math.random();

        //3.方法引用中，左边的函数式接口不能声明为var
//        Consumer<String> con = System.out::println;

//        var con = System.out::println;

        //4.数组的静态初始化中，注意如下的情况也不可以
        int[] arr = {9, 5, 2, 7};
//        var arr = {9,5,2,7};
    }

    @Test
    public void test3() {
//        情况1：没有初始化的局部变量声明
//        var s = null;
        
//        情况6：catch块
//        try{
//
//        }catch(var e){
//            e.printStackTrace();
//        }
    }
    //情况2：方法的返回类型
//    public var method1(){
//
////        return 0;
//    }
    // 情况3：方法的参数类型
//    public void method2(var num){
//
//    }

    //情况4：构造器的参数类型
//    public Java10Test(var i){
//
//    }

    //情况5：属性
//    var num;


    @Test
    public void test4() {
        try {
            var url = new URL("http://www.waysto.work/");
            var connection = url.openConnection();
            var reader = new BufferedReader(
                    new InputStreamReader(connection.getInputStream()));
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

- 工作原理

  > 在处理var时，编译器先是查看表达式右边部分，并根据右边变量值的类型进行推断，作为左边变量的类型，然后将该类型写入字节码当中。

- 注意

  > var不是一个关键字
  >
  > 你不需要担心变量名或方法名会与var发生冲突，因为var实际上并不是一个关键字，而是一个类型名，只有在编译器需要知道类型的地方才需要用到它。除此之外，它就是一个普通合法的标识符。也就是说，除了不能用它作为类名，其他的都可以，但极少人会用它作为类名。
  >
  > 这不是JavaScript
  >
  > 首先我要说明的是，var并不会改变Java是一门静态类型语言的事实。编译器负责推断出类型，并把结果写入字节码文件，就好像是开发人员自己敲入类型一样。下面是使用IntelliJ（实际上是Fernflower的反编译器）反编译器反编译出的代码



### java10新特性：集合新增创建不可变集合的方法

- 自Java9开始，Jdk里面为集合（List/Set/Map）都添加了of(jdk9新增)和copyOf(jdk10新增)方法，它们两个都用来创建不可变的集合，来看下它们的使用和区别。

```java
import org.junit.Test;

import java.util.ArrayList;
import java.util.List;

/**
 * @author subei
 * @create 2020-05-20 8:57
 */
public class JDK10Test {

    //java10的新特性二：集合中新增的copyOf()，用于创建一个只读的集合
    @Test
    public void test5(){
        //示例1：
        var list1 = List.of("Java", "Python", "C");
        var copy1 = List.copyOf(list1);
        System.out.println(list1 == copy1); // true

        //示例2：
        var list2 = new ArrayList<String>();
        list2.add("KKK");
        var copy2 = List.copyOf(list2);
        System.out.println(list2 == copy2); // false

        //示例1和2代码基本一致，为什么一个为true,一个为false?
        //结论：copyOf(Xxx coll):如果参数coll本身就是一个只读集合，则copyOf()返回值即为当前的coll
        //如果参数coll不是一个只读集合，则copyOf()返回一个新的集合，这个集合是只读的。
    }
}
```

- 从 源 码 分 析，可以看出copyOf方 法 会 先 判 断 来 源 集 合 是 不 是AbstractImmutableList类型的，如果是，就直接返回，如果不是，则调用of创建一个新的集合。
- 示例2因为用的new创建的集合，不属于不可变AbstractImmutableList类的子类，所以copyOf方法又创建了一个新的实例，所以为false。
- 注意：使用of和copyOf创建的集合为不可变集合，不能进行添加、删除、替换、排序等操作，不然会报java.lang.UnsupportedOperationException异常。
- 上面演示了List的of和copyOf方法，Set和Map接口都有。

## Java 11 的新特性

### java11新特性的概述

> 北京时间2018年9月26日，Oracle官方宣布Java11正式发布。这是Java大版本周期变化后的第一个长期支持版本，非常值得关注。从官网即可下载,最新发布的Java11将带来ZGC、HttpClient等重要特性，一共包含17个JEP（JDKEnhancementProposals，JDK增强提案）。其实，总共更新不止17个，只是我们更关注如下的17个JEP更新。

![image-20200520115708509](F:\MyNut\我的坚果云\JavaSE\img\JDK9-11\28.png)

- JDK11将是一个企业不可忽视的版本。从时间节点来看，JDK11的发布正好处在JDK8免费更新到期的前夕，同时JDK9、10也陆续成为“历史版本”，下面是[OracleJDK支持路线图](https://www.oracle.com/java/technologies/java-se-support-roadmap.html)：

![image-20200520114747220](F:\MyNut\我的坚果云\JavaSE\img\JDK9-11\27.png)

> [按照 Oracle 公布的支持路线图](https://www.oracle.com/technetwork/java/javase/eol-135779.html)，Java 11 将会获得 Oracle 提供的长期支持服务，直至2026年9月。

![Java 11 正式发布！支持期限至2026年9月](F:\MyNut\我的坚果云\JavaSE\img\JDK9-11\29.png)

### java11新特性：String新增的方法

|         描述         |                      举例                      |
| :------------------: | :--------------------------------------------: |
| 判断字符串是否为空白 |             " ".isBlank(); // true             |
|     去除首尾空白     |     " Javastack ".strip(); // "Javastack"      |
|     去除尾部空格     | " Javastack ".stripTrailing(); // " Javastack" |
|     去除首部空格     | " Javastack ".stripLeading(); // "Javastack "  |
|      复制字符串      |       "Java".repeat(3);// "JavaJavaJava"       |
|       行数统计       |        "A\nB\nC".lines().count(); // 3         |

```java
import org.junit.Test;

/**
 * @author subei
 * @create 2020-05-20 10:27
 */
public class JDK11Test {
    
    //java 11新特性一：String中新增的方法
    @Test
    public void test(){
//        isBlank():判断字符串是否为空白
        System.out.println("  \t  \t  \n  ".isBlank());
//        strip():去除首尾空白
        System.out.println("++++" + "  \t abc \t  \n  ".strip() + "++++");
        System.out.println("++++" + "  \t abc \t  \n  ".trim() + "++++");
//        stripTrailing():去除尾部空格
        System.out.println("++++" + "  \t abc \t  \n  ".stripTrailing() + "++++");
//        stripLeading():去除首部空格
        System.out.println("++++" + "  \t abc \t  \n  ".stripLeading() + "++++");
//        repeat(int count):复制字符串
        String str1 = "abc";
        String str2 = str1.repeat(5);
        System.out.println(str2);

//        lines().count():行数统计
        String str3 = "abc\nEFG\nH";
        System.out.println(str3.lines().count());
    }
}
```

### java11新特性：Optional新增的方法

> Optional也增加了几个非常酷的方法，现在可以很方便的将一个Optional转换成一个Stream,或者当一个空Optional时给它一个替代的。

|新增方法 |描述|新增的版本|
| :----------------: |------------------: | :---------------: |
|boolean isEmpty()|判断value是否为空 |JDK 11|
|ifPresentOrElse(Consumer<? superT>action,RunnableemptyAction)|value非空，执行参数1功能；如果value为空，执行参数2功能|JDK 9|
|Optional<T>or(Supplier<? extendsOptional<? extendsT>>supplier)|value非空，返回对应的Optional；value为空，返回形参封装的Optional|JDK 9|
|Stream<T>stream()|value非空，返回仅包含此value的Stream；否则，返回一个空的Stream|JDK 9|
|TorElseThrow()|value非空，返回value；否则抛异常NoSuchElementException|JDK 10|

```java
import org.junit.Test;

import java.util.Optional;

/**
 * @author subei
 * @create 2020-05-20 10:27
 */
public class JDK11Test {

    //java11新特性二：Optional新增的方法
    @Test
    public void test2(){
        var op = Optional.empty();
        System.out.println(op.isPresent());//判断内部的value是否存在
        System.out.println(op.isEmpty());//判断内部的value是否为空

        op = Optional.of("abc");
        //orElseThrow():value非空，返回value；否则抛异常NoSuchElementException
        var obj = op.orElseThrow();
        System.out.println(obj);

        Optional<String> op1 = Optional.of("hello");
//        op = Optional.empty();
        //or:value非空，返回对应的Optional；value为空，返回形参封装的Optional
        Optional<Object> op2 = op.or(() -> op1);
        System.out.println(op2);
    }
}
```

### java11新特性：局部变量类型推断的升级

> 在var上添加注解的语法格式，在jdk10中是不能实现的。在JDK11中加入了这样的语法。

```java
import org.junit.Test;

import java.util.function.Consumer;

/**
 * @author subei
 * @create 2020-05-20 10:27
 */
public class JDK11Test {

    //java11新特性三：局部变量类型推断的升级
    @Test
    public void test3(){
        //错误的形式: 必须要有类型, 可以加上var
//        Consumer<String> con1 = (@Deprecated t) -> System.out.println(t.toUpperCase());
        // 正确的形式:
        // 使用var的好处是在使用lambda表达式时给参数加上注解。
        Consumer<String> con2 = (@Deprecated var t) -> System.out.println(t.toUpperCase());
    }
}
```

### java11新特性：HttpClient

- HTTP，用于传输网页的协议，早在1997年就被采用在目前的1.1版本中。直到2015年，HTTP2才成为标准。

  ![image-20200520123708978](F:\MyNut\我的坚果云\JavaSE\img\JDK9-11\30.png)

- HTTP/1.1和HTTP/2的主要区别是如何在客户端和服务器之间构建和传输数据。HTTP/1.1依赖于请求/响应周期。HTTP/2允许服务器“push”数据：它可以发送比客户端请求更多的数据。这使得它可以优先处理并发送对于首先加载网页至关重要的数据。

- 这是Java9开始引入的一个处理HTTP请求的的HTTPClientAPI，该API支持同步和异步，而在Java11中已经为正式可用状态，你可以在java.net包中找到这个API。

- 它将替 代 仅 适 用 于blocking模式的HttpURLConnection（HttpURLConnection是在HTTP1.0的时代创建的，并使用了协议无关的方法），并提供对WebSocket和HTTP/2的支持。

- day13——module-info.java类

```java
/**
 * @author subei
 * @create 2020-05-19 13:34
 */
module day13 {
    requires JDK9Test;  //requires 包名---》接收包
    requires junit;//若要调用JDK9以上版本的测试类，需要引入
    exports github;
    exports github2;
    exports github3;
    requires java.net.http;
}
```

- 测试类

```java
import org.junit.Test;

import java.io.IOException;
import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;
import java.util.concurrent.CompletableFuture;

/**
 * @author subei
 * @create 2020-05-20 10:27
 */
public class JDK11Test {

    //java11新特性四：HttpClient替换原有的HttpURLConnection。
    @Test
    public void test4(){
        try {
            HttpClient client = HttpClient.newHttpClient();
            HttpRequest request = HttpRequest.newBuilder(URI.create("http://127.0.0.1:8080/test/")).build();
            HttpResponse.BodyHandler<String> responseBodyHandler = HttpResponse.BodyHandlers.ofString();
            HttpResponse<String> response = client.send(request, responseBodyHandler);
            String body = response.body();
            System.out.println(body);
        } catch (IOException e) {
            e.printStackTrace();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }

    @Test
    public void test5(){
        HttpClient client = HttpClient.newHttpClient();
        HttpRequest request = HttpRequest.newBuilder(URI.create("http://127.0.0.1:8080/test/")).build();
        HttpResponse.BodyHandler<String> responseBodyHandler = HttpResponse.BodyHandlers.ofString();
        CompletableFuture<HttpResponse<String>> sendAsync = client.sendAsync(request, responseBodyHandler);
        sendAsync.thenApply(t -> t.body()).thenAccept(System.out::println);
        //HttpResponse<String> response = sendAsync.get();
        //String body = response.body();
        //System.out.println(body);
    }
}
```

### java11新特性：更简化的编译运行程序

```java
看下面的代码。
    //编译
    javac Javastack.java
    //运行
    java Javastack
```

> 在我们的认知里面，要运行一个Java源代码必须先编译，再运行，两步执行动作。而在未来的Java11版本中，通过一个java命令就直接搞定了，如以下所示：

> java Javastack.java

![image-20200520125254649](F:\MyNut\我的坚果云\JavaSE\img\JDK9-11\31.png)

> 一个命令编译运行源代码的注意点：
>
> - 执行源文件中的第一个类, 第一个类必须包含主方法。
> - 并且不可以使用其它源文件中的自定义类, 本文件中的自定义类是可以使用的。

### Java语言高级-java11新特性：其它新特性

#### 废弃Nashorn引擎

> 废除Nashornjavascript引擎，在后续版本准备移除掉，有需要的可以考虑使用GraalVM。

#### ZGC

- GC是java主要优势之一。然而,当GC停顿太长,就会开始影响应用的响应时间。消除或者减少GC停顿时长,java将对更广泛的应用场景是一个更有吸引力的平台。此外,现代系统中可用内存不断增长,用户和程序员希望JVM能够以高效的方式充分利用这些内存,并且无需长时间的GC暂停时间。
- ZGC,AScalableLow-LatencyGarbageCollector(Experimental)ZGC,这应该是JDK11最为瞩目的特性,没有之一。但是后面带了Experimental,说明这还不建议用到生产环境。
- ZGC是一个并发,基于region,压缩型的垃圾收集器,只有root扫描阶段会STW(stoptheworld),因此GC停顿时间不会随着堆的增长和存活对象的增长而变长。
- 优势：
  - GC暂停时间不会超过10ms
  - 既能处理几百兆的小堆,也能处理几个T的大堆(OMG)
  - 和G1相比,应用吞吐能力不会下降超过15%
  - 为未来的GC功能和利用colord指针以及Loadbarriers优化奠定基础
  - 初始只支持64位系统
- ZGC的设计目标是：支持TB级内存容量，暂停时间低（<10ms），对整个程序吞吐量的影响小于15%。将来还可以扩展实现机制，以支持不少令人兴奋的功能，例如多层堆（即热对象置于DRAM和冷对象置于NVMe闪存），或压缩堆。

#### 其他的新特性

- Unicode 10
- Deprecate the Pack200 Tools and API
- 新的Epsilon垃圾收集器
- 完全支持Linux容器（包括Docker）
- 支持G1上的并行完全垃圾收集
- 最新的HTTPS安全协议TLS 1.3
- Java Flight Recorder

#### 在当前JDK中看不到什么？

> 一个标准化和轻量级的JSON API

- 一个标准化和轻量级的JSONAPI被许多Java开发人员所青睐。但是由于资金问题无法在Java当前版本中见到，但并不会削减掉。Java平台首席架构师MarkReinhold在JDK9邮件列中说：“这个JEP将是平台上的一个有用的补充，但是在计划中，它并不像Oracle资助的其他功能那么重要，可能会重新考虑JDK10或更高版本中实现。”

> 新的货币API

- 对许多应用而言货币价值都是一个关键的特性，但JDK对此却几乎没有任何支持。严格来讲，现有的java.util.Currency类只是代表了当前ISO4217货币的一个数据结构，但并没有关联的值或者自定义货币。JDK对货币的运算及转换也没有内建的支持，更别说有一个能够代表货币值的标准类型了。
- 此前，Oracle公布的JSR354定义了一套新的Java货币API：JavaMoney，计划会在Java9中正式引入。但是目前没有出现在JDK新特性中。
- 不过，如果你用的是Maven的话，可以做如下的添加，即可使用相关的API处理货币：

```java
<dependency>
    <groupId>org.javamoney</groupId>
    <artifactId>moneta</artifactId>
    <version>0.9</version>
</dependency>
```

## Java 12&13&14 的新特性

> Java开发在目前开发中，仍多数以JDK8为主，JDK12-14是2019年2月7日——2020年3月17日发布。所以，就目前时间而言，对于初学者就不做深入学习，因为目前普遍仍以JDK8为主。若有需要，自行了解。以下是相关课件视频链接：

[https://www.yuque.com/nizhegechouloudetuboshu/library/mlenxx](https://www.yuque.com/nizhegechouloudetuboshu/library/mlenxx)

- Java12&13视频链接：https://www.bilibili.com/video/BV1jJ411M7kQ

- Java14视频链接：https://www.bilibili.com/video/BV1tC4y147US