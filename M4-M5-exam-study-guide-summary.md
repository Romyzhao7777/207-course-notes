# M4和M5考试知识点总结
# M4 and M5 Exam Study Guide Summary

## [M4] Design Patterns

### What is a design pattern?
### 什么是设计模式？

**Answer / 答案：**

设计模式是对常见编程问题的流行解决方案的描述（Design patterns are descriptions of popular solutions to commonly-experienced programming problems）。如果实现的是不太方便的解决方案，我们称之为反模式（anti-pattern）（If a less convenient solution has been implemented instead, we call that an anti-pattern）。

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

- **Simple Factory（简单工厂）**：使用一个（通常是静态的）方法根据输入参数创建对象（Uses a (usually static) method to create objects based on input parameters）
- **Abstract Factory（抽象工厂）**：使用组合将实例化逻辑委托给另一个对象（Uses composition to delegate the instantiation logic to another object）。添加新类型时，只需要添加一个新的工厂子类，而不需要修改现有代码（When adding new types, you add a new factory subclass rather than modifying existing code）

**Builder Pattern（建造者模式）**

**问题（Problem）**：创建一个具有许多部分或选项的复杂对象会使你的代码混乱且难以阅读（Creating a complex object with many parts or options makes your code messy and hard to read）。

**解决方案（Solution）**：使用一个逐步的"builder"，逐步组装对象，然后给你完成的产品（Use a step-by-step "builder" that assembles the object piece by piece, then gives you the finished product）。

Builder模式的结构（Structure）：
- 创建一个"builder"对象（Create a "builder" object）
- 逐步添加部分（通过多次调用方法）（Add parts to it step-by-step by calling methods multiple times）
- 获得最终产品（通过调用builder的`build()`方法）（Get the final product by calling the builder's `build()` method）

例子：`StringBuilder`和`Okhttp`的`Request.Builder`（Examples: `StringBuilder` and `Okhttp`'s `Request.Builder`）

---

#### Behavioural patterns: Strategy, Observer
#### 行为型模式：Strategy, Observer

**Strategy Pattern（策略模式）**

**问题（Problem）**：你有几个算法来完成同一个任务，你想在它们之间轻松切换（You have several algorithms to do the same task, and you want to switch between them easily）。

**解决方案（Solution）**：在每个类中实现每个算法，使它们可以互换，这样你就可以在不改变使用它的代码的情况下改变算法（Implement each algorithm in its own class and make them interchangeable, so that you can change the algorithm without changing the code that uses it）。

例子：`Map`类使用`DirectionGenerator`接口作为Strategy，`DrivingDirections`和`TransitDirections`实现它（Example: `Map` class uses `DirectionGenerator` interface as Strategy, `DrivingDirections` and `TransitDirections` implement it）。在UML图中，`Map`是Context，`DirectionGenerator`是Strategy接口，`DrivingDirections`和`TransitDirections`是Concrete Strategies（In the UML diagram, `Map` is the Context, `DirectionGenerator` is the Strategy interface, and `DrivingDirections` and `TransitDirections` are the Concrete Strategies）。

**Observer Pattern（观察者模式）**

**问题（Problem）**：程序的多个部分需要在对象改变时做出反应，但你不想在这些部分和被观察的对象之间有紧耦合（Multiple parts of your program need to react when an object changes, but you don't want tight coupling between those parts and the object being observed）。

**解决方案（Solution）**：定义一对多的关系：当被观察的对象改变时，所有相关的对象都会收到通知，以便它们可以响应（Define a one-to-many relationship: when the observed object changes, all related objects get notified so that they can respond）。被观察的对象不需要知道观察它的对象的具体细节（The observed object doesn't need to know anything about the specifics of the objects observing it）。

例子：`JButton`组件的`ActionListener`对象（Example: `ActionListener` objects attached to `JButton` components）。在Clean Architecture中，ViewModel是Observable，View是Observer（In Clean Architecture, a ViewModel is an Observable, and a View is an Observer）。在Java中，使用`java.beans.PropertyChangeSupport`管理观察者列表（In Java, use `java.beans.PropertyChangeSupport` to manage observer list）。

---

#### Structural patterns: Façade, Adapter
#### 结构型模式：Façade, Adapter

**Façade Pattern（外观模式）**

