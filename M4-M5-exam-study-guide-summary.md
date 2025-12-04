# M4和M5考试知识点总结
# M4 and M5 Exam Study Guide Summary

## [M4] Design Patterns

### What is a design pattern?
### 什么是设计模式？

**Answer / 答案：**

设计模式是对常见编程问题的流行解决方案的描述（Design patterns are descriptions of popular solutions to commonly-experienced programming problems）。如果实现的是不太方便的解决方案，我们称之为反模式（anti-pattern）（If a less convenient solution has been implemented instead, we call that an anti-pattern）。如果代码显示了反模式，你可以通过重构来实现设计模式来改进代码的设计（If code displays an anti-pattern, you can improve the design of the code by refactoring to implement a design pattern instead）。

设计模式描述的是代码的结构而不是细节（These patterns describe the structure of the code rather than the details）。它们是一种交流设计思想的手段（They are a means of communicating design ideas）。它们不特定于任何单一编程语言（They are not specific to any single programming language），因此UML图可以自然地用来解释设计模式的结构（As such, UML diagrams can naturally be used to explain the structure of a design pattern）。

设计模式的概念最初由Gang of Four（四人帮）在1995年发表（The idea of design patterns was first published by the Gang of Four in 1995）。原书描述了23种模式：11种行为型、5种创建型和7种结构型模式（The original book described 23 patterns: 11 behavioural, 5 creational, and 7 structural patterns）。

设计模式建立在设计原则之上，就像数学定理建立在公理之上一样（Design patterns are built on design principles, just as mathematical theorems are built on axioms）。设计原则（如SOLID）是基础指导原则，它们旨在非常通用（Design principles like SOLID are foundational guidelines that are intended to be quite general）。设计模式是通过将设计原则应用到常见问题而建立的解决方案，它们旨在比其底层原则更实用、更少抽象（Design patterns are established solutions derived from applying design principles to common problems, intended to be more practically applicable and less abstract than their underlying principles）。

---

### Each pattern solves a problem. What problem is solved by each of these patterns and how is it solved?
### 每个模式解决什么问题，如何解决？

#### Creational patterns: Builder, Factory
#### 创建型模式：Builder, Factory

**Factory Pattern（工厂模式）**

**问题（Problem）**：你需要创建都是同一抽象的子类或实现类的对象，但你不想让你的代码依赖于确切的类名或它们是如何构建的（You need to create objects that are all subclasses or implementing classes of the same abstraction, but you don't want your code to depend on the exact class names or how they're built）。

**解决方案（Solution）**：使用一个特殊的"factory"对象或方法，决定创建哪个类并返回一个可直接使用的实例（Use a special "factory" object or method that decides which class to create and returns a ready-to-use instance）。

**Simple Factory（简单工厂）**：使用一个（通常是静态的）方法根据输入参数创建对象（Uses a (usually static) method to create objects based on input parameters）。它可以生成共享共同接口或超类的不同具体类型（It can produce different concrete types that share a common interface or superclass）。

**Abstract Factory（抽象工厂）**：使用组合将实例化逻辑委托给另一个对象（Uses composition to delegate the instantiation logic to another object）。这创建了一个或多个相关对象的家族（This creates a family of one or more related objects）。添加新类型时，只需要添加一个新的工厂子类，而不需要修改现有代码（When adding new types, you add a new factory subclass rather than modifying existing code）。

**Builder Pattern（建造者模式）**

**问题（Problem）**：创建一个具有许多部分或选项的复杂对象会使你的代码混乱且难以阅读（Creating a complex object with many parts or options makes your code messy and hard to read）。

**解决方案（Solution）**：使用一个逐步的"builder"，逐步组装对象，然后给你完成的产品（Use a step-by-step "builder" that assembles the object piece by piece, then gives you the finished product）。

Builder模式的结构（Structure）：
- 创建一个"builder"对象（Create a "builder" object）
- 逐步添加部分（通过多次调用方法，如`append()`或`addHeader()`）（Add parts to it step-by-step by calling methods multiple times）
- 获得最终产品（通过调用builder的`build()`或`toString()`方法）（Get the final product by calling the builder's `build()` or `toString()` method）

你可能在`StringBuilder`和`Okhttp`的`Request.Builder`中见过这个模式（You may recognize this pattern from `StringBuilder` and `Okhttp`'s `Request.Builder`）。

---

#### Behavioural patterns: Strategy, Observer
#### 行为型模式：Strategy, Observer

**Strategy Pattern（策略模式）**

**问题（Problem）**：你有几个算法来完成同一个任务，你想在它们之间轻松切换（You have several algorithms to do the same task, and you want to switch between them easily）。

**解决方案（Solution）**：在每个类中实现每个算法，使它们可以互换，这样你就可以在不改变使用它的代码的情况下改变算法（Implement each algorithm in its own class and make them interchangeable, so that you can change the algorithm without changing the code that uses it）。

例如，考虑一个需要`getDirections`方法的`Map`类，该方法应该根据方向是用于驾驶还是公共交通返回不同的`String`（For example, consider a `Map` class that requires a `getDirections` method, which should return a different `String` depending on whether the directions are for driving or public transit）。我们可以定义一个`DirectionGenerator`接口作为Strategy，让`DrivingDirections`和`TransitDirections`类实现它（We can define a `DirectionGenerator` interface as the Strategy and have classes `DrivingDirections` and `TransitDirections` implement it）。当`Map`类被实例化时，它被赋予一个实现Strategy的对象（When the `Map` class is instantiated, it is given an object implementing the Strategy）。

在UML图中，`Map`是Context（上下文），`DirectionGenerator`是Strategy接口，`DrivingDirections`和`TransitDirections`是Concrete Strategies（具体策略）（In the UML diagram, `Map` is the Context, `DirectionGenerator` is the Strategy interface, and `DrivingDirections` and `TransitDirections` are the Concrete Strategies）。

**Observer Pattern（观察者模式）**

**问题（Problem）**：程序的多个部分需要在对象改变时做出反应，但你不想在这些部分和被观察的对象之间有紧耦合（Multiple parts of your program need to react when an object changes, but you don't want tight coupling between those parts and the object being observed）。

**解决方案（Solution）**：定义一对多的关系：当被观察的对象改变时，所有相关的对象都会收到通知，以便它们可以响应（Define a one-to-many relationship: when the observed object changes, all related objects get notified so that they can respond）。被观察的对象不需要知道观察它的对象的具体细节（The observed object doesn't need to know anything about the specifics of the objects observing it）。

例如，考虑我们附加到`JButton`组件的`ActionListener`对象（For example, consider the `ActionListener` objects that we attach to `JButton` components）。当按钮被点击（事件）时，监听器的`actionPerformed`方法被调用（反应）（When the button is clicked (event), the listener's `actionPerformed` method is called (reaction)）。

在Clean Architecture中，ViewModel是一个Observable，View是一个Observer（In Clean Architecture, a ViewModel is an Observable, and a View is an Observer）。在Java中，这通常通过让Observable使用`java.beans.PropertyChangeSupport`对象来实现，它管理一个`PropertyChangeListener`对象（Observers）列表（In Java, this is usually accomplished by having the Observable use a `java.beans.PropertyChangeSupport` object, which manages a list of `PropertyChangeListener` objects (the Observers)）。

---

#### Structural patterns: Façade, Adapter
#### 结构型模式：Façade, Adapter

**Façade Pattern（外观模式）**

**问题（Problem）**：子系统向客户端暴露许多类和操作，迫使它们处理不必要的复杂性（A subsystem exposes many classes and operations to clients, forcing them to deal with unnecessary complexity）。

**解决方案（Solution）**：创建一个简单的面向客户端的类（façade），为常见任务提供方法，同时隐藏子系统的复杂细节（Create a simple client-facing class (the façade) that provides methods for common tasks while hiding the subsystem's complex details）。

例如，`EmployeeFacade`类包含类型为`EmployeeCalculator`、`EmployeeReporter`和`EmployeeSaver`的变量（For example, the `EmployeeFacade` class contains variables of type `EmployeeCalculator`, `EmployeeReporter`, and `EmployeeSaver`）。当你调用`employee.calculatePay()`时，它通过调用`payCalculator.calculatePay()`来委托工作给相应的对象，这是一个单行委托（When you call `employee.calculatePay()`, it delegates work to one of those three objects using the appropriate private variable, which is a one-line delegation）。

