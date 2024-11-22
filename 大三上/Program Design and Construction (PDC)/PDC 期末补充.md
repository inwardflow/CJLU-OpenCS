# PDC 期末补充

> [!Note]
>
> 本文档只是补充了一些代码，请严格按照 PPT 进行复习！

### 请解释 Java 中的封装、继承和多态的概念

**封装 (Encapsulation)**：将数据（变量）和操作数据的函数（方法）结合在一起，隐藏数据的内部实现细节。

**继承 (Inheritance)**：一种通过已有的类创建新类的方式，新类继承了现有类的属性和行为，并可以添加新的属性和行为。

**多态 (Polymorphism)**：指同一接口或方法在不同的类或对象上的表现形式或行为。



### 详解 interrupt、interrupted 和 isInterrupted 方法之间的区别

interrupt：用于中断线程。调用该方法的线程的状态将会被设置为“中断状态”。 

【注意】线程中断仅仅是设置线程的中断状态位，**并不会停止线程**，需要用户自己去监视线程的状态并作出处理。

[阅读材料](https://www.jb51.net/program/308109s0w.htm)



### Fundamental OO Concepts

* **Encapsulation**: Making the **fields** in a class **private** and providing access to the fields via public methods. (**Getters and Setters**)
* **Abstraction**: is to provide essential **general** features without providing implementation details <u>using abstract class or an interface</u>.
* **Inheritance**: when a class wants to **inherit** the features of another existing class. It enables <u>reuse of previous code and solution</u>.
* **Polymorphism**: is the ability of an object to take on many forms. The most common use of polymorphism in OOP occurs when a parent class reference is used to refer to a child class object. 多态是指同一个接口或方法可以<u>根据调用对象的不同而表现出不同的行为</u>。在面向对象编程中，多态通常通过**方法重写**（即子类覆盖父类的方法）来实现。



### Class Relationships

关联（Association）、聚合（Aggregation）、组合（Composition） 和 继承（Inheritance） 

接下来，我们按照条件，从宽松到严格，逐一介绍这四个关系。

* 关联（Association）：对象之间的连接关系，可以是单向的、双向的或多对多的。
* 聚合（Aggregation）：表示“整体-部分”关系，部分**可以独立**于整体存在。
* 组合（Composition）：表示“整体-部分”关系，部分**不能独立**于整体存在。
* 继承（Inheritance）：表示“is-a”关系，子类从父类派生，继承父类的属性和方法。

#### 1. 关联（Association）

在数据库中，可以使用 student_id 和 course_id 建表，来存储它们之间的映射关系。

假设有一个 Student 类和一个 Course 类，一个学生**可以选修多个**课程，一个课程也**可以被多个学生选修**。这可以用关联来表示。

```java
public class Student {
	private String name;
	private List<Course> courses;
    public Student(String name) {
        this.name = name;
        this.courses = new ArrayList<>();
    }

    public void enroll(Course course) {
        this.courses.add(course);
        course.getStudents().add(this);
    }

    public String getName() {
        return name;
    }

    public List<Course> getCourses() {
        return courses;
    }
}
```
```java
public class Course {
    private String title;
    private List<Student> students;
    public Course(String title) {
        this.title = title;
        this.students = new ArrayList<>();
    }

    public void addStudent(Student student) {
        this.students.add(student);
    }

    public String getTitle() {
        return title;
    }

    public List<Student> getStudents() {
        return students;
    }
}
```
#### 2. 聚合（Aggregation）

是一种**「整体-部分」**关系。假设有一个 Department 类和一个 Employee 类，一个部门可以有多个员工，但员工可以在没有部门的情况下独立存在。这可以用聚合来表示。

```java
public class Employee {
    private String name;

    public Employee(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }
}

public class Department {
    private String name;
    private List<Employee> employees;
    public Department(String name) {
        this.name = name;
        this.employees = new ArrayList<>();
    }

    public void addEmployee(Employee employee) {
        this.employees.add(employee);
    }

    public String getName() {
        return name;
    }

    public List<Employee> getEmployees() {
        return employees;
    }
}
```
#### 3. 组合（Composition）

假设有一个 House 类和一个 Room 类，一个房子由多个房间组成，但房间不能独立于房子存在。这可以用组合来表示。

```java
public class Room {
    private String name;
    
    public Room(String name) {
        this.name = name;
	}

    public String getName() {
        return name;
	}
}

public class House {
    private String address;
    private List<Room> rooms;
    
    public House(String address) {
        this.address = address;
        this.rooms = new ArrayList<>();
    }

    public void addRoom(Room room) {
        this.rooms.add(room);
    }

    public String getAddress() {
        return address;
    }

    public List<Room> getRooms() {
        return rooms;
    }
}
```
#### 4. 继承（Inheritance）

假设有一个 Animal 类和它的两个子类 Dog 和 Cat。

```java
public class Animal {
private String name;
	public Animal(String name) {
        this.name = name;
    }
    public void makeSound() {
        System.out.println("Some generic sound");
    }
    public String getName() {
        return name;
    }
}

public class Dog extends Animal {
    public Dog(String name) {
        super(name);
    }

    @Override
    public void makeSound() {
        System.out.println("Bark");
    }
}

public class Cat extends Animal {
    public Cat(String name) {
        super(name);
    }

    @Override
    public void makeSound() {
        System.out.println("Meow");
    }
}
```

### SOLID Principles

#### 1. Single Responsibility Principle, SRP

> "A CLASS SHOULD HAVE ONLY ONE REASON TO CHANGE."

单一职责原则，一个类应该只有一个改变的理由，即一个类应该只有一个职责。

#### 2. Open/Closed Principle, OCP

> "SOFTWARE ENTITIES (CLASSES, MODULES, FUNCTIONS, etc.) SHOULD BE OPEN FOR EXTENSION BUT CLOSED FOR MODIFICATION."

开闭原则，对扩展开放，对修改关闭。

#### 3. Liskov Substitution Principle, LSP

> "SUB CLASSES SHOULD BEHAVE NICELY WHEN USED IN PLACE OF THEIR BASE CLASS."

里氏替换原则，子类型必须能够替换它们的基类型。

```java
// 违反LSP
public class Bird {
    public void fly() {
        // 飞行逻辑
    }
}

public class Penguin extends Bird {
    @Override
    public void fly() {
        throw new UnsupportedOperationException("企鹅不会飞");
    }
}

// 符合LSP
public interface Flyable {
    void fly();
}

public class Bird implements Flyable {
    @Override
    public void fly() {
        // 飞行逻辑
    }
}

public class Penguin {
    public void swim() {
        // 游泳逻辑
    }
}
```

#### 4. Interface Segregation Principle, ISP

> “A CLIENT SHOULD NEVER BE FORCED TO IMPLEMENT AN INTERFACE THAT IT DOESN'T USE OR CLIENTS SHOULDN'T BE FORCED TO DEPEND ON METHODS THEY DON'T USE."

接口隔离原则，客户端不应该被迫依赖于它们不使用的接口。

一个类对另一个类的依赖应该建立在最小的接口上。

如果一个接口太大，<u>应该将其拆分为更小的接口</u>，以便客户端**只依赖于**它们实际使用的接口。

#### 5. Dependency Inversion Principle, DIP

> “HIGH-LEVEL MODULES SHOULD NOT DEPEND ON LOW-LEVEL MODULES. BOTH SHOULD DEPEND ON ABSTRACTIONS. ABSTRACTIONS SHOULD NOT DEPEND ON DETAILS. DETAILS SHOULD DEPEND ON ABSTRACTIONS."

依赖倒置原则，高层模块不应该依赖低层模块，两者都应该依赖于抽象。抽象不应该依赖于细节，细节应该依赖于抽象。



### 设计模式 (Design Patterns)

#### 单例模式 (Singleton Pattern)

确保一个类只有一个实例，并提供一个全局访问点。

[五种单例模式详解](https://blog.csdn.net/weixin_46456187/article/details/142821988)

[菜鸟教程：设计模式大全](https://www.runoob.com/design-pattern/design-pattern-tutorial.html)

##### 饿汉式

饿汉式的实现方式，在类加载的期间，就已经将 `instance` 静态实例初始化好了，所以，instance 实例的创建是线程安全的。不过，这样的实现方式不支持延迟加载实例。

##### 懒汉式

相对于饿汉式的优势是支持延迟加载。这种实现方式会导致频繁加锁、释放锁，以及并发度低等问题，频繁的调用会产生性能瓶颈。

##### 双重检测

双重检测实现方式既支持延迟加载、又支持高并发的单例实现方式。只要 instance 被创建之后，再调用 `getInstance()` 函数都不会进入到加锁逻辑中。所以，这种实现方式解决了懒汉式并发度低的问题。

##### 静态内部类

利用 Java 的静态内部类来实现单例。这种实现方式，既支持延迟加载，也支持高并发，实现起来也比双重检测简单。

##### 枚举方式

最简单的实现方式，基于枚举类型的单例实现。这种实现方式通过 Java 枚举类型本身的特性，保证了实例创建的线程安全性和实例的唯一性(同时阻止了反射和序列化对单例的破坏)。

下面贴出**双重检测单例模式**的代码：

```java
public class Singleton {
    private volatile static Singleton instance;

    // 私有构造方法，防止外部实例化
    private Singleton() {}

    public static Singleton getInstance() {
        if (instance == null) {
            synchronized (Singleton.class) {
                if (instance == null) {
                    instance = new Singleton();
                }
            }
        }
        return instance;
    }
}
```

#### 适配器模式 (Adapter Pattern)

使接口不兼容的类能够一起工作。

```java
interface Target {
    void request();
}

class Adaptee {
    public void specificRequest() {
        System.out.println("Specific Request");
    }
}

class Adapter implements Target {
    private Adaptee adaptee;

    public Adapter(Adaptee adaptee) {
        this.adaptee = adaptee;
    }

    @Override
    public void request() {
        adaptee.specificRequest();
    }
}
```

#### 观察者模式 (Observer Pattern)

定义了一种一对多的依赖关系，当一个对象的状态改变时，所有依赖于它的对象都会得到通知。

```java
import java.util.ArrayList;
import java.util.List;

interface Observer {
    void update(String message);
}

class Subject {
    private List<Observer> observers = new ArrayList<>();

    public void addObserver(Observer observer) {
        observers.add(observer);
    }

    public void removeObserver(Observer observer) {
        observers.remove(observer);
    }

    public void notifyObservers(String message) {
        for (Observer observer : observers) {
            observer.update(message);
        }
    }
}

class ConcreteObserver implements Observer {
    @Override
    public void update(String message) {
        System.out.println("Received: " + message);
    }
}
```



### **MVC 架构**

MVC（Model-View-Controller）是一种常用的架构风格，将应用程序分为三个主要部分：

* **Model**: 处理数据逻辑
* **View**: 处理显示逻辑
* **Controller**: 处理用户输入

MVVM 是 `Model-View-ViewModel` 的简写。它本质上就是[MVC](https://baike.baidu.com/item/MVC/85990?fromModule=lemma_inlink)的改进版。

MVVM 模式有助于将应用程序的业务和表示逻辑与[用户界面](https://baike.baidu.com/item/用户界面/6582461?fromModule=lemma_inlink) (UI) 清晰分离。

保持应用程序逻辑和 UI 之间的清晰分离有助于解决许多开发问题，并使应用程序更易于测试、维护和演变。 它还可以显著提高代码重用机会，并允许开发人员和[UI设计](https://baike.baidu.com/item/UI设计/750896?fromModule=lemma_inlink)人员在开发应用各自的部分时更轻松地进行协作。



### Verification vs. Validation

**Verification** 是确保**软件开发过程**中的每个步骤都按计划进行，关注的是<u>内部的一致性和正确性</u>。

**Validation** 是确保**最终产品**满足用户的**需求和期望**，关注的是<u>外部的有效性和适用性</u>。

#### 总结

**Verification** 是“做事情的正确方式”，确保每个环节都符合标准。

**Validation** 是“做正确的事情”，确保最终产品满足用户需求。



### JUnit Tests

**@Test**：标记一个方法为测试方法。

**@Before**：在每个测试方法之前运行。

**@After**：在每个测试方法之后运行。

**@BeforeClass**：在所有测试方法之前运行一次，通常用于初始化静态资源。

**@AfterClass**：在所有测试方法之后运行一次，通常用于清理静态资源。

**@Ignore**：标记一个测试方法被忽略，不会被执行。