**问题（Problem）**：子系统向客户端暴露许多类和操作，迫使它们处理不必要的复杂性（A subsystem exposes many classes and operations to clients, forcing them to deal with unnecessary complexity）。

**解决方案（Solution）**：创建一个简单的面向客户端的类（façade），为常见任务提供方法，同时隐藏子系统的复杂细节（Create a simple client-facing class (the façade) that provides methods for common tasks while hiding the subsystem's complex details）。

例子：`EmployeeFacade`类包含`EmployeeCalculator`、`EmployeeReporter`和`EmployeeSaver`，委托工作给这些对象（Example: `EmployeeFacade` class contains `EmployeeCalculator`, `EmployeeReporter`, and `EmployeeSaver`, delegates work to these objects）。

**Adapter Pattern（适配器模式）**

**问题（Problem）**：两个组件无法一起工作，因为它们的接口不匹配（Two components can't work together because their interfaces don't match）。这通常发生在你需要重用为不同上下文设计的现有类时（This often happens when you need to reuse an existing class that was designed for a different context）。

**解决方案（Solution）**：引入一个adapter（适配器）——一个在预期接口和现有接口之间进行转换的类（Introduce an adapter — a class that translates between the expected interface and the existing one）。

**实现方式（Implementation）**：
- **使用委托（With Delegation）**：适配器持有一个对遗留类的引用，并将工作委托给它（The adapter holds a reference to the legacy class and delegates work to it）
- **使用继承（With Inheritance）**：适配器扩展遗留类并添加代码以与预期接口保持一致（The adapter extends the legacy class and adds code to be consistent with the expected interface）

类比：USB-C转HDMI适配器（Analogy: USB-C to HDMI adapter）

---

### What are the classes involved in each of the above design patterns and what (if any) is their relationship?
### 每个设计模式涉及哪些类，它们之间有什么关系？

#### Factory Pattern（工厂模式）

**Simple Factory涉及的类（Classes involved）**：
- `ShapeFactory`：工厂类（Factory class）
- `Shape`：抽象产品接口（Abstract product interface）
- `Rectangle`, `Circle`, `Square`：具体产品类（Concrete product classes）

**关系（Relationships）**：`ShapeFactory`依赖`Shape`接口；`Rectangle`, `Circle`, `Square`实现`Shape`；客户端使用`ShapeFactory`创建`Shape`对象（`ShapeFactory` depends on `Shape` interface; `Rectangle`, `Circle`, `Square` implement `Shape`; Client uses `ShapeFactory` to create `Shape` objects）

**Abstract Factory涉及的类（Classes involved）**：
- `ShapeFactory`：抽象工厂类（Abstract factory class）
- `RectangleFactory`, `CircleFactory`, `SquareFactory`：具体工厂类（Concrete factory classes）
- `Shape`：抽象产品（Abstract product）
- `Rectangle`, `Circle`, `Square`：具体产品（Concrete products）

**关系（Relationships）**：具体工厂类继承抽象工厂类；每个具体工厂创建对应的具体产品；具体产品实现抽象产品接口（Concrete factory classes extend abstract factory class; Each concrete factory creates corresponding concrete products; Concrete products implement abstract product interface）

---

#### Builder Pattern（建造者模式）

**涉及的类（Classes involved）**：
- `Builder`：建造者类（Builder class）
- `Product`：要构建的产品类（Product class）
- `Director`（可选）：指导构建过程的类（Optional: Director class）

**关系（Relationships）**：`Builder`负责创建和组装`Product`的各个部分；`Builder`有`build()`方法返回最终的`Product`；客户端使用`Builder`逐步构建对象（`Builder` is responsible for creating and assembling parts of `Product`; `Builder` has a `build()` method that returns the final `Product`; Client uses `Builder` to build object step by step）

例子：`StringBuilder`是Builder，`String`是Product（Example: `StringBuilder` is the Builder, `String` is the Product）

---

#### Strategy Pattern（策略模式）

**涉及的类（Classes involved）**：
- `Context`：上下文类，使用策略（Context class that uses the strategy）
- `Strategy`：策略接口（Strategy interface）
- `ConcreteStrategyA`, `ConcreteStrategyB`：具体策略类（Concrete strategy classes）