Façade类的方法以相同的方式结构化，它们委托给适当的对象（Façade class methods are structured the same way, they delegate to the appropriate object）。这样，客户端不需要知道底层的复杂性，只需要与简单的Façade接口交互（This way, clients don't need to know the underlying complexity, they only need to interact with the simple Façade interface）。

**Adapter Pattern（适配器模式）**

**问题（Problem）**：两个组件无法一起工作，因为它们的接口不匹配（Two components can't work together because their interfaces don't match）。这通常发生在你需要重用为不同上下文设计的现有类时（This often happens when you need to reuse an existing class that was designed for a different context）。

**解决方案（Solution）**：引入一个adapter（适配器）——一个在预期接口和现有接口之间进行转换的类（Introduce an adapter — a class that translates between the expected interface and the existing one）。适配器暴露你的客户端代码期望的接口，并在内部将调用转发到遗留类，根据需要转换输入和输出（The adapter exposes the interface your client code expects and internally forwards calls to the legacy class, converting inputs and outputs as needed）。

**类比**：想想USB-C转HDMI适配器（Analogy: Think of a USB-C to HDMI adapter）。许多笔记本电脑可以通过USB-C输出视频，但你的显示器只接受HDMI输入（Many laptops can output video through USB-C, but your monitor only accepts HDMI input）。适配器不会改变笔记本电脑或显示器——它只是在两个接口之间进行转换，使它们能够协同工作（The adapter doesn't change the laptop or the monitor — it simply translates between the two interfaces so that they work together）。

Adapter模式可以通过两种方式实现（Adapter pattern can be implemented in two ways）：
- **使用委托（With Delegation）**：适配器持有一个对遗留类的引用，并将工作委托给它（The adapter holds a reference to the legacy class and delegates work to it）
- **使用继承（With Inheritance）**：适配器扩展遗留类并添加代码以与预期接口保持一致（The adapter extends the legacy class and adds code to be consistent with the expected interface）

---

### What are the classes involved in each of the above design patterns and what (if any) is their relationship?
### 每个设计模式涉及哪些类，它们之间有什么关系？

#### Factory Pattern（工厂模式）

**Simple Factory涉及的类（Classes involved）**：
- `ShapeFactory`：工厂类，包含创建方法（Factory class containing creation method）
- `Shape`：抽象产品接口或类（Abstract product interface or class）
- `Rectangle`, `Circle`, `Square`：具体产品类（Concrete product classes）

**关系（Relationships）**：
- `ShapeFactory`依赖`Shape`接口（`ShapeFactory` depends on `Shape` interface）
- `Rectangle`, `Circle`, `Square`实现或继承`Shape`（`Rectangle`, `Circle`, `Square` implement or extend `Shape`）
- 客户端使用`ShapeFactory`来创建`Shape`对象（Client uses `ShapeFactory` to create `Shape` objects）

**Abstract Factory涉及的类（Classes involved）**：
- `ShapeFactory`：抽象工厂类（Abstract factory class）
- `RectangleFactory`, `CircleFactory`, `SquareFactory`：具体工厂类（Concrete factory classes）
- `Shape`：抽象产品（Abstract product）
- `Rectangle`, `Circle`, `Square`：具体产品（Concrete products）

**关系（Relationships）**：
- 具体工厂类继承抽象工厂类（Concrete factory classes extend abstract factory class）
- 每个具体工厂创建对应的具体产品（Each concrete factory creates corresponding concrete products）
- 具体产品实现抽象产品接口（Concrete products implement abstract product interface）

---

#### Builder Pattern（建造者模式）

**涉及的类（Classes involved）**：
- `Builder`：建造者类，包含逐步构建对象的方法（Builder class with methods to build object step by step）
- `Product`：要构建的产品类（Product class to be built）
- `Director`（可选）：指导构建过程的类（Optional: Director class that guides the building process）

**关系（Relationships）**：
- `Builder`负责创建和组装`Product`的各个部分（`Builder` is responsible for creating and assembling parts of `Product`）
- `Builder`有`build()`方法返回最终的`Product`（`Builder` has a `build()` method that returns the final `Product`）
- 客户端使用`Builder`逐步构建对象，然后调用`build()`获得最终产品（Client uses `Builder` to build object step by step, then calls `build()` to get final product）

**例子（Example）**：
- `StringBuilder`是Builder，`String`是Product（`StringBuilder` is the Builder, `String` is the Product）
- `Request.Builder`是Builder，`Request`是Product（`Request.Builder` is the Builder, `Request` is the Product）

---

#### Strategy Pattern（策略模式）

**涉及的类（Classes involved）**：
- `Context`：上下文类，使用策略（Context class that uses the strategy）
- `Strategy`：策略接口（Strategy interface）
- `ConcreteStrategyA`, `ConcreteStrategyB`：具体策略类（Concrete strategy classes）

**关系（Relationships）**：
- `Context`持有`Strategy`接口的引用（`Context` holds a reference to `Strategy` interface）
- `ConcreteStrategyA`和`ConcreteStrategyB`实现`Strategy`接口（`ConcreteStrategyA` and `ConcreteStrategyB` implement `Strategy` interface）
- `Context`通过`Strategy`接口调用算法，可以在运行时切换不同的具体策略（`Context` calls algorithm through `Strategy` interface, can switch between different concrete strategies at runtime）

**例子（Example）**：
- `Map`是Context（`Map` is the Context）
- `DirectionGenerator`是Strategy接口（`DirectionGenerator` is the Strategy interface）
- `DrivingDirections`和`TransitDirections`是Concrete Strategies（`DrivingDirections` and `TransitDirections` are Concrete Strategies）

---

#### Observer Pattern（观察者模式）

**涉及的类（Classes involved）**：
- `Observable`（或`Subject`）：被观察的对象（The object being observed）
- `Observer`（或`Listener`）：观察者接口（Observer interface）
- `ConcreteObserverA`, `ConcreteObserverB`：具体观察者类（Concrete observer classes）

**关系（Relationships）**：
- `Observable`维护一个`Observer`列表（`Observable` maintains a list of `Observer`s）
- `ConcreteObserverA`和`ConcreteObserverB`实现`Observer`接口（`ConcreteObserverA` and `ConcreteObserverB` implement `Observer` interface）
- 当`Observable`的状态改变时，它通知所有注册的`Observer`（When `Observable`'s state changes, it notifies all registered `Observer`s）
- 观察者收到通知后执行相应的操作（Observers perform corresponding actions after receiving notification）

**在Java中的实现（Implementation in Java）**：
- `ViewModel`是Observable，使用`PropertyChangeSupport`管理观察者列表（`ViewModel` is Observable, uses `PropertyChangeSupport` to manage observer list）
- `View`实现`PropertyChangeListener`接口，是Observer（`View` implements `PropertyChangeListener` interface, is Observer）
- 当ViewModel改变时，调用`firePropertyChange()`，所有View的`propertyChange()`方法被调用（When ViewModel changes, calls `firePropertyChange()`, all Views' `propertyChange()` methods are called）

---

#### Façade Pattern（外观模式）

**涉及的类（Classes involved）**：
- `Facade`：外观类，提供简化的接口（Facade class providing simplified interface）
- `SubsystemClassA`, `SubsystemClassB`, `SubsystemClassC`：子系统类（Subsystem classes）

**关系（Relationships）**：
- `Facade`持有对子系统类的引用（`Facade` holds references to subsystem classes）
- `Facade`的方法委托给相应的子系统类（`Facade` methods delegate to appropriate subsystem classes）
- 客户端只与`Facade`交互，不需要知道子系统的复杂性（Clients only interact with `Facade`, don't need to know subsystem complexity）

**例子（Example）**：
- `EmployeeFacade`是Facade（`EmployeeFacade` is the Facade）
- `EmployeeCalculator`, `EmployeeReporter`, `EmployeeSaver`是子系统类（`EmployeeCalculator`, `EmployeeReporter`, `EmployeeSaver` are subsystem classes）
- `EmployeeFacade`的方法委托给这些子系统类（`EmployeeFacade` methods delegate to these subsystem classes）

