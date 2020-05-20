@[TOC]
> 全部源码：https://github.com/name365/JavaSE-30Day
# 项目三 开发团队调度软件
## 目标
- 模拟实现一个基于文本界面的《开发团队调度软件》
- 熟悉Java面向对象的高级特性，进一步掌握编程技巧和调试技巧
- 主要涉及以下知识点：
  - 类的继承性和多态性
  - 对象的值传递、接口
  - static和final修饰符
  - 特殊类的使用：包装类、抽象类、内部类
  - 异常处理

## 需求说明
- 该软件实现以下功能：
  - 软件启动时，根据给定的数据创建公司部分成员列表（数组）
  - 根据菜单提示，基于现有的公司成员，组建一个开发团队以开发一个新的项目
  - 组建过程包括将成员插入到团队中，或从团队中删除某成员，还可以列出团队中现有成员的列表
  - 开发团队成员包括架构师、设计师和程序员

- 本软件采用单级菜单方式工作。当软件运行时，主界面显示公司成员的列表，如下：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200506225503805.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzQ2MTUzOTQ5,size_16,color_FFFFFF,t_70#pic_center)

- 当选择“添加团队成员”菜单时，将执行从列表中添加指定（通过ID）成员到开发团队的功能：

![在这里插入图片描述](https://img-blog.csdnimg.cn/2020050622564845.jpg#pic_center)

- 添加成功后，按回车键将重新显示主界面。

- 开发团队人员组成要求：
  - 最多一名架构师
  - 最多两名设计师
  - 最多三名程序员

- 如果添加操作因某种原因失败，将显示类似以下信息（失败原因视具体原因而不同）：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200506225708965.jpg#pic_center)

- 失败信息包含以下几种：
  - 成员已满，无法添加
  - 该成员不是开发人员，无法添加
  - 该员工已在本开发团队中
  - 该员工已是某团队成员–该员正在休假，无法添加
  - 团队中至多只能有一名架构师
  - 团队中至多只能有两名设计师
  - 团队中至多只能有三名程序员

- 当选择“删除团队成员”菜单时，将执行从开发团队中删除指定（通过TeamID）成员的功能：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200506225726513.jpg#pic_center)

- 删除成功后，按回车键将重新显示主界面。

- 当选择“团队列表”菜单时，将列出开发团队中的现有成员，例如：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200506225743452.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzQ2MTUzOTQ5,size_16,color_FFFFFF,t_70#pic_center)
## 软件设计结构

- 该软件由以下三个模块组成：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200506225757227.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzQ2MTUzOTQ5,size_16,color_FFFFFF,t_70#pic_center)

- github.view模块为主控模块，负责菜单的显示和处理用户操作
- github.service模块为实体对象（Employee及其子类如程序员等）的管理模块，NameListService和TeamService类分别用各自的数组来管理公司员工和开发团队成员对象
- domain模块为Employee及其子类等JavaBean类所在的包

- github.domain模块中包含了所有实体类：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200506225813712.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzQ2MTUzOTQ5,size_16,color_FFFFFF,t_70#pic_center)

- 其中程序员(Programmer)及其子类，均会领用某种电子设备(Equipment)。

## 第1步—创建项目基本组件
1. 完成以下工作：
   1. 创建TeamSchedule项目
   2. 按照设计要求，创建所有包
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200506225900167.png#pic_center)

   3. 将项目提供的几个类复制到相应的包中(view包中：TSUtility.java;   service包中：Data.java)

- TSUtility.java

```java
import java.util.*;

/**
  * 
  * @Description 项目中提供了TSUtility.java类，可用来方便地实现键盘访问。
  * @author subei Email:subei@163.com
  * @version
  * @date 2020年5月6日下午3:10:30
  *
 */
public class TSUtility {
    private static Scanner scanner = new Scanner(System.in);
   /**
     * 
     * @Description 该方法读取键盘，如果用户键入’1’-’4’中的任意字符，则方法返回。返回值为用户键入字符。
     * @author subei
     * @date 2020年5月6日下午3:10:48
     * @return
    */
	public static char readMenuSelection() {
        char c;
        for (; ; ) {
            String str = readKeyBoard(1, false);
            c = str.charAt(0);
            if (c != '1' && c != '2' &&
                c != '3' && c != '4') {
                System.out.print("选择错误，请重新输入：");
            } else break;
        }
        return c;
    }
	/**
	  * 
	  * @Description 该方法提示并等待，直到用户按回车键后返回。
	  * @author subei
	  * @date 2020年5月6日下午3:11:04
	 */
    public static void readReturn() {
        System.out.print("按回车键继续...");
        readKeyBoard(100, true);
    }
    /**
      * 
      * @Description 该方法从键盘读取一个长度不超过2位的整数，并将其作为方法的返回值。
      * @author subei
      * @date 2020年5月6日下午3:11:17
      * @return
     */
    public static int readInt() {
        int n;
        for (; ; ) {
            String str = readKeyBoard(2, false);
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
      * 
      * @Description 从键盘读取‘Y’或’N’，并将其作为方法的返回值。
      * @author subei
      * @date 2020年5月6日下午3:11:33
      * @return
     */
    public static char readConfirmSelection() {
        char c;
        for (; ; ) {
            String str = readKeyBoard(1, false).toUpperCase();
            c = str.charAt(0);
            if (c == 'Y' || c == 'N') {
                break;
            } else {
                System.out.print("选择错误，请重新输入：");
            }
        }
        return c;
    }

    private static String readKeyBoard(int limit, boolean blankReturn) {
        String line = "";

        while (scanner.hasNextLine()) {
            line = scanner.nextLine();
            if (line.length() == 0) {
                if (blankReturn) return line;
                else continue;
            }

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

- Data.java

```java
public class Data {
    public static final int EMPLOYEE = 10;
    public static final int PROGRAMMER = 11;
    public static final int DESIGNER = 12;
    public static final int ARCHITECT = 13;

    public static final int PC = 21;
    public static final int NOTEBOOK = 22;
    public static final int PRINTER = 23;

    //Employee  :  10, id, name, age, salary
    //Programmer:  11, id, name, age, salary
    //Designer  :  12, id, name, age, salary, bonus
    //Architect :  13, id, name, age, salary, bonus, stock
    public static final String[][] EMPLOYEES = {
        {"10", "1", "马云", "22", "3000"},
        {"13", "2", "马化腾", "32", "18000", "15000", "2000"},
        {"11", "3", "李彦宏", "23", "7000"},
        {"11", "4", "刘强东", "24", "7300"},
        {"12", "5", "雷军", "28", "10000", "5000"},
        {"11", "6", "任志强", "22", "6800"},
        {"12", "7", "柳传志", "29", "10800","5200"},
        {"13", "8", "杨元庆", "30", "19800", "15000", "2500"},
        {"12", "9", "史玉柱", "26", "9800", "5500"},
        {"11", "10", "丁磊", "21", "6600"},
        {"11", "11", "张朝阳", "25", "7100"},
        {"12", "12", "杨致远", "27", "9600", "4800"}
    };
    
    //如下的EQIPMENTS数组与上面的EMPLOYEES数组元素一一对应
    //PC      :21, model, display
    //NoteBook:22, model, price
    //Printer :23, type, name
    public static final String[][] EQIPMENTS = {
        {},
        {"22", "联想T4", "6000"},
        {"21", "戴尔", "NEC17寸"},
        {"21", "戴尔", "三星 17寸"},
        {"23", "激光", "佳能 2900"},
        {"21", "华硕", "三星 17寸"},
        {"21", "华硕", "三星 17寸"},
        {"23", "针式", "爱普生20K"},
        {"22", "惠普m6", "5800"},
        {"21", "戴尔", "NEC 17寸"},
        {"21", "华硕","三星 17寸"},
        {"22", "惠普m6", "5800"}
    };
}
```

2. 按照设计要求，在github.domain包中，创建Equipment接口及其各实现子类代码
3. 按照设计要求，在github.domain包中，创建Employee类及其各子类代码
4. 检验代码的正确性

### Equipment接口及其实现子类的设计
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200506230142332.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzQ2MTUzOTQ5,size_16,color_FFFFFF,t_70#pic_center)

- 说明：
  - model 表示机器的型号
  - display 表示显示器名称
  - type 表示机器的类型

- 根据需要提供各属性的get/set方法以及重载构造器
- 实现类实现接口的方法，返回各自属性的信息

- Equipment类

```java
public interface Equipment {
	String getDescription();
}
```

- PC类

```java
public class PC implements Equipment{

	private String model;	//表示机器的型号
	private String display;	//表示显示器名称
	@Override
	public String getDescription() {
		return model + "(" + display + ")";
	}
	public String getModel() {
		return model;
	}
	public void setModel(String model) {
		this.model = model;
	}
	public String getDisplay() {
		return display;
	}
	public void setDisplay(String display) {
		this.display = display;
	}
	public PC() {
		super();
	}
	public PC(String model, String display) {
		super();
		this.model = model;
		this.display = display;
	}
	
}
```

- Printer类

```java
public class Printer implements Equipment{

	private String name;	//表示机器的名称
	private String type;	//表示机器的类型
	
	public String getName() {
		return name;
	}
	
	public void setName(String name) {
		this.name = name;
	}
	
	public String getType() {
		return type;
	}
	
	public void setType(String type) {
		this.type = type;
	}

	@Override
	public String getDescription() {
		return name + "(" + type + ")";
	}

	public Printer() {
		super();
	}

	public Printer(String name, String type) {
		super();
		this.name = name;
		this.type = type;
	}
		
}
```

- NoteBook类

```java
public class NoteBook implements Equipment{

	private String model;//表示机器的型号
	private double price;//表示价格
	
	@Override
	public String getDescription() {
		return model + "(" + price + ")";
	}
	
	public String getModel() {
		return model;
	}

	public void setModel(String model) {
		this.model = model;
	}

	public double getPrice() {
		return price;
	}

	public void setPrice(double price) {
		this.price = price;
	}
	
	public NoteBook() {
		super();
	}

	public NoteBook(String model, double price) {
		super();
		this.model = model;
		this.price = price;
	}
		
}
```

### Employee类及其子类的设计
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200506230215667.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzQ2MTUzOTQ5,size_16,color_FFFFFF,t_70#pic_center)

**说明**

- memberId用来记录成员加入开发团队后在团队中的ID
- Status是项目service包下自定义的类，声明三个对象属性，分别表示成员的状态。
  - FREE-空闲
  - BUSY-已加入开发团队
  - VOCATION-正在休假
- equipment 表示该成员领用的设备
- 可根据需要为类提供各属性的get/set方法以及重载构造器

- Employee类

```java
public class Employee {
    private int id;
    private String name;
    private int age;
    private double salary;

    public Employee() {
    }

    public Employee(int id, String name, int age, double salary) {
        this.id = id;
        this.name = name;
        this.age = age;
        this.salary = salary;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public double getSalary() {
        return salary;
    }

    public void setSalary(double salary) {
        this.salary = salary;
    }

    protected String getDetails() {
        return id + "\t" + name + "\t" + age+ "\t" +salary;
    }

    @Override
    public String toString() {
        return getDetails();
    }
}
```

- Programer类

```java
import github.service.Status;

public class Programer extends Employee {
	private int memberId;
	private Status status = Status.FREE;
	private Equipment equipment;

	public Programer() {
	}

	public Programer(int id, String name, int age, double salary, Equipment equipment) {
		super(id, name, age, salary);
		this.equipment = equipment;
	}

	public Status getStatus() {
		return status;
	}

	public void setStatus(Status status) {
		this.status = status;
	}

	public Equipment getEquipment() {
		return equipment;
	}

	public void setEquipment(Equipment equipment) {
		this.equipment = equipment;
	}

	public int getMemberId() {
		return memberId;
	}

	public void setMemberId(int memberId) {
		this.memberId = memberId;
	}

	protected String getMemberDetails() {
		return getMemberId() + "/" + getDetails();
	}

	public String getDetailsForTeam() {
		return getMemberDetails() + "\t程序员";
	}

	@Override
	public String toString() {
		return getDetails() + "\t程序员\t" + status + "\t\t\t" + equipment.getDescription();
	}
}
```

- Status类
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200506230232377.jpg#pic_center)

```java
/**
  * 
  * @Description 表示员工的状态
  * @author subei Email:subei@163.com
  * @version
  * @date 2020年5月6日下午5:09:18
  *
 */
public class Status {
	
	private final String NAME;
	private Status(String name) {
		this.NAME = name;
	}
	public static final Status FREE = new Status("FREE");
	public static final Status VOCATION = new Status("VOCATION");
	public static final Status BUSY = new Status("BUSY");
	public String getNAME() {
		return NAME;
	}
	@Override
	public String toString() {
		return NAME;
	}
	
}
```

### Employee类及其子类的设计
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200506230248973.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzQ2MTUzOTQ5,size_16,color_FFFFFF,t_70#pic_center)

- 说明：
  - bonus表示奖金
  - stock 表示公司奖励的股票数量
- 可根据需要为类提供各属性的get/set方法以及重载构造器

- Designer类

```java
public class Designer extends Programer {
	private double bonus; // 表示奖金

	public Designer() {
		super();
	}

	public Designer(int id, String name, int age, double salary, Equipment equipment, double bonus) {
		super(id, name, age, salary, equipment);
		this.bonus = bonus;
	}

	public double getBonus() {
		return bonus;
	}

	public void setBonus(double bonus) {
		this.bonus = bonus;
	}

	public String getDetailsForTeam() {
        return getMemberDetails() + "\t设计师\t" + getBonus();
    }

    @Override
    public String toString() {
        return getDetails() + "\t设计师\t" + getStatus() + "\t" +
               getBonus() +"\t\t" + getEquipment().getDescription();
    }
}
```

- Architect类

```java
public class Architect extends Designer {
	private int stock; // 表示公司奖励的股票数量

	public Architect() {
		super();
	}

	public Architect(int id, String name, int age, double salary, Equipment equipment, double bonus, int stock) {
		super(id, name, age, salary, equipment, bonus);
		this.stock = stock;
	}

	public int getStock() {
		return stock;
	}

	public void setStock(int stock) {
		this.stock = stock;
	}

	public String getDetailsForTeam() {
        return getMemberDetails() + "\t架构师\t" + 
               getBonus() + "\t" + getStock();
    }

    @Override
    public String toString() {
        return getDetails() + "\t架构师\t" + getStatus() + "\t" +
               getBonus() + "\t" + getStock() + "\t" + getEquipment().getDescription();
    }
}
```

## 第2步—实现service包中的类

1. 按照设计要求编写NameListService类
2. 在NameListService类中临时添加一个main方法中，作为单元测试方法。
3. 在方法中创建NameListService对象，然后分别用模拟数据调用该对象的各个方法，以测试是否正确。注：测试应细化到包含了所有非正常的情况，以确保方法完全正确。
4. 重复1-3步，完成TeamService类的开发

### NameListService类的设计
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200506230304938.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzQ2MTUzOTQ5,size_16,color_FFFFFF,t_70#pic_center)

- 功能：负责将Data中的数据封装到Employee[]数组中，同时提供相关操作Employee[]的方法。
- 说明：
  - employees用来保存公司所有员工对象
  - NameListService()构造器：
    - 根据项目提供的Data类构建相应大小的employees数组
    - 再根据Data类中的数据构建不同的对象，包括Employee、Programmer、Designer和Architect对象，以及相关联的Equipment子类的对象
    - 将对象存于数组中
    - Data类位于com.atguigu.team.service包中
    - getAllEmployees ()方法：获取当前所有员工。
      - 返回：包含所有员工对象的数组
    - getEmployee(id : int)方法：获取指定ID的员工对象。
      - 参数：指定员工的ID
      - 返回：指定员工对象
      - 异常：找不到指定的员工
    - 在service子包下提供自定义异常类：TeamException
    - 另外，可根据需要自行添加其他方法或重载构造器

- NameListService类

```java
import github.domain.*;
import static github.service.Data.*;
/**
 * 
 * @Description 负责将Data中的数据封装到Employee[]数组中，同时提供相关操作Employee[]的方法。
 * @author subei Email:subei@163.com
 * @version v1.0
 * @date 2020年5月6日下午5:42:19
 *
 */
public class NameListService {
	private Employee[] employees;

	/**
	 * 给employees及数组元素进行初始化
	 */
	public NameListService() {
		/*
		 * 1.根据项目提供的Data类构建相应大小的employees数组
		 * 2.再根据Data类中的数据构建不同的对象，包括Employee、Programmer、Designer
		 * 和Architect对象，以及相关联的Equipment子类的对象 3.将对象存于数组中
		 */
		employees = new Employee[EMPLOYEES.length];

		for (int i = 0; i < employees.length; i++) {
			// 获取员工的类型
			int type = Integer.parseInt(EMPLOYEES[i][0]);
			//获取employee的4个基本信息
			int id = Integer.parseInt(EMPLOYEES[i][1]);
			String name = EMPLOYEES[i][2];
			int age = Integer.parseInt(EMPLOYEES[i][3]);
			double salary = Double.parseDouble(EMPLOYEES[i][4]);
			
			//
			Equipment eq;
			double bonus;
			int stock;
			
			switch(type){
			case EMPLOYEE:
				employees[i] = new Employee(id, name, age, salary);
				break;
			case PROGRAMMER:
				eq = createEquipment(i);
				employees[i] = new Programer(id, name, age, salary, eq);
				break;
			case DESIGNER:
				eq = createEquipment(i);
				bonus = Integer.parseInt(EMPLOYEES[i][5]);
				employees[i] = new Designer(id, name, age, salary, eq, bonus);
				break;
			case ARCHITECT:
				eq = createEquipment(i);
				bonus = Integer.parseInt(EMPLOYEES[i][5]);
				stock = Integer.parseInt(EMPLOYEES[i][6]);
				employees[i] = new Architect(id, name, age, salary, eq, bonus,
						stock);
				break;
			}
		}
	}

	/**
	  * 
	  * @Description 获取指定index上的员工的设备
	  * @author subei
	  * @date 2020年5月6日下午6:15:23
	  * @param i
	  * @return
	 */
	private Equipment createEquipment(int index) {
		int type = Integer.parseInt(EQIPMENTS[index][0]);
		switch (type) {
		case PC:
			return new PC(EQIPMENTS[index][1], EQIPMENTS[index][2]);
		case NOTEBOOK:
			int price = Integer.parseInt(EQIPMENTS[index][2]);
			return new NoteBook(EQIPMENTS[index][1], price);
		case PRINTER:
			return new Printer(EQIPMENTS[index][1], EQIPMENTS[index][2]);
		}
		return null;
	}

	/**
	  * 
	  * @Description 获取当前所有员工。
	  * @author subei
	  * @date 2020年5月6日下午8:22:47
	  * @return
	 */
	public Employee[] getAllEmployees() {
		return employees;
	}

	/**
	  * 
	  * @Description 获取指定ID的员工对象。
	  * @author subei
	  * @date 2020年5月6日下午8:26:12
	  * @param id
	  * @return
	 * @throws TeamException 
	 */
	public Employee getEmployee(int id) throws TeamException{
		for(Employee e : employees){
			if(e.getId() == id){
				return e;
			}
		}		
		throw new TeamException("找不到指定的员工");
	}
}
```

- TeamException类

```java
/**
  * 
  * @Description 自定义异常类
  * @author subei Email:subei@163.com
  * @version
  * @date 2020年5月6日下午8:29:54
  *
 */
public class TeamException extends Exception{
	static final long serialVersionUID = -33875169124229948L;
	
	public TeamException(){
		super();
	}
	
	public TeamException(String img){
		super(img);
	}
}
```

- NameListServiceTest类——测试NameListService类

```java
import org.junit.Test;
import github.domain.Employee;
import github.service.NameListService;
import github.service.TeamException;
/**
  * 
  * @Description 对NameListService类的测试
  * @author subei Email:subei@163.com
  * @version
  * @date 2020年5月6日下午8:37:51
  *
 */
public class NameListServiceTest {

	@Test
	public void testGetAllEmployees(){
		NameListService service = new NameListService();
		Employee[] employees = service.getAllEmployees();
		for(int i = 0;i < employees.length;i++){
			System.out.println(employees[i]);
		}
	}
	
	@Test
	public void testGetEmployee(){
		int id = 101;
		NameListService listService = new NameListService();
		try {
			Employee emp = listService.getEmployee(id);
			System.out.println(emp);
		} catch (TeamException e) {
			System.out.println(e.getMessage());
		}
	}
}
```

### TeamService类的设计
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200506230323862.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzQ2MTUzOTQ5,size_16,color_FFFFFF,t_70#pic_center)

- 功能：关于开发团队成员的管理：添加、删除等。
- 说明：
  - counter为静态变量，用来为开发团队新增成员自动生成团队中的唯一ID，即memberId。（提示：应使用增1的方式）
  - MAX_MEMBER：表示开发团队最大成员数
  - team数组：用来保存当前团队中的各成员对象
  - total：记录团队成员的实际人数
  - getTeam()方法：返回当前团队的所有对象
    - 返回：包含所有成员对象的数组，数组大小与成员人数一致
  - addMember(e: Employee)方法：向团队中添加成员
    - 参数：待添加成员的对象
    - 异常：添加失败，TeamException中包含了失败原因
  - removeMember(memberId: int)方法：从团队中删除成员
    - 参数：待删除成员的memberId
    - 异常：找不到指定memberId的员工，删除失败
- 另外，可根据需要自行添加其他方法或重载构造器

```java
import github.domain.Architect;
import github.domain.Designer;
import github.domain.Employee;
import github.domain.Programer;
/**
  * 
  * @Description 关于开发团队成员的管理：添加、删除等。
  * @author subei Email:subei@163.com
  * @version
  * @date 2020年5月6日下午9:14:19
  *
 */
public class TeamService {

	private static int counter = 1;	//为开发团队新增成员自动生成团队中的唯一ID
	private final int MAX_MEMBER = 5;	//限定开发团队的人数
	private Programer[] team = new Programer[MAX_MEMBER];	//用来保存当前团队中的各成员对象
	private static int total = 0;	//记录团队成员的实际人数
	
	public TeamService() {
		super();
	}

	/**
	  * 
	  * @Description 获取当前团队的所有对象,即返回team中所有程序员构成的数组
	  * @author subei
	  * @date 2020年5月6日下午9:19:18
	  * @return
	 */
	public Programer[] getTeam() {
		Programer[] team = new Programer[total];

        for (int i = 0; i < total; i++) {
            team[i] = this.team[i];
        }
		return team;
	}
	
	/**
	  * 
	  * @Description 向团队中添加成员,即将指定员工添加到开发团队中
	  * @author subei
	  * @date 2020年5月6日下午9:23:06
	  * @param e
	 * @throws TeamException 
	 */
	public void addMember(Employee e) throws TeamException{
//		失败信息包含以下几种：
//		– 成员已满，无法添加
		if(total >= MAX_MEMBER){
			throw new TeamException("成员已满，无法添加");
		}
//		– 该成员不是开发人员，无法添加
		if(!(e instanceof Programer)){
			throw new TeamException("该成员不是开发人员，无法添加");
		}
				
//		– 该员工已在本开发团队中
		if(isExist(e)){
			throw new TeamException("该员工已在本开发团队中");
		}
//		– 该员工已是某团队成员
//		– 该员正在休假，无法添加
		Programer p = (Programer)e;	//一定不会出现类型转化异常:ClassCaseException
		if("BUSY".equalsIgnoreCase(p.getStatus().getNAME())){
			throw new TeamException("该员工已是某团队成员");
		}else if("VOCATION".equalsIgnoreCase(p.getStatus().getNAME())){
			throw new TeamException("该员正在休假，无法添加");
		}		
//		– 团队中至多只能有一名架构师
//		– 团队中至多只能有两名设计师
//		– 团队中至多只能有三名程序员	
		
		//获取team已有成员中架构师，设计师，程序员的人数
		int numOfArch = 0,numOfDes = 0,numOfPro = 0;
		for(int i = 0;i < total;i++){
			if(team[i] instanceof Architect){
				numOfArch++;
			}else if(team[i] instanceof Designer){
				numOfDes++;
			}else if(team[i] instanceof Programer){
				numOfPro++;
			}
		}
		
		//正确的写法
		if(p instanceof Architect){
			if(numOfArch >= 1){
				throw new TeamException("团队中至多只能有一名架构师");
			}
		}else if(p instanceof Designer){
			if(numOfDes >= 2){
				throw new TeamException("团队中至多只能有两名设计师");
			}
		}else if(p instanceof Programer){
			if(numOfPro >= 3){
				throw new TeamException("团队中至多只能有三名程序员");
			}
		}
		
		//错误的写法
//		if(p instanceof Architect && numOfArch >= 1){
//			throw new TeamException("团队中至多只能有一名架构师");
//		}else if(p instanceof Designer && numOfDes >= 2){
//			throw new TeamException("团队中至多只能有两名设计师");
//		}else if(p instanceof Programer && numOfPro >= 3){
//			throw new TeamException("团队中至多只能有三名程序员");
//		}
		
		//p的属性赋值
		p.setStatus(Status.BUSY);
		p.setMemberId(counter++);
		//将p添加到现有的team中
        team[total++] = p;
	}
	
	private boolean isExist(Employee e) {
		for(int i = 0;i < total;i++){
			return team[i].getId() == e.getId();
		}
		return false;
	}

	/**
	  * 
	  * @Description 从团队中删除成员,即删除指定memberId的程序员
	  * @author subei
	  * @date 2020年5月6日下午9:23:44
	  * @param memberId
	 * @throws TeamException 
	 */
	public void removeMember(int memberId) throws TeamException{
		int n = 0;
        //找到指定memberId的员工，并删除
        for (n = 0; n < total; n++) {
            if (team[n].getMemberId() == memberId) {
                team[n].setStatus(Status.FREE);
                break;
            }
        }
        //如果遍历一遍，都找不到，则报异常
        if (n == total)
            throw new TeamException("找不到该成员，无法删除");
        //后面的元素覆盖前面的元素
        for (int i = n + 1; i < total; i++) {
            team[i - 1] = team[i];
        }
        
        //写法一
//        team[total - 1] = null;
//        total --;
        
        //写法二
        team[--total] = null;       
	}
}
```

## 第3步—实现view包中类

1. 按照设计要求编写TeamView类，逐一实现各个方法，并编译
2. 执行main方法中，测试软件全部功能
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200506230341526.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzQ2MTUzOTQ5,size_16,color_FFFFFF,t_70#pic_center)

- 说明：
  - listSvc和teamSvc属性：供类中的方法使用
  - enterMainMenu()方法：主界面显示及控制方法。
  - 以下方法仅供enterMainMenu()方法调用：
    - listAllEmployees()方法：以表格形式列出公司所有成员
    - getTeam()方法：显示团队成员列表操作
    - addMember()方法：实现添加成员操作
    - deleteMember()方法：实现删除成员操作

```java
import github.domain.Employee;
import github.domain.Programer;
import github.service.NameListService;
import github.service.TeamException;
import github.service.TeamService;

public class TeamView {
	private NameListService listSvc = new NameListService();
	private TeamService teamSvc = new TeamService();

	public void enterMainMenu() {
		boolean loopFlag = true;
		char num = 0;

		while (loopFlag) {
			//小细节
			if (num != '1') {
				listAllEmployees();
			}
			System.out.print("1-团队列表  2-添加团队成员  3-删除团队成员 4-退出   请选择(1-4)：");
			num = TSUtility.readMenuSelection();
			switch (num) {
			case '1':
				getTeam();
				break;
			case '2':
				addMember();
				break;
			case '3':
				deleteMember();
				break;
			case '4':
				System.out.print("确认是否退出(Y/N)：");
				char isExit = TSUtility.readConfirmSelection();
				if (isExit == 'Y')
					loopFlag = false;
				break;
			}
		}
	}

	/**
	 * 
	 * @Description 以表格形式列出公司所有成员
	 * @author subei
	 * @date 2020年5月6日下午10:36:51
	 */
	private void listAllEmployees() {
		System.out.println("\n-------------------------------开发团队调度软件--------------------------------\n");
		Employee[] emps = listSvc.getAllEmployees();
		if (emps == null || emps.length == 0) {
			System.out.println("没有客户记录！");
		} else {
			System.out.println("ID\t姓名\t年龄\t工资\t职位\t状态\t奖金\t股票\t领用设备");
		}

		for (int i = 0;i < emps.length;i++) {
			System.out.println(emps[i]);
		}
		System.out.println("-------------------------------------------------------------------------------");
	}

	/**
	 * 
	 * @Description 显示团队成员列表操作
	 * @author subei
	 * @date 2020年5月6日下午10:37:45
	 */
	private void getTeam() {
//		System.out.println("查看团队开发情况");
		
		System.out.println("\n--------------------团队成员列表---------------------\n");
		Programer[] team = teamSvc.getTeam();
		if (team == null || team.length == 0) {
			System.out.println("开发团队目前没有成员！");
		} else {
			System.out.println("TID/ID\t姓名\t年龄\t工资\t职位\t奖金\t股票");
			for (int i = 0;i < team.length;i++) {
				System.out.println(team[i].getDetailsForTeam());
			}
		}

		System.out.println("-----------------------------------------------------");
	}

	/**
	 * 
	 * @Description 实现添加成员操作
	 * @author subei
	 * @date 2020年5月6日下午10:38:43
	 */
	private void addMember() {
//		System.out.println("添加团队成员");
		
		System.out.println("---------------------添加成员---------------------");
		System.out.print("请输入要添加的员工ID：");
		int id = TSUtility.readInt();

		try {
			Employee emp = listSvc.getEmployee(id);
			teamSvc.addMember(emp);
			System.out.println("添加成功");
		} catch (TeamException e) {
			System.out.println("添加失败，原因：" + e.getMessage());
		}
		// 按回车键继续...
		TSUtility.readReturn();
	}

	/**
	 * 
	 * @Description 实现删除成员操作
	 * @author subei
	 * @date 2020年5月6日下午10:38:28
	 */
	private void deleteMember() {
//		System.out.println("删除团队成员");
		
		System.out.println("---------------------删除成员---------------------");
		System.out.print("请输入要删除员工的TID：");
		int id = TSUtility.readInt();
		System.out.print("确认是否删除(Y/N)：");
		char dn = TSUtility.readConfirmSelection();
		if (dn == 'N'){
			return;
		}
		try {
			teamSvc.removeMember(id);
			System.out.println("删除成功");
		} catch (TeamException e) {
			System.out.println("删除失败，原因：" + e.getMessage());
		}
		// 按回车键继续...
		TSUtility.readReturn();
	}

	public static void main(String[] args) {
		TeamView view = new TeamView();
		view.enterMainMenu();
	}
}
```

- 整体结构
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200506230400234.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzQ2MTUzOTQ5,size_16,color_FFFFFF,t_70#pic_center)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200507000125370.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzQ2MTUzOTQ5,size_16,color_FFFFFF,t_70#pic_center)
## 结束
>>这个项目，先是自己写了一半，就写不下去了。之后看源码，看的似懂非懂，最后又去看视频，看到11:00，然后改bug改了1小时。最终，大体上清楚了，可还是有些地方比较懵。这里记录的是最后的源码，可以运行！！！
>
>> 整个Java全栈系列都是笔者自己敲的笔记。写作不易，如果可以，点个赞呗！✌