**关系（Relationships）**：`Context`持有`Strategy`接口的引用；`ConcreteStrategyA`和`ConcreteStrategyB`实现`Strategy`接口；`Context`通过`Strategy`接口调用算法，可以在运行时切换不同的具体策略（`Context` holds a reference to `Strategy` interface; `ConcreteStrategyA` and `ConcreteStrategyB` implement `Strategy` interface; `Context` calls algorithm through `Strategy` interface, can switch between different concrete strategies at runtime）

例子：`Map`是Context，`DirectionGenerator`是Strategy接口，`DrivingDirections`和`TransitDirections`是Concrete Strategies（Example: `Map` is the Context, `DirectionGenerator` is the Strategy interface, `DrivingDirections` and `TransitDirections` are Concrete Strategies）

---

#### Observer Pattern（观察者模式）

**涉及的类（Classes involved）**：
- `Observable`（或`Subject`）：被观察的对象（The object being observed）
- `Observer`（或`Listener`）：观察者接口（Observer interface）
- `ConcreteObserverA`, `ConcreteObserverB`：具体观察者类（Concrete observer classes）

**关系（Relationships）**：`Observable`维护一个`Observer`列表；`ConcreteObserverA`和`ConcreteObserverB`实现`Observer`接口；当`Observable`的状态改变时，它通知所有注册的`Observer`（`Observable` maintains a list of `Observer`s; `ConcreteObserverA` and `ConcreteObserverB` implement `Observer` interface; When `Observable`'s state changes, it notifies all registered `Observer`s）

**在Java中的实现（Implementation in Java）**：`ViewModel`是Observable，使用`PropertyChangeSupport`管理观察者列表；`View`实现`PropertyChangeListener`接口，是Observer（`ViewModel` is Observable, uses `PropertyChangeSupport` to manage observer list; `View` implements `PropertyChangeListener` interface, is Observer）

---

#### Façade Pattern（外观模式）

**涉及的类（Classes involved）**：
- `Facade`：外观类，提供简化的接口（Facade class providing simplified interface）
- `SubsystemClassA`, `SubsystemClassB`, `SubsystemClassC`：子系统类（Subsystem classes）

**关系（Relationships）**：`Facade`持有对子系统类的引用；`Facade`的方法委托给相应的子系统类；客户端只与`Facade`交互（`Facade` holds references to subsystem classes; `Facade` methods delegate to appropriate subsystem classes; Clients only interact with `Facade`）

例子：`EmployeeFacade`是Facade，`EmployeeCalculator`, `EmployeeReporter`, `EmployeeSaver`是子系统类（Example: `EmployeeFacade` is the Facade, `EmployeeCalculator`, `EmployeeReporter`, `EmployeeSaver` are subsystem classes）

---

#### Adapter Pattern（适配器模式）

**使用委托的Adapter（Adapter with Delegation）**：
- `Adapter`：适配器类（Adapter class）
- `Adaptee`：需要适配的遗留类（Legacy class）
- `Target`：目标接口（Target interface）

**关系（Relationships）**：`Adapter`实现`Target`接口；`Adapter`持有`Adaptee`的引用；`Adapter`将`Target`接口的调用转换为`Adaptee`的方法调用（`Adapter` implements `Target` interface; `Adapter` holds a reference to `Adaptee`; `Adapter` converts `Target` interface calls to `Adaptee` method calls）

**使用继承的Adapter（Adapter with Inheritance）**：
- `Adapter`继承`Adaptee`并实现`Target`接口（`Adapter` extends `Adaptee` and implements `Target` interface）

例子：`MovieTicket`是Adapter，`Ticket`是Adaptee，`Tradable`是Target接口（Example: `MovieTicket` is the Adapter, `Ticket` is the Adaptee, `Tradable` is the Target interface）

---

### What is an anti-pattern? What might the anti-pattern of each design pattern above look like?
### 什么是反模式？每个设计模式的反模式可能是什么样子？

**什么是反模式（What is an anti-pattern）**：

反模式是设计模式的反面——它们是对常见编程问题的不太方便的解决方案（Anti-patterns are the opposite of design patterns — they are less convenient solutions to commonly-experienced programming problems）。如果代码显示了反模式，你可以通过重构来实现设计模式来改进代码的设计（If code displays an anti-pattern, you can improve the design of the code by refactoring to implement a design pattern instead）。

**各模式的反模式（Anti-patterns）**：