---

#### Adapter Pattern（适配器模式）

**使用委托的Adapter（Adapter with Delegation）**：

**涉及的类（Classes involved）**：
- `Adapter`：适配器类（Adapter class）
- `Adaptee`：需要适配的遗留类（Legacy class that needs to be adapted）
- `Target`：目标接口（Target interface）

**关系（Relationships）**：
- `Adapter`实现`Target`接口（`Adapter` implements `Target` interface）
- `Adapter`持有`Adaptee`的引用（`Adapter` holds a reference to `Adaptee`）
- `Adapter`将`Target`接口的调用转换为`Adaptee`的方法调用（`Adapter` converts `Target` interface calls to `Adaptee` method calls）

**使用继承的Adapter（Adapter with Inheritance）**：

**涉及的类（Classes involved）**：
- `Adapter`：适配器类（Adapter class）
- `Adaptee`：需要适配的遗留类（Legacy class that needs to be adapted）
- `Target`：目标接口（Target interface）

**关系（Relationships）**：
- `Adapter`继承`Adaptee`并实现`Target`接口（`Adapter` extends `Adaptee` and implements `Target` interface）
- `Adapter`可以重用`Adaptee`的方法，并添加新功能（`Adapter` can reuse `Adaptee` methods and add new functionality）

**例子（Example）**：
- `MovieTicket`是Adapter（`MovieTicket` is the Adapter）
- `Ticket`是Adaptee（`Ticket` is the Adaptee）
- `Tradable`是Target接口（`Tradable` is the Target interface）

---

### What is an anti-pattern? What might the anti-pattern of each design pattern above look like?
### 什么是反模式？每个设计模式的反模式可能是什么样子？

**什么是反模式（What is an anti-pattern）**：

反模式是设计模式的反面——它们是对常见编程问题的不太方便的解决方案（Anti-patterns are the opposite of design patterns — they are less convenient solutions to commonly-experienced programming problems）。如果代码显示了反模式，你可以通过重构来实现设计模式来改进代码的设计（If code displays an anti-pattern, you can improve the design of the code by refactoring to implement a design pattern instead）。

---

#### Factory Pattern的反模式（Anti-pattern of Factory Pattern）

**反模式**：客户端代码直接使用`new`关键字创建具体类，导致紧耦合（Client code directly uses `new` keyword to create concrete classes, causing tight coupling）。

**例子（Example）**：
```java
// 反模式：直接创建具体类
Shape shape;
if (userInput.equals("Rectangle")) {
    shape = new Rectangle();  // 直接依赖具体类
} else if (userInput.equals("Circle")) {
    shape = new Circle();     // 直接依赖具体类
}
```

**问题（Problems）**：
- 客户端代码依赖于具体类名（Client code depends on concrete class names）
- 添加新类型需要修改客户端代码（Adding new types requires modifying client code）
- 违反了开闭原则（Violates Open/Closed Principle）

---

#### Builder Pattern的反模式（Anti-pattern of Builder Pattern）

**反模式**：使用一个有很多参数的构造函数，或者使用多个构造函数来处理不同的参数组合（Using a constructor with many parameters, or using multiple constructors to handle different parameter combinations）。

**例子（Example）**：
```java
// 反模式：有很多参数的构造函数
Pizza pizza = new Pizza(true, false, true, "large", "pepperoni", "mushrooms", "onions", "cheese", "tomato");
// 很难知道每个参数代表什么
```

**问题（Problems）**：
- 参数太多，难以理解（Too many parameters, hard to understand）
- 容易出错，参数顺序很重要（Error-prone, parameter order matters）
- 可选参数需要多个构造函数（Optional parameters require multiple constructors）

---

#### Strategy Pattern的反模式（Anti-pattern of Builder Pattern）

**反模式**：在类中使用大量的if-else或switch语句来选择不同的算法（Using many if-else or switch statements in a class to choose between different algorithms）。

**例子（Example）**：
```java
// 反模式：使用if-else选择算法
class Author {
    public void sortBooks(String sortType) {
        if (sortType.equals("insertion")) {
            // 插入排序代码
        } else if (sortType.equals("selection")) {
            // 选择排序代码
        }
    }
    
    public void displayBooks(String displayType) {
        if (displayType.equals("natural")) {
            // 自然顺序显示代码
        } else if (displayType.equals("reverse")) {
            // 反向显示代码
        }
    }
}
```

**问题（Problems）**：
- 添加新算法需要修改现有类（Adding new algorithms requires modifying existing class）
- 违反了开闭原则（Violates Open/Closed Principle）
- 类承担了太多职责（Class has too many responsibilities）

---

#### Observer Pattern的反模式（Anti-pattern of Observer Pattern）

**反模式**：被观察的对象直接调用观察者的方法，导致紧耦合（The observed object directly calls observer methods, causing tight coupling）。

**例子（Example）**：
```java
// 反模式：直接调用观察者
class ViewModel {
    private View view1;
    private View view2;
    
    public void update() {
        view1.update();  // 直接调用
        view2.update();  // 直接调用
    }
}
```

**问题（Problems）**：
- 被观察对象需要知道所有观察者的具体类型（Observable needs to know all observer concrete types）
- 添加新观察者需要修改被观察对象（Adding new observers requires modifying observable）
- 紧耦合，难以测试（Tight coupling, hard to test）

---

#### Façade Pattern的反模式（Anti-pattern of Façade Pattern）

**反模式**：客户端直接与多个子系统类交互，需要了解所有子系统的复杂性（Client directly interacts with multiple subsystem classes, needs to understand all subsystem complexity）。

**例子（Example）**：
```java
// 反模式：客户端直接使用子系统
EmployeeCalculator calculator = new EmployeeCalculator();
EmployeeReporter reporter = new EmployeeReporter();
EmployeeSaver saver = new EmployeeSaver();

// 客户端需要知道如何使用每个子系统
double pay = calculator.calculatePay(employee);
reporter.reportHours(employee);
saver.save(employee);
```

**问题（Problems）**：
- 客户端需要了解子系统的复杂性（Client needs to understand subsystem complexity）
- 客户端代码与多个子系统耦合（Client code coupled to multiple subsystems）
- 难以维护和修改（Hard to maintain and modify）

---

#### Adapter Pattern的反模式（Anti-pattern of Adapter Pattern）

**反模式**：修改遗留类以匹配新接口，或者让客户端直接使用不兼容的接口（Modifying legacy class to match new interface, or having client directly use incompatible interfaces）。

**例子（Example）**：
```java
// 反模式1：修改遗留类
class Ticket {
    // 修改原始类以添加新功能
    public void trade(String newOwner) { ... }
}

// 反模式2：客户端直接处理不兼容的接口
Ticket ticket = new Ticket();
// 客户端需要自己处理接口不匹配的问题
```

**问题（Problems）**：
- 修改遗留类可能破坏现有代码（Modifying legacy class may break existing code）
- 客户端需要处理接口不匹配（Client needs to handle interface mismatch）
- 违反了开闭原则（Violates Open/Closed Principle）

---

### What is the difference between a "refactoring technique" and any other modification to a class or program?
### "重构技术"和其他对类或程序的修改有什么区别？

**Answer / 答案：**

重构（refactoring）是指程序员进行一系列改进软件设计的更改——但不改变行为（Refactoring refers to when programmers make a series of changes that improve the design of the software — but without changing the behaviour）。

**关键区别（Key Differences）**：

1. **不改变行为（No behavior change）**：重构只改变代码的结构和设计，不改变程序的功能（Refactoring only changes code structure and design, does not change program functionality）。重构后的代码应该通过所有现有的测试（Refactored code should pass all existing tests）。

2. **改进设计（Improves design）**：重构的目的是让代码更容易理解、导航和调试（The purpose of refactoring is to make code easier to understand, navigate, and debug），更容易自动测试（easier to automatically test），更容易添加新功能（easier to add new features）。