- **Factory Pattern的反模式**：客户端代码直接使用`new`关键字创建具体类，导致紧耦合（Client code directly uses `new` keyword to create concrete classes, causing tight coupling）
- **Builder Pattern的反模式**：使用一个有很多参数的构造函数（Using a constructor with many parameters）
- **Strategy Pattern的反模式**：在类中使用大量的if-else或switch语句来选择不同的算法（Using many if-else or switch statements in a class to choose between different algorithms）
- **Observer Pattern的反模式**：被观察的对象直接调用观察者的方法，导致紧耦合（The observed object directly calls observer methods, causing tight coupling）
- **Façade Pattern的反模式**：客户端直接与多个子系统类交互（Client directly interacts with multiple subsystem classes）
- **Adapter Pattern的反模式**：修改遗留类以匹配新接口（Modifying legacy class to match new interface）

---

### What is the difference between a "refactoring technique" and any other modification to a class or program?
### "重构技术"和其他对类或程序的修改有什么区别？

**Answer / 答案：**

重构（refactoring）是指程序员进行一系列改进软件设计的更改——但不改变行为（Refactoring refers to when programmers make a series of changes that improve the design of the software — but without changing the behaviour）。

**关键区别（Key Differences）**：

1. **不改变行为（No behavior change）**：重构只改变代码的结构和设计，不改变程序的功能（Refactoring only changes code structure and design, does not change program functionality）。重构后的代码应该通过所有现有的测试（Refactored code should pass all existing tests）

2. **改进设计（Improves design）**：重构的目的是让代码更容易理解、导航和调试，更容易自动测试，更容易添加新功能（The purpose of refactoring is to make code easier to understand, navigate, debug, automatically test, and add new features）

3. **系统化的技术（Systematic techniques）**：重构技术是经过验证的、系统化的方法来改进代码（Refactoring techniques are proven, systematic methods to improve code）

**其他修改（Other modifications）**：添加新功能、修复bug、性能优化都会改变程序的行为（Adding new features, fixing bugs, performance optimization all change program behavior）

**规则（Rule）**：重构时，代码应该始终通过现有的测试（When refactoring, the code should always pass the existing tests）！

---

### Explain how each refactoring technique works
### 解释每个重构技术如何工作

#### Extract Method（提取方法）

将一段代码从方法中提取出来，创建一个新的辅助方法（Extract a block of code from a method and create a new helper method）。原始方法调用这个新方法（The original method calls this new method）。

**步骤（Steps）**：选择要提取的代码块；创建一个新方法，将选中的代码移到新方法中；用新方法调用替换原始代码；根据目的和上下文，可以选择将新方法设为private和可能static（Select the block of code to extract; Create a new method and move selected code to it; Replace original code with call to new method; May choose to make it private and possibly static）

**好处（Benefits）**：代码更易读；可以重用提取的方法；更容易测试（Code is more readable; Extracted method can be reused; Easier to test）

---

#### Change Method Declaration（更改方法声明）

修改方法的定义，比如改变参数、返回类型或方法名（Modify how a method is defined, such as altering its parameters, return type, or method name）。必须小心更新任何客户端代码以及被修改的方法体（One must be careful to update any client code, as well as the body of the method being altered）。

**在IntelliJ中（In IntelliJ）**：使用`Change Signature`功能来执行这种重构（Use `Change Signature` feature to perform this refactoring）

---

#### Encapsulate Fields（封装字段）

将实例变量的访问修饰符改为private，并引入getter和setter方法来提供适当的访问（Change access modifiers on instance variables to private, and introduce getters and setters to provide appropriate access）。更新任何客户端或实现代码，使用getter和setter，而不是直接访问数据（Update any client or implementation code to use getters and setters where data was directly accessed previously）。

**在IntelliJ中（In IntelliJ）**：选择字段，然后选择`Refactoring -> Encapsulate Fields...`（Select fields, then choose `Refactoring -> Encapsulate Fields...`）

---

#### Split Loop（拆分循环）

将一个执行多个计算的循环拆分成多个独立的循环，每个循环执行一个独立的计算（Split a loop that performs multiple computations into separate loops, each performing an independent computation）。

**好处（Benefits）**：每个循环职责单一；更容易应用Extract Method；代码更易理解（Each loop has a single responsibility; Easier to apply Extract Method; Code is more understandable）

---

#### Slide Statements（滑动语句）

移动代码行，以更有意义的方式将代码分组在一起（Move lines of code around to help group together code in more meaningful ways）。例如，将每个累加器变量的声明移到对应的累加器循环之前（For example, move the declaration of each accumulator variable so that they are defined immediately before each of their corresponding accumulator loops）。

**在IntelliJ中（In IntelliJ）**：使用Alt+Shift+Up/Down移动当前行（Use Alt+Shift+Up/Down to move current line）

---

#### Replace Constructor with Builder（用Builder替换构造函数）

重构对象的构造方式，引入一个builder类，负责分步构建类的实例（Refactor how objects are constructed by introducing a builder class that is responsible for constructing instances of the class in steps）。

**好处（Benefits）**：代码更易读；参数顺序不重要；可选参数更容易处理（Code is more readable; Parameter order doesn't matter; Optional parameters are easier to handle）

---

#### Replace Constructor with Factory Method（用工厂方法替换构造函数）

重构对象的构造方式，引入一个静态方法，负责返回类的实例，而不是让代码直接调用构造函数（Refactor how objects are constructed by introducing a static method that is responsible for returning the instance of the class rather than having the code directly call the constructor）。

**好处（Benefits）**：方法名可以更清楚地表达意图；可以返回子类实例；可以控制实例的创建；隐藏构造函数调用的细节（Method name can clearly express intent; Can return subclass instances; Can control instance creation; Hides detail of how instance is created）

---

### Which design patterns are built into Clean Architecture? In other words, if you implement Clean Architecture, which design patterns will necessarily appear in your code?
### Clean Architecture中内置了哪些设计模式？换句话说，如果你实现Clean Architecture，哪些设计模式必然会在你的代码中出现？

**Answer / 答案：**

Clean Architecture的实现中必然会出现以下设计模式（The following design patterns will necessarily appear in Clean Architecture implementations）：

#### 1. Dependency Injection（依赖注入）

Clean Architecture要求依赖必须指向内层（Clean Architecture requires dependencies to point inward）。内层定义接口，外层实现接口（Inner layers define interfaces, outer layers implement interfaces）。这意味着依赖必须通过构造函数或方法参数注入，而不是在类内部直接创建（This means dependencies must be injected through constructors or method parameters, not created directly inside classes）。

#### 2. Observer Pattern（观察者模式）

在Clean Architecture中，ViewModel是Observable，View是Observer（In Clean Architecture, ViewModel is Observable, View is Observer）。当ViewModel的状态改变时，View需要更新以反映新数据（When ViewModel's state changes, View needs to update to reflect new data）。在Java中，使用`PropertyChangeSupport`管理观察者列表（In Java, use `PropertyChangeSupport` to manage observer list）。

#### 3. Adapter Pattern（适配器模式）

Clean Architecture的Interface Adapters层本质上就是Adapter模式的体现（The Interface Adapters layer in Clean Architecture is essentially an embodiment of the Adapter pattern）。Controller、Presenter都是适配器，它们将数据从一种格式转换为另一种格式（Controller and Presenter are adapters that convert data from one format to another）。

#### 4. Strategy Pattern（策略模式，可能）

虽然Strategy模式不是Clean Architecture的必需部分，但它经常出现在Use Case层（Although Strategy pattern is not a required part of Clean Architecture, it often appears in the Use Case layer）。

#### 5. Factory Pattern（工厂模式，可能）

Main组件（或Driver）负责创建和组装所有对象（The Main component (or Driver) is responsible for creating and assembling all objects）。这可以使用Factory模式来实现（This can be implemented using the Factory pattern）。

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

在软件设计中，理解言语行为有助于设计更好的用户界面和交互（In software design, understanding speech acts helps design better user interfaces and interactions）。例如，按钮上的文字"保存"是一个命令，而"已保存"是一个状态声明（For example, the text "Save" on a button is a command, while "Saved" is a state declaration）。

---

### What is the difference between material and relational harm?
### 物质伤害和关系伤害的区别是什么？

**Answer / 答案：**

**物质伤害（Material Harm）**：对个人或群体的物质资源、财产或身体造成的实际损害（Actual damage to an individual's or group's material resources, property, or physical well-being）。这种伤害是可见的、可量化的（This harm is visible and quantifiable）。