3. **系统化的技术（Systematic techniques）**：重构技术是经过验证的、系统化的方法来改进代码（Refactoring techniques are proven, systematic methods to improve code）。它们有明确的步骤和规则（They have clear steps and rules）。

**其他修改（Other modifications）**：
- 添加新功能（Adding new features）：改变程序的行为（Changes program behavior）
- 修复bug（Fixing bugs）：改变程序的行为（Changes program behavior）
- 性能优化（Performance optimization）：可能改变行为（May change behavior）

**规则（Rule）**：重构时，代码应该始终通过现有的测试（When refactoring, the code should always pass the existing tests）！

---

### Explain how each refactoring technique works
### 解释每个重构技术如何工作

#### Extract Method（提取方法）

**如何工作（How it works）**：

将一段代码从方法中提取出来，创建一个新的辅助方法（Extract a block of code from a method and create a new helper method）。原始方法调用这个新方法（The original method calls this new method）。

**步骤（Steps）**：
1. 选择要提取的代码块（Select the block of code to extract）
2. 创建一个新方法，将选中的代码移到新方法中（Create a new method and move selected code to it）
3. 用新方法调用替换原始代码（Replace original code with call to new method）
4. 根据目的和上下文，可以选择将新方法设为private和可能static（Depending on purpose and context, you may choose to make it private and possibly static）

**例子（Example）**：
```java
// 重构前（Before）
public void processOrder(Order order) {
    // 验证订单
    if (order.getAmount() <= 0) {
        throw new IllegalArgumentException("Invalid amount");
    }
    if (order.getCustomer() == null) {
        throw new IllegalArgumentException("Customer required");
    }
    // 处理订单...
}

// 重构后（After）
public void processOrder(Order order) {
    validateOrder(order);  // 调用提取的方法
    // 处理订单...
}

private void validateOrder(Order order) {  // 提取的方法
    if (order.getAmount() <= 0) {
        throw new IllegalArgumentException("Invalid amount");
    }
    if (order.getCustomer() == null) {
        throw new IllegalArgumentException("Customer required");
    }
}
```

**好处（Benefits）**：
- 代码更易读（Code is more readable）
- 可以重用提取的方法（Extracted method can be reused）
- 更容易测试（Easier to test）

---

#### Change Method Declaration（更改方法声明）

**如何工作（How it works）**：

修改方法的定义，比如改变参数、返回类型或方法名（Modify how a method is defined, such as altering its parameters, return type, or method name）。必须小心更新任何客户端代码以及被修改的方法体（One must be careful to update any client code, as well as the body of the method being altered）。

**步骤（Steps）**：
1. 修改方法签名（参数、返回类型、方法名）（Modify method signature (parameters, return type, method name)）
2. 更新方法体以适应新签名（Update method body to accommodate new signature）
3. 更新所有调用该方法的地方（Update all places where the method is called）

**在IntelliJ中（In IntelliJ）**：
- 使用`Change Signature`功能来执行这种重构（Use `Change Signature` feature to perform this refactoring）
- IntelliJ会自动更新所有调用点（IntelliJ automatically updates all call sites）

**例子（Example）**：
```java
// 重构前（Before）
public void process(String name, int age) { ... }

// 重构后（After）
public void processUser(String name, int age, String email) { ... }
// 所有调用process()的地方都被更新为processUser()
```

---

#### Encapsulate Fields（封装字段）

**如何工作（How it works）**：

将实例变量的访问修饰符改为private，并引入getter和setter方法来提供适当的访问（Change access modifiers on instance variables to private, and introduce getters and setters to provide appropriate access）。更新任何客户端或实现代码，使用getter和setter，而不是直接访问数据（Update any client or implementation code to use getters and setters where data was directly accessed previously）。

**步骤（Steps）**：
1. 将实例变量改为private（Change instance variables to private）
2. 创建getter方法（Create getter methods）
3. 创建setter方法（如果需要修改）（Create setter methods if modification is needed）
4. 更新所有直接访问字段的代码，改为使用getter/setter（Update all code that directly accesses fields to use getters/setters）

**在IntelliJ中（In IntelliJ）**：
- 选择字段，然后选择`Refactoring -> Encapsulate Fields...`（Select fields, then choose `Refactoring -> Encapsulate Fields...`）
- IntelliJ会自动生成getter和setter，并更新所有引用（IntelliJ automatically generates getters and setters and updates all references）

**例子（Example）**：
```java
// 重构前（Before）
public class Student {
    public String name;  // public字段
    public int age;
}

// 重构后（After）
public class Student {
    private String name;  // private字段
    private int age;
    
    public String getName() { return name; }  // getter
    public void setName(String name) { this.name = name; }  // setter
    public int getAge() { return age; }
    public void setAge(int age) { this.age = age; }
}
```

**好处（Benefits）**：
- 控制对数据的访问（Control access to data）
- 可以在getter/setter中添加验证逻辑（Can add validation logic in getters/setters）
- 符合Java编码规范（Follows Java coding conventions）

---

#### Split Loop（拆分循环）

**如何工作（How it works）**：

将一个执行多个计算的循环拆分成多个独立的循环，每个循环执行一个独立的计算（Split a loop that performs multiple computations into separate loops, each performing an independent computation）。

**步骤（Steps）**：
1. 识别循环中执行的不同计算（Identify different computations performed in the loop）
2. 为每个计算创建一个新的循环（Create a new loop for each computation）
3. 每个循环遍历相同的数据，但只执行一个计算（Each loop iterates over the same data but performs only one computation）

**例子（Example）**：
```java
// 重构前（Before）
int sum = 0;
int max = Integer.MIN_VALUE;
for (int num : numbers) {
    sum += num;      // 计算总和
    if (num > max) { // 找最大值
        max = num;
    }
}

// 重构后（After）
int sum = 0;
for (int num : numbers) {
    sum += num;  // 第一个循环：计算总和
}

int max = Integer.MIN_VALUE;
for (int num : numbers) {
    if (num > max) {  // 第二个循环：找最大值
        max = num;
    }
}
```

**好处（Benefits）**：
- 每个循环职责单一（Each loop has a single responsibility）
- 更容易应用Extract Method（Easier to apply Extract Method）
- 代码更易理解（Code is more understandable）

**注意（Note）**：这个重构在IntelliJ中不直接支持，但可以使用复制+粘贴然后删除重复部分来实现（This refactoring is not directly supported by IntelliJ, but can be implemented using copy+paste followed by deleting duplicated parts）。

---

#### Slide Statements（滑动语句）

**如何工作（How it works）**：

移动代码行，以更有意义的方式将代码分组在一起（Move lines of code around to help group together code in more meaningful ways）。例如，将每个累加器变量的声明移到对应的累加器循环之前（For example, move the declaration of each accumulator variable so that they are defined immediately before each of their corresponding accumulator loops）。

**步骤（Steps）**：
1. 识别应该组合在一起的代码（Identify code that should be grouped together）
2. 移动代码行到更合适的位置（Move lines of code to more appropriate positions）
3. 确保移动后代码逻辑不变（Ensure code logic remains unchanged after moving）

**例子（Example）**：
```java
// 重构前（Before）
int sum = 0;
int max = Integer.MIN_VALUE;
int count = 0;

for (int num : numbers) {
    sum += num;
}

for (int num : numbers) {
    if (num > max) {
        max = num;
    }
}

for (int num : numbers) {
    count++;
}

// 重构后（After）
int sum = 0;
for (int num : numbers) {
    sum += num;
}

int max = Integer.MIN_VALUE;
for (int num : numbers) {
    if (num > max) {
        max = num;
    }
}

int count = 0;
for (int num : numbers) {
    count++;
}
// 每个变量声明紧挨着使用它的循环
```

**好处（Benefits）**：
- 相关代码组合在一起（Related code is grouped together）
- 更容易应用Extract Method（Easier to apply Extract Method）
- 代码更易理解（Code is more understandable）

**在IntelliJ中（In IntelliJ）**：
- 可以使用快捷键移动代码行（Can use shortcuts to move lines of code）
- 使用Alt+Shift+Up/Down移动当前行（Use Alt+Shift+Up/Down to move current line）

---