**例子（Examples）**：经济损失（Financial loss）、身体伤害（Physical harm）、数据丢失（Data loss）、隐私泄露（Privacy breach）

**关系伤害（Relational Harm）**：对个人或群体的社会关系、声誉、尊严或社会地位造成的损害（Damage to an individual's or group's social relationships, reputation, dignity, or social status）。这种伤害影响的是人与人之间的关系和社会地位（This harm affects relationships between people and social status）。

**例子（Examples）**：声誉损害（Reputation damage）、社会排斥（Social exclusion）、尊严受损（Dignity harm）、关系破裂（Relationship breakdown）

**如何识别（How to identify）**：
- **识别物质伤害**：是否有经济损失？是否有身体伤害？是否有资源损失？伤害是否可以直接测量？（Is there financial loss? Physical harm? Resource loss? Can the harm be directly measured?）
- **识别关系伤害**：是否影响社会关系？是否损害声誉？是否影响尊严或自尊？是否导致社会排斥或边缘化？（Does it affect social relationships? Damage reputation? Affect dignity or self-esteem? Cause social exclusion or marginalization?）

---

### What are the similarities and differences between the medical and social models of disability?
### 医疗模式和社会模式的残疾模型有什么相似之处和不同之处？

**Answer / 答案：**

**医疗模式（Medical Model）**：将残疾视为个人身体或心理的缺陷或疾病（Views disability as a defect or disease in an individual's body or mind）。这种模式认为残疾是个人需要"修复"或"治疗"的问题（This model sees disability as a problem that the individual needs to "fix" or "treat"）。

**特点（Characteristics）**：残疾是个人问题；重点在于"修复"个人；残疾被视为异常或缺陷；解决方案是医疗干预或康复（Disability is an individual problem; Focus on "fixing" the individual; Disability is seen as abnormal or defective; Solution is medical intervention or rehabilitation）

**社会模式（Social Model）**：将残疾视为社会和环境障碍的结果，而不是个人缺陷（Views disability as a result of social and environmental barriers, not individual defects）。这种模式认为社会应该适应和包容所有人（This model believes society should adapt and include everyone）。

**特点（Characteristics）**：残疾是社会问题；重点在于消除社会和环境障碍；残疾是正常的人类多样性的一部分；解决方案是改变环境和社会（Disability is a social problem; Focus on removing social and environmental barriers; Disability is part of normal human diversity; Solution is changing environment and society）

**相似之处（Similarities）**：都承认残疾的存在；都试图改善残疾人的生活；都涉及医疗和社会支持（Both acknowledge the existence of disability; Both attempt to improve the lives of people with disabilities; Both involve medical and social support）

**不同之处（Differences）**：

| 方面 | 医疗模式 | 社会模式 |
|------|---------|---------|
| **问题所在** | 个人 | 社会和环境 |
| **解决方案** | 治疗个人 | 改变社会和环境 |
| **责任** | 个人 | 社会 |
| **视角** | 残疾是缺陷 | 残疾是多样性 |
| **目标** | 修复个人 | 包容所有人 |

**在软件设计中的应用（Application in Software Design）**：
- **医疗模式的方法**：为残疾人创建"特殊"功能；认为用户需要适应软件（Create "special" features for people with disabilities; Users need to adapt to software）
- **社会模式的方法**：设计所有人都能使用的软件；遵循通用设计原则；消除软件中的障碍（Design software that everyone can use; Follow universal design principles; Remove barriers in software）

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
5. **容错性（Tolerance for Error）**：设计将危险和意外操作的后果降至最低（Design minimizes hazards and the adverse consequences of accidental or unintended actions）
6. **低体力消耗（Low Physical Effort）**：可以高效舒适地使用，减少疲劳（Can be used efficiently and comfortably with minimum fatigue）
7. **尺寸和空间（Size and Space）**：无论用户的身体尺寸、姿势或移动性如何，都提供适当的大小和空间（Appropriate size and space provided regardless of user's body size, posture, or mobility）