#### Replace Constructor with Builder（用Builder替换构造函数）

**如何工作（How it works）**：

重构对象的构造方式，引入一个builder类，负责分步构建类的实例（Refactor how objects are constructed by introducing a builder class that is responsible for constructing instances of the class in steps）。

**步骤（Steps）**：
1. 创建一个Builder类（Create a Builder class）
2. Builder类有设置各个属性的方法（Builder class has methods to set each property）
3. Builder类有`build()`方法返回最终对象（Builder class has `build()` method that returns final object）
4. 将原始构造函数改为private（Make original constructor private）
5. 更新客户端代码使用Builder（Update client code to use Builder）

**例子（Example）**：
```java
// 重构前（Before）
Pizza pizza = new Pizza(true, false, true, "large", "pepperoni");

// 重构后（After）
Pizza pizza = new PizzaBuilder()
    .setCheese(true)
    .setPepperoni(true)
    .setBacon(false)
    .setSize("large")
    .setTopping("pepperoni")
    .build();
```

**好处（Benefits）**：
- 代码更易读（Code is more readable）
- 参数顺序不重要（Parameter order doesn't matter）
- 可选参数更容易处理（Optional parameters are easier to handle）

**在IntelliJ中（In IntelliJ）**：
- 使用`Replace Constructor with Builder`重构功能（Use `Replace Constructor with Builder` refactoring feature）

---

#### Replace Constructor with Factory Method（用工厂方法替换构造函数）

**如何工作（How it works）**：

重构对象的构造方式，引入一个静态方法，负责返回类的实例，而不是让代码直接调用构造函数（Refactor how objects are constructed by introducing a static method that is responsible for returning the instance of the class rather than having the code directly call the constructor）。

**步骤（Steps）**：
1. 创建一个静态方法（Create a static method）
2. 静态方法内部调用构造函数（Static method internally calls constructor）
3. 将构造函数改为private（可选）（Make constructor private (optional)）
4. 更新客户端代码使用工厂方法（Update client code to use factory method）

**例子（Example）**：
```java
// 重构前（Before）
Shape shape = new Circle(5.0);

// 重构后（After）
Shape shape = Circle.create(5.0);  // 或 Circle.of(5.0)

// Circle类中
public static Circle create(double radius) {
    return new Circle(radius);
}
```

**好处（Benefits）**：
- 方法名可以更清楚地表达意图（Method name can clearly express intent）
- 可以返回子类实例（Can return subclass instances）
- 可以控制实例的创建（Can control instance creation）
- 隐藏构造函数调用的细节（Hides detail of how instance is created）

**在IntelliJ中（In IntelliJ）**：
- 使用`Replace Constructor with Factory Method`重构功能（Use `Replace Constructor with Factory Method` refactoring feature）

---

### Which design patterns are built into Clean Architecture? In other words, if you implement Clean Architecture, which design patterns will necessarily appear in your code?
### Clean Architecture中内置了哪些设计模式？换句话说，如果你实现Clean Architecture，哪些设计模式必然会在你的代码中出现？

**Answer / 答案：**

Clean Architecture的实现中必然会出现以下设计模式（The following design patterns will necessarily appear in Clean Architecture implementations）：

#### 1. Dependency Injection（依赖注入）

**为什么必然出现（Why it's necessary）**：

Clean Architecture要求依赖必须指向内层（Clean Architecture requires dependencies to point inward）。内层定义接口，外层实现接口（Inner layers define interfaces, outer layers implement interfaces）。这意味着依赖必须通过构造函数或方法参数注入，而不是在类内部直接创建（This means dependencies must be injected through constructors or method parameters, not created directly inside classes）。

**例子（Example）**：
```java
// Use Case Interactor通过构造函数接收依赖
class LoginUseCaseInteractor {
    private UserDataAccessInterface userDataAccess;  // 依赖接口
    private LoginOutputBoundary outputBoundary;
    
    // 依赖注入
    public LoginUseCaseInteractor(
            UserDataAccessInterface userDataAccess,
            LoginOutputBoundary outputBoundary) {
        this.userDataAccess = userDataAccess;
        this.outputBoundary = outputBoundary;
    }
}
```

---

#### 2. Observer Pattern（观察者模式）

**为什么必然出现（Why it's necessary）**：

在Clean Architecture中，ViewModel是Observable，View是Observer（In Clean Architecture, ViewModel is Observable, View is Observer）。当ViewModel的状态改变时，View需要更新以反映新数据（When ViewModel's state changes, View needs to update to reflect new data）。这使用Observer模式完成（This is accomplished using the Observer pattern）。

**例子（Example）**：
```java
// ViewModel使用PropertyChangeSupport（Observable）
class LoginViewModel extends ViewModel {
    private PropertyChangeSupport support = new PropertyChangeSupport(this);
    
    public void firePropertyChanged() {
        support.firePropertyChange("state", null, this.state);
    }
}

// View实现PropertyChangeListener（Observer）
class LoginView implements PropertyChangeListener {
    @Override
    public void propertyChange(PropertyChangeEvent evt) {
        // 更新UI
    }
}
```

---

#### 3. Strategy Pattern（策略模式，可能）

**为什么可能出现（Why it might appear）**：

虽然Strategy模式不是Clean Architecture的必需部分，但它经常出现在Use Case层（Although Strategy pattern is not a required part of Clean Architecture, it often appears in the Use Case layer）。不同的Use Case可能使用不同的策略来处理相同的任务（Different Use Cases may use different strategies to handle the same task）。

**例子（Example）**：
```java
// 不同的验证策略
interface ValidationStrategy {
    boolean validate(String input);
}

class EmailValidationStrategy implements ValidationStrategy { ... }
class PasswordValidationStrategy implements ValidationStrategy { ... }

// Use Case使用策略
class SignupUseCase {
    private ValidationStrategy emailValidator;
    private ValidationStrategy passwordValidator;
}
```

---

#### 4. Adapter Pattern（适配器模式）

**为什么必然出现（Why it's necessary）**：

Clean Architecture的Interface Adapters层本质上就是Adapter模式的体现（The Interface Adapters layer in Clean Architecture is essentially an embodiment of the Adapter pattern）。Controller、Presenter都是适配器，它们将数据从一种格式转换为另一种格式（Controller and Presenter are adapters that convert data from one format to another）。

**例子（Example）**：
```java
// Controller适配用户输入到Input Data
class LoginController {
    public void handleLogin(String username, String password) {
        // 将原始输入适配为Input Data格式
        LoginInputData inputData = new LoginInputData(username, password);
        loginUseCase.execute(inputData);
    }
}

// Presenter适配Output Data到ViewModel格式
class LoginPresenter {
    public void present(LoginOutputData outputData) {
        // 将Output Data适配为ViewModel格式
        viewModel.setState(outputData.isSuccess() ? "成功" : "失败");
    }
}
```

---

#### 5. Factory Pattern（工厂模式，可能）

**为什么可能出现（Why it might appear）**：

Main组件（或Driver）负责创建和组装所有对象（The Main component (or Driver) is responsible for creating and assembling all objects）。这可以使用Factory模式来实现（This can be implemented using the Factory pattern）。

**例子（Example）**：
```java
// Main组件使用Factory创建对象
class Main {
    public static void main(String[] args) {
        // 可以看作是一个简单的Factory
        UserDataAccessInterface dataAccess = createDataAccess();
        LoginViewModel viewModel = createViewModel();
        LoginPresenter presenter = createPresenter(viewModel);
        // ...
    }
}
```

---

## [M5] Ethics and Regex

### What is a speech act?
### 什么是言语行为？

**Answer / 答案：**

言语行为（speech act）是语言哲学中的一个概念，指的是通过说话来执行的行为（A speech act is a concept in philosophy of language that refers to an action performed by speaking）。言语行为不仅仅是描述或陈述事实，而是通过语言来执行某种行为（Speech acts are not just describing or stating facts, but performing some action through language）。

**例子（Examples）**：
- **断言（Assertion）**："今天是星期一"（"Today is Monday"）- 陈述一个事实（States a fact）
- **承诺（Promise）**："我保证会完成作业"（"I promise to finish the homework"）- 做出承诺（Makes a promise）
- **请求（Request）**："请帮我一下"（"Please help me"）- 提出请求（Makes a request）
- **命令（Command）**："关闭门"（"Close the door"）- 发出命令（Issues a command）
- **道歉（Apology）**："对不起"（"I'm sorry"）- 表达歉意（Expresses apology）

在软件设计中，理解言语行为有助于设计更好的用户界面和交互（In software design, understanding speech acts helps design better user interfaces and interactions）。例如，按钮上的文字"保存"是一个命令，而"已保存"是一个状态声明（For example, the text "Save" on a button is a command, while "Saved" is a state declaration）。

---

### What is the difference between material and relational harm?
### 物质伤害和关系伤害的区别是什么？

**Answer / 答案：**

**物质伤害（Material Harm）**：

物质伤害是指对个人或群体的物质资源、财产或身体造成的实际损害（Material harm refers to actual damage to an individual's or group's material resources, property, or physical well-being）。这种伤害是可见的、可量化的（This harm is visible and quantifiable）。

**例子（Examples）**：
- 经济损失（Financial loss）：软件bug导致用户损失金钱（Software bug causes user to lose money）
- 身体伤害（Physical harm）：医疗设备软件故障导致患者受伤（Medical device software failure causes patient injury）
- 数据丢失（Data loss）：系统故障导致重要数据丢失（System failure causes important data loss）
- 隐私泄露（Privacy breach）：个人信息被泄露，导致身份盗窃（Personal information leaked, leading to identity theft）

**关系伤害（Relational Harm）**：

关系伤害是指对个人或群体的社会关系、声誉、尊严或社会地位造成的损害（Relational harm refers to damage to an individual's or group's social relationships, reputation, dignity, or social status）。这种伤害影响的是人与人之间的关系和社会地位（This harm affects relationships between people and social status）。

**例子（Examples）**：
- 声誉损害（Reputation damage）：虚假信息在社交媒体上传播，损害某人的声誉（False information spread on social media damages someone's reputation）
- 社会排斥（Social exclusion）：软件设计导致某些群体被边缘化（Software design causes certain groups to be marginalized）
- 尊严受损（Dignity harm）：界面设计让用户感到被侮辱或贬低（Interface design makes users feel insulted or degraded）
- 关系破裂（Relationship breakdown）：软件功能导致用户之间的关系出现问题（Software features cause problems in user relationships）

**如何识别（How to identify）**：

**识别物质伤害（Identifying Material Harm）**：
- 是否有经济损失？（Is there financial loss?）
- 是否有身体伤害？（Is there physical harm?）
- 是否有资源损失？（Is there resource loss?）
- 伤害是否可以直接测量？（Can the harm be directly measured?）

**识别关系伤害（Identifying Relational Harm）**：
- 是否影响社会关系？（Does it affect social relationships?）
- 是否损害声誉？（Does it damage reputation?）
- 是否影响尊严或自尊？（Does it affect dignity or self-esteem?）
- 是否导致社会排斥或边缘化？（Does it cause social exclusion or marginalization?）

---

### What are the similarities and differences between the medical and social models of disability?
### 医疗模式和社会模式的残疾模型有什么相似之处和不同之处？

**Answer / 答案：**

**医疗模式（Medical Model）**：

医疗模式将残疾视为个人身体或心理的缺陷或疾病（The medical model views disability as a defect or disease in an individual's body or mind）。这种模式认为残疾是个人需要"修复"或"治疗"的问题（This model sees disability as a problem that the individual needs to "fix" or "treat"）。

**特点（Characteristics）**：
- 残疾是个人问题（Disability is an individual problem）
- 重点在于"修复"个人（Focus on "fixing" the individual）
- 残疾被视为异常或缺陷（Disability is seen as abnormal or defective）
- 解决方案是医疗干预或康复（Solution is medical intervention or rehabilitation）

**例子（Example）**：
- 认为失明是需要治疗的疾病（Views blindness as a disease that needs treatment）
- 认为轮椅使用者需要"康复"（Views wheelchair users as needing "rehabilitation"）

**社会模式（Social Model）**：

社会模式将残疾视为社会和环境障碍的结果，而不是个人缺陷（The social model views disability as a result of social and environmental barriers, not individual defects）。这种模式认为社会应该适应和包容所有人（This model believes society should adapt and include everyone）。

**特点（Characteristics）**：
- 残疾是社会问题（Disability is a social problem）
- 重点在于消除社会和环境障碍（Focus on removing social and environmental barriers）
- 残疾是正常的人类多样性的一部分（Disability is part of normal human diversity）
- 解决方案是改变环境和社会（Solution is changing environment and society）

**例子（Example）**：
- 失明不是问题，缺乏无障碍设计才是问题（Blindness is not the problem, lack of accessible design is）
- 轮椅使用者不是问题，缺乏无障碍设施才是问题（Wheelchair users are not the problem, lack of accessible facilities is）

**相似之处（Similarities）**：
- 都承认残疾的存在（Both acknowledge the existence of disability）
- 都试图改善残疾人的生活（Both attempt to improve the lives of people with disabilities）
- 都涉及医疗和社会支持（Both involve medical and social support）

**不同之处（Differences）**：

| 方面 | 医疗模式 | 社会模式 |
|------|---------|---------|
| **问题所在** | 个人 | 社会和环境 |
| **解决方案** | 治疗个人 | 改变社会和环境 |
| **责任** | 个人 | 社会 |
| **视角** | 残疾是缺陷 | 残疾是多样性 |
| **目标** | 修复个人 | 包容所有人 |

**在软件设计中的应用（Application in Software Design）**：

**医疗模式的方法（Medical Model Approach）**：
- 为残疾人创建"特殊"功能（Create "special" features for people with disabilities）
- 认为用户需要适应软件（Users need to adapt to software）

**社会模式的方法（Social Model Approach）**：
- 设计所有人都能使用的软件（Design software that everyone can use）
- 遵循通用设计原则（Follow universal design principles）
- 消除软件中的障碍（Remove barriers in software）

---

### Why and how can we use the Principles of Universal Design when designing software?
### 为什么以及如何在设计软件时使用通用设计原则？

**Answer / 答案：**

**为什么使用通用设计原则（Why use Universal Design Principles）**：

1. **包容性（Inclusivity）**：让软件对所有用户都可用，无论他们的能力、年龄、背景如何（Make software usable for all users regardless of their abilities, age, or background）

2. **法律要求（Legal Requirements）**：许多国家和地区有法律要求软件必须可访问（Many countries and regions have laws requiring software to be accessible）

3. **商业利益（Business Benefits）**：更大的用户群体意味着更大的市场（Larger user base means larger market）

4. **道德责任（Ethical Responsibility）**：作为软件开发者，我们有责任创建包容性的软件（As software developers, we have a responsibility to create inclusive software）

5. **更好的设计（Better Design）**：遵循通用设计原则通常会导致更好的整体设计（Following universal design principles often results in better overall design）

**通用设计原则（Universal Design Principles）**：

1. **公平使用（Equitable Use）**：设计对所有用户都有用且具有市场吸引力（Design is useful and marketable to people with diverse abilities）

2. **使用灵活性（Flexibility in Use）**：设计适应广泛的个人偏好和能力（Design accommodates a wide range of individual preferences and abilities）

3. **简单直观（Simple and Intuitive）**：使用与用户经验、知识、语言技能和当前注意力水平无关的方式（Use regardless of user's experience, knowledge, language skills, or current concentration level）

4. **信息感知（Perceptible Information）**：无论环境条件或用户的感觉能力如何，都能有效传达必要的信息（Effectively communicates necessary information regardless of ambient conditions or user's sensory abilities）

5. **容错性（Tolerance for Error）**：设计将危险和意外操作的 adverse 后果降至最低（Design minimizes hazards and the adverse consequences of accidental or unintended actions）

6. **低体力消耗（Low Physical Effort）**：可以高效舒适地使用，减少疲劳（Can be used efficiently and comfortably with minimum fatigue）

7. **尺寸和空间（Size and Space）**：无论用户的身体尺寸、姿势或移动性如何，都提供适当的大小和空间（Appropriate size and space provided regardless of user's body size, posture, or mobility）