**如何在软件设计中应用（How to apply in Software Design）**：
- **可访问性（Accessibility）**：提供键盘导航、支持屏幕阅读器、使用足够的颜色对比度、提供文本替代图片（Provide keyboard navigation, support screen readers, use sufficient color contrast, provide text alternatives for images）
- **灵活性（Flexibility）**：允许用户自定义界面、提供多种输入方式、支持不同的显示偏好（Allow users to customize interface, provide multiple input methods, support different display preferences）
- **简单性（Simplicity）**：清晰的导航、直观的界面、一致的交互模式（Clear navigation, intuitive interface, consistent interaction patterns）
- **信息传达（Information Communication）**：清晰的错误消息、多种信息呈现方式、适当的反馈（Clear error messages, multiple ways to present information, appropriate feedback）
- **容错性（Error Tolerance）**：确认危险操作、提供撤销功能、清晰的错误恢复（Confirm dangerous actions, provide undo functionality, clear error recovery）

---

### What are the basic regular expression (regex) symbols that we covered in the reading and/or in lecture?
### 我们在阅读和/或课程中涉及的基本正则表达式（regex）符号有哪些？

**Answer / 答案：**

**基本正则表达式符号（Basic Regular Expression Symbols）**：

1. **`.`（点号）**：匹配除换行符外的任何单个字符（Matches any single character except newline）
2. **`^`（脱字符）**：匹配字符串的开始（Matches the beginning of the string）
3. **`$`（美元符号）**：匹配字符串的结束（Matches the end of the string）
4. **`*`（星号）**：匹配前面的字符零次或多次（Matches the preceding character zero or more times）
5. **`+`（加号）**：匹配前面的字符一次或多次（Matches the preceding character one or more times）
6. **`?`（问号）**：匹配前面的字符零次或一次（Matches the preceding character zero or one time）
7. **`[]`（字符类）**：匹配方括号内的任何一个字符（Matches any one character inside the square brackets）
   - `[a-z]` 匹配任何小写字母（Matches any lowercase letter）
   - `[0-9]` 匹配任何数字（Matches any digit）