**如何在软件设计中应用（How to apply in Software Design）**：

1. **可访问性（Accessibility）**：
   - 提供键盘导航（Provide keyboard navigation）
   - 支持屏幕阅读器（Support screen readers）
   - 使用足够的颜色对比度（Use sufficient color contrast）
   - 提供文本替代图片（Provide text alternatives for images）

2. **灵活性（Flexibility）**：
   - 允许用户自定义界面（Allow users to customize interface）
   - 提供多种输入方式（Provide multiple input methods）
   - 支持不同的显示偏好（Support different display preferences）

3. **简单性（Simplicity）**：
   - 清晰的导航（Clear navigation）
   - 直观的界面（Intuitive interface）
   - 一致的交互模式（Consistent interaction patterns）

4. **信息传达（Information Communication）**：
   - 清晰的错误消息（Clear error messages）
   - 多种信息呈现方式（Multiple ways to present information）
   - 适当的反馈（Appropriate feedback）

5. **容错性（Error Tolerance）**：
   - 确认危险操作（Confirm dangerous actions）
   - 提供撤销功能（Provide undo functionality）
   - 清晰的错误恢复（Clear error recovery）

6. **效率（Efficiency）**：
   - 减少不必要的点击（Reduce unnecessary clicks）
   - 提供快捷方式（Provide shortcuts）
   - 优化性能（Optimize performance）

7. **适应性（Adaptability）**：
   - 响应式设计（Responsive design）
   - 支持不同屏幕尺寸（Support different screen sizes）
   - 适应不同的输入设备（Adapt to different input devices）

---

### What are the basic regular expression (regex) symbols that we covered in the reading and/or in lecture?
### 我们在阅读和/或课程中涉及的基本正则表达式（regex）符号有哪些？

**Answer / 答案：**

**基本正则表达式符号（Basic Regular Expression Symbols）**：

1. **`.`（点号）**：匹配除换行符外的任何单个字符（Matches any single character except newline）
   - 例子：`a.c` 匹配 "abc", "a1c", "a c"（Example: `a.c` matches "abc", "a1c", "a c"）

2. **`^`（脱字符）**：匹配字符串的开始（Matches the beginning of the string）
   - 例子：`^abc` 只匹配以"abc"开头的字符串（Example: `^abc` only matches strings starting with "abc"）

3. **`$`（美元符号）**：匹配字符串的结束（Matches the end of the string）
   - 例子：`abc$` 只匹配以"abc"结尾的字符串（Example: `abc$` only matches strings ending with "abc"）

4. **`*`（星号）**：匹配前面的字符零次或多次（Matches the preceding character zero or more times）
   - 例子：`ab*c` 匹配 "ac", "abc", "abbc", "abbbc"（Example: `ab*c` matches "ac", "abc", "abbc", "abbbc"）

5. **`+`（加号）**：匹配前面的字符一次或多次（Matches the preceding character one or more times）
   - 例子：`ab+c` 匹配 "abc", "abbc", "abbbc"，但不匹配 "ac"（Example: `ab+c` matches "abc", "abbc", "abbbc", but not "ac"）

6. **`?`（问号）**：匹配前面的字符零次或一次（Matches the preceding character zero or one time）
   - 例子：`ab?c` 匹配 "ac" 或 "abc"（Example: `ab?c` matches "ac" or "abc"）

7. **`[]`（字符类）**：匹配方括号内的任何一个字符（Matches any one character inside the square brackets）
   - 例子：`[abc]` 匹配 "a", "b", 或 "c"（Example: `[abc]` matches "a", "b", or "c"）
   - `[a-z]` 匹配任何小写字母（`[a-z]` matches any lowercase letter）
   - `[0-9]` 匹配任何数字（`[0-9]` matches any digit）

8. **`[^]`（否定字符类）**：匹配不在方括号内的任何字符（Matches any character not inside the square brackets）
   - 例子：`[^abc]` 匹配除了 "a", "b", "c" 之外的任何字符（Example: `[^abc]` matches any character except "a", "b", "c"）

9. **`|`（管道符）**：表示"或"，匹配左边或右边的模式（Represents "or", matches the pattern on the left or right）
   - 例子：`cat|dog` 匹配 "cat" 或 "dog"（Example: `cat|dog` matches "cat" or "dog"）

10. **`()`（分组）**：将多个字符组合在一起（Groups multiple characters together）
    - 例子：`(ab)+` 匹配 "ab", "abab", "ababab"（Example: `(ab)+` matches "ab", "abab", "ababab"）

11. **`\`（转义符）**：转义特殊字符，使其按字面意思匹配（Escapes special characters to match them literally）
    - 例子：`\.` 匹配字面的点号 "."（Example: `\.` matches the literal dot "."）
    - `\\` 匹配字面的反斜杠 "\"（`\\` matches the literal backslash "\"）

12. **`\d`**：匹配任何数字，等价于 `[0-9]`（Matches any digit, equivalent to `[0-9]`）

13. **`\w`**：匹配任何单词字符（字母、数字、下划线），等价于 `[a-zA-Z0-9_]`（Matches any word character (letter, digit, underscore), equivalent to `[a-zA-Z0-9_]`）

14. **`\s`**：匹配任何空白字符（空格、制表符、换行符等）（Matches any whitespace character (space, tab, newline, etc.)）

15. **`{n}`**：匹配前面的字符恰好n次（Matches the preceding character exactly n times）
    - 例子：`a{3}` 匹配 "aaa"（Example: `a{3}` matches "aaa"）

16. **`{n,}`**：匹配前面的字符至少n次（Matches the preceding character at least n times）
    - 例子：`a{2,}` 匹配 "aa", "aaa", "aaaa"（Example: `a{2,}` matches "aa", "aaa", "aaaa"）

17. **`{n,m}`**：匹配前面的字符至少n次，最多m次（Matches the preceding character at least n times, at most m times）
    - 例子：`a{2,4}` 匹配 "aa", "aaa", "aaaa"（Example: `a{2,4}` matches "aa", "aaa", "aaaa"）

---

### How can we write a regular expression that matches a set of Strings?
### 如何编写匹配一组字符串的正则表达式？

**Answer / 答案：**

编写正则表达式来匹配一组字符串的步骤（Steps to write a regular expression that matches a set of Strings）：

1. **分析字符串的共同模式（Analyze common patterns in the strings）**：
   - 识别固定部分和可变部分（Identify fixed parts and variable parts）
   - 识别重复模式（Identify repeating patterns）
   - 识别可选部分（Identify optional parts）

2. **使用适当的符号（Use appropriate symbols）**：
   - 固定文本直接写（Write fixed text directly）
   - 使用字符类 `[]` 匹配一组字符（Use character class `[]` to match a set of characters）
   - 使用量词 `*`, `+`, `?`, `{n}` 匹配重复（Use quantifiers `*`, `+`, `?`, `{n}` to match repetitions）
   - 使用 `|` 表示"或"（Use `|` for "or"）
   - 使用 `()` 分组（Use `()` for grouping）

3. **测试和调整（Test and adjust）**：
   - 测试正则表达式是否匹配所有目标字符串（Test if regex matches all target strings）
   - 确保不匹配不应该匹配的字符串（Ensure it doesn't match strings it shouldn't）
   - 根据需要调整（Adjust as needed）

**例子（Examples）**：

**例子1：匹配邮箱地址（Match email addresses）**：
```regex
[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}
```
- `[a-zA-Z0-9._%+-]+`：用户名部分，一个或多个字母、数字或特定字符（Username part, one or more letters, digits, or specific characters）
- `@`：字面的@符号（Literal @ symbol）
- `[a-zA-Z0-9.-]+`：域名部分（Domain part）
- `\.`：字面的点号（Literal dot）
- `[a-zA-Z]{2,}`：顶级域名，至少2个字母（Top-level domain, at least 2 letters）

**例子2：匹配电话号码（Match phone numbers）**：
```regex
\d{3}-\d{3}-\d{4}
```
- 匹配格式：123-456-7890（Matches format: 123-456-7890）

**例子3：匹配以特定前缀开头的字符串（Match strings starting with specific prefix）**：
```regex
^(user|admin|guest)_\d+
```
- 匹配：user_123, admin_456, guest_789（Matches: user_123, admin_456, guest_789）

---

### How can we find a String that conforms to a given regular expression?
### 如何找到符合给定正则表达式的字符串？

**Answer / 答案：**

找到符合给定正则表达式的字符串的方法（Methods to find a String that conforms to a given regular expression）：

1. **手动构造（Manual construction）**：
   - 理解正则表达式的含义（Understand what the regex means）
   - 根据模式构造字符串（Construct string according to the pattern）
   - 确保字符串匹配所有要求（Ensure string matches all requirements）

2. **使用工具（Using tools）**：
   - 使用在线正则表达式测试工具（Use online regex testing tools）
   - 使用正则表达式生成器（Use regex generators）
   - 使用支持正则表达式的文本编辑器（Use text editors that support regex）

3. **系统化方法（Systematic approach）**：
   - 从左到右分析正则表达式（Analyze regex from left to right）
   - 为每个部分构造对应的字符串（Construct corresponding string for each part）
   - 组合各部分（Combine all parts）

**例子（Example）**：

给定正则表达式：`^[A-Z][a-z]+\d{2,3}$`

**分析（Analysis）**：
- `^`：字符串开始（Start of string）
- `[A-Z]`：一个大写字母（One uppercase letter）
- `[a-z]+`：一个或多个小写字母（One or more lowercase letters）
- `\d{2,3}`：2到3个数字（2 to 3 digits）
- `$`：字符串结束（End of string）

**符合的字符串（Conforming strings）**：
- "Hello12" ✅
- "World123" ✅
- "Java99" ✅
- "Python456" ✅

**不符合的字符串（Non-conforming strings）**：
- "hello12" ❌（不是以大写字母开头）
- "Hello1" ❌（数字少于2个）
- "Hello1234" ❌（数字超过3个）

---

### What do we have to do to a regular expression to use it in a Java program?
### 在Java程序中使用正则表达式需要做什么？

**Answer / 答案：**

在Java程序中使用正则表达式需要（To use a regular expression in a Java program, you need to）：

1. **转义特殊字符（Escape special characters）**：
   - 在Java字符串中，反斜杠 `\` 是转义字符（In Java strings, backslash `\` is an escape character）
   - 正则表达式中的 `\` 需要写成 `\\`（`\` in regex needs to be written as `\\`）
   - 例如：正则表达式 `\d` 在Java中写成 `"\\d"`（For example: regex `\d` is written as `"\\d"` in Java）

2. **使用Pattern和Matcher类（Use Pattern and Matcher classes）**：
   - `Pattern` 类：编译正则表达式（`Pattern` class: compiles the regular expression）
   - `Matcher` 类：执行匹配操作（`Matcher` class: performs matching operations）

3. **基本步骤（Basic steps）**：
   ```java
   // 1. 编译正则表达式（Compile the regex）
   Pattern pattern = Pattern.compile("your_regex_here");
   
   // 2. 创建Matcher对象（Create Matcher object）
   Matcher matcher = pattern.matcher("string_to_match");
   
   // 3. 执行匹配（Perform matching）
   boolean matches = matcher.matches();
   ```

**例子（Example）**：

```java
import java.util.regex.Pattern;
import java.util.regex.Matcher;

// 正则表达式：匹配邮箱
// 在Java字符串中，需要转义反斜杠
String regex = "[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\\.[a-zA-Z]{2,}";

// 编译正则表达式
Pattern pattern = Pattern.compile(regex);

// 创建Matcher
Matcher matcher = pattern.matcher("user@example.com");

// 检查是否匹配
boolean matches = matcher.matches();  // true
```

**注意事项（Notes）**：
- Java字符串中的 `\\` 表示一个反斜杠（`\\` in Java string represents one backslash）
- 正则表达式中的特殊字符在Java字符串中可能需要转义（Special characters in regex may need escaping in Java strings）
- 使用 `Pattern.compile()` 编译正则表达式可以提高性能（Using `Pattern.compile()` to compile regex improves performance）

---

### What are three ways of checking if a String conforms to a regular expression in Java?
### 在Java中检查字符串是否符合正则表达式有哪三种方法？

**Answer / 答案：**

在Java中检查字符串是否符合正则表达式有三种主要方法（There are three main ways to check if a String conforms to a regular expression in Java）：

#### 方法1：使用String.matches()方法
#### Method 1: Using String.matches() method

**语法（Syntax）**：
```java
boolean matches = string.matches(regex);
```

**特点（Characteristics）**：
- 最简单直接的方法（Simplest and most direct method）
- 自动编译正则表达式（Automatically compiles the regex）
- 每次调用都会重新编译，性能较低（Recompiles on each call, lower performance）
- 只检查整个字符串是否匹配（Only checks if entire string matches）

**例子（Example）**：
```java
String email = "user@example.com";
String regex = "[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\\.[a-zA-Z]{2,}";

boolean isValid = email.matches(regex);  // true
```

---

#### 方法2：使用Pattern和Matcher类
#### Method 2: Using Pattern and Matcher classes

**语法（Syntax）**：
```java
Pattern pattern = Pattern.compile(regex);
Matcher matcher = pattern.matcher(string);
boolean matches = matcher.matches();
```

**特点（Characteristics）**：
- 更灵活，可以执行多种操作（More flexible, can perform various operations）
- 可以重用Pattern对象，性能更好（Can reuse Pattern object, better performance）
- 可以使用`find()`查找部分匹配（Can use `find()` to find partial matches）
- 可以使用`group()`提取匹配的部分（Can use `group()` to extract matched parts）

**例子（Example）**：
```java
String email = "user@example.com";
String regex = "[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\\.[a-zA-Z]{2,}";

Pattern pattern = Pattern.compile(regex);
Matcher matcher = pattern.matcher(email);
boolean matches = matcher.matches();  // true

// 也可以使用find()查找部分匹配
boolean found = matcher.find();  // 查找字符串中是否有匹配的部分
```

---

#### 方法3：使用Pattern.matches()静态方法
#### Method 3: Using Pattern.matches() static method

**语法（Syntax）**：
```java
boolean matches = Pattern.matches(regex, string);
```

**特点（Characteristics）**：
- 静态方法，使用方便（Static method, convenient to use）
- 内部使用Pattern和Matcher（Internally uses Pattern and Matcher）
- 每次调用都会重新编译，性能较低（Recompiles on each call, lower performance）
- 只检查整个字符串是否匹配（Only checks if entire string matches）

**例子（Example）**：
```java
String email = "user@example.com";
String regex = "[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\\.[a-zA-Z]{2,}";

boolean matches = Pattern.matches(regex, email);  // true
```

---

**三种方法的比较（Comparison of the three methods）**：

| 方法 | 性能 | 灵活性 | 使用场景 |
|------|------|--------|---------|
| **String.matches()** | 低（每次重新编译） | 低 | 简单的一次性检查 |
| **Pattern + Matcher** | 高（可重用Pattern） | 高 | 需要多次匹配或提取信息 |
| **Pattern.matches()** | 低（每次重新编译） | 中 | 简单的一次性检查 |

**推荐使用（Recommendations）**：
- **简单的一次性检查**：使用`String.matches()`或`Pattern.matches()`（Simple one-time check: use `String.matches()` or `Pattern.matches()`）
- **需要多次匹配**：使用`Pattern.compile()`创建Pattern对象，然后重用（Need to match multiple times: use `Pattern.compile()` to create Pattern object, then reuse）
- **需要提取匹配的部分**：使用`Pattern`和`Matcher`，配合`group()`方法（Need to extract matched parts: use `Pattern` and `Matcher` with `group()` method）

---

## 总结（Summary）

本总结涵盖了M4（设计模式和重构技术）和M5（伦理和正则表达式）的所有考试知识点（This summary covers all exam knowledge points for M4 (Design Patterns and Refactoring Techniques) and M5 (Ethics and Regex)）。每个问题都提供了中英文对照的详细答案（Each question provides detailed answers in both Chinese and English）。