8. **`[^]`（否定字符类）**：匹配不在方括号内的任何字符（Matches any character not inside the square brackets）
9. **`|`（管道符）**：表示"或"，匹配左边或右边的模式（Represents "or", matches the pattern on the left or right）
10. **`()`（分组）**：将多个字符组合在一起（Groups multiple characters together）
11. **`\`（转义符）**：转义特殊字符，使其按字面意思匹配（Escapes special characters to match them literally）
12. **`\d`**：匹配任何数字，等价于 `[0-9]`（Matches any digit, equivalent to `[0-9]`）
13. **`\w`**：匹配任何单词字符（字母、数字、下划线），等价于 `[a-zA-Z0-9_]`（Matches any word character (letter, digit, underscore), equivalent to `[a-zA-Z0-9_]`）
14. **`\s`**：匹配任何空白字符（空格、制表符、换行符等）（Matches any whitespace character (space, tab, newline, etc.)）
15. **`{n}`**：匹配前面的字符恰好n次（Matches the preceding character exactly n times）
16. **`{n,}`**：匹配前面的字符至少n次（Matches the preceding character at least n times）
17. **`{n,m}`**：匹配前面的字符至少n次，最多m次（Matches the preceding character at least n times, at most m times）

---

### How can we write a regular expression that matches a set of Strings?
### 如何编写匹配一组字符串的正则表达式？

**Answer / 答案：**

**步骤（Steps）**：
1. **分析字符串的共同模式（Analyze common patterns）**：识别固定部分和可变部分；识别重复模式；识别可选部分（Identify fixed parts and variable parts; Identify repeating patterns; Identify optional parts）
2. **使用适当的符号（Use appropriate symbols）**：固定文本直接写；使用字符类 `[]` 匹配一组字符；使用量词 `*`, `+`, `?`, `{n}` 匹配重复；使用 `|` 表示"或"；使用 `()` 分组（Write fixed text directly; Use character class `[]` to match a set of characters; Use quantifiers `*`, `+`, `?`, `{n}` to match repetitions; Use `|` for "or"; Use `()` for grouping）
3. **测试和调整（Test and adjust）**：测试正则表达式是否匹配所有目标字符串；确保不匹配不应该匹配的字符串（Test if regex matches all target strings; Ensure it doesn't match strings it shouldn't）

**例子（Examples）**：
- 邮箱地址：`[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}`
- 电话号码：`\d{3}-\d{3}-\d{4}`（格式：123-456-7890）
- 以特定前缀开头：`^(user|admin|guest)_\d+`（匹配：user_123, admin_456, guest_789）

---

### How can we find a String that conforms to a given regular expression?
### 如何找到符合给定正则表达式的字符串？

**Answer / 答案：**

**方法（Methods）**：
1. **手动构造（Manual construction）**：理解正则表达式的含义；根据模式构造字符串；确保字符串匹配所有要求（Understand what the regex means; Construct string according to the pattern; Ensure string matches all requirements）
2. **使用工具（Using tools）**：使用在线正则表达式测试工具；使用正则表达式生成器（Use online regex testing tools; Use regex generators）
3. **系统化方法（Systematic approach）**：从左到右分析正则表达式；为每个部分构造对应的字符串；组合各部分（Analyze regex from left to right; Construct corresponding string for each part; Combine all parts）

**例子（Example）**：给定正则表达式：`^[A-Z][a-z]+\d{2,3}$`
- 符合的字符串：`"Hello12"`, `"World123"`, `"Java99"` ✅
- 不符合的字符串：`"hello12"`（不是以大写字母开头）❌，`"Hello1"`（数字少于2个）❌

---

### What do we have to do to a regular expression to use it in a Java program?
### 在Java程序中使用正则表达式需要做什么？

**Answer / 答案：**

1. **转义特殊字符（Escape special characters）**：在Java字符串中，反斜杠 `\` 是转义字符（In Java strings, backslash `\` is an escape character）。正则表达式中的 `\` 需要写成 `\\`（`\` in regex needs to be written as `\\`）。例如：正则表达式 `\d` 在Java中写成 `"\\d"`（For example: regex `\d` is written as `"\\d"` in Java）

2. **使用Pattern和Matcher类（Use Pattern and Matcher classes）**：
   ```java
   // 1. 编译正则表达式（Compile the regex）
   Pattern pattern = Pattern.compile("your_regex_here");
   
   // 2. 创建Matcher对象（Create Matcher object）
   Matcher matcher = pattern.matcher("string_to_match");
   
   // 3. 执行匹配（Perform matching）
   boolean matches = matcher.matches();
   ```

**注意事项（Notes）**：Java字符串中的 `\\` 表示一个反斜杠（`\\` in Java string represents one backslash）；使用 `Pattern.compile()` 编译正则表达式可以提高性能（Using `Pattern.compile()` to compile regex improves performance）

---

### What are three ways of checking if a String conforms to a regular expression in Java?
### 在Java中检查字符串是否符合正则表达式有哪三种方法？

**Answer / 答案：**

#### 方法1：使用String.matches()方法
#### Method 1: Using String.matches() method

**语法（Syntax）**：`boolean matches = string.matches(regex);`

**特点（Characteristics）**：最简单直接的方法；自动编译正则表达式；每次调用都会重新编译，性能较低；只检查整个字符串是否匹配（Simplest and most direct method; Automatically compiles the regex; Recompiles on each call, lower performance; Only checks if entire string matches）

#### 方法2：使用Pattern和Matcher类
#### Method 2: Using Pattern and Matcher classes

**语法（Syntax）**：
```java
Pattern pattern = Pattern.compile(regex);
Matcher matcher = pattern.matcher(string);
boolean matches = matcher.matches();
```

**特点（Characteristics）**：更灵活，可以执行多种操作；可以重用Pattern对象，性能更好；可以使用`find()`查找部分匹配；可以使用`group()`提取匹配的部分（More flexible, can perform various operations; Can reuse Pattern object, better performance; Can use `find()` to find partial matches; Can use `group()` to extract matched parts）

#### 方法3：使用Pattern.matches()静态方法
#### Method 3: Using Pattern.matches() static method

**语法（Syntax）**：`boolean matches = Pattern.matches(regex, string);`

**特点（Characteristics）**：静态方法，使用方便；内部使用Pattern和Matcher；每次调用都会重新编译，性能较低；只检查整个字符串是否匹配（Static method, convenient to use; Internally uses Pattern and Matcher; Recompiles on each call, lower performance; Only checks if entire string matches）

**三种方法的比较（Comparison）**：

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

本总结涵盖了M4（设计模式和重构技术）和M5（伦理和正则表达式）的所有考试知识点（This summary covers all exam knowledge points for M4 (Design Patterns and Refactoring Techniques) and M5 (Ethics and Regex)）。每个问题都提供了中英文对照的答案（Each question provides answers in both Chinese and English）。
