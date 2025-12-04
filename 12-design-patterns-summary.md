# Chapter 12: Design Patterns - 知识点总结

## 12.1 什么是设计模式（What is a Design Pattern）？

• **Design patterns（设计模式）**是对常见编程问题的流行解决方案的描述。如果实现的是不太方便的解决方案，我们称之为**anti-pattern（反模式）**。如果代码显示了反模式，你可以通过重构来实现设计模式来改进代码的设计

• 设计模式描述的是代码的结构而不是细节。它们是一种交流设计思想的手段。它们不特定于任何单一编程语言，因此 UML 图可以自然地用来解释设计模式的结构

• 设计模式的概念最初由 **Gang of Four（四人帮）**在 1995 年发表。原书描述了 23 种模式：11 种行为型、5 种创建型和 7 种结构型模式。自那时起，更多的模式被添加，其他作者也写了许多关于这个主题的书籍

• 在本课程中，我们将重点学习三类模式，每类两个示例模式：**Creational Patterns（创建型模式）**、**Behavioural Patterns（行为型模式）**和**Structural Patterns（结构型模式）**

## 12.1.1 与设计原则的关系（Relation to Design Principles）

• 就像我们刚刚学到的 Clean Architecture，设计模式实际上只是底层原则的应用，比如"低耦合高内聚"和 SOLID 原则

• 设计模式建立在设计原则之上，就像数学定理建立在公理之上一样。设计原则（如 SOLID）是基础指导原则，它们旨在非常通用。设计模式是通过将设计原则应用到常见问题而建立的解决方案，它们旨在比其底层原则更实用、更少抽象

• 学习设计模式的好处是获得一种通用语言，用来与其他程序员交流更复杂的设计思想。如果已经有人通过仔细、严格地应用一组原则证明了某个模式的有效性，我们就不需要重复这项工作，而是可以直接使用他们的结果并应用到我们的任务中

## 12.1.2 类比：数学公理和定理（An Analogy: Mathematical Axioms and Theorems）

• 在数学中，**axioms（公理）**是不需要证明就被假设为真的基础真理。在软件设计中，设计原则（如 SOLID）是我们遵循以构建"好的"系统的基础指导原则。这些原则旨在非常通用

• 在数学中，**theorems（定理）**是从公理推导出来的证明结果。在软件中，设计模式是通过将设计原则应用到常见问题而建立的解决方案。这些模式旨在比其底层原则更实用、更少抽象

• 示例：
  - 公理：通过任意两点，恰好有一条直线
  - 原则：一个类应该只有一个改变的理由
  - 定理：三角形内角和为 180°
  - 模式：Observer 模式解决了当一个对象改变时如何通知多个对象的问题

## 12.2 创建型模式（Creational Patterns）

• **创建型模式**专注于对象的创建。这些模式帮助避免常见的陷阱，如紧耦合、过度使用构造函数，以及引入系统硬依赖的不灵活的实例化逻辑

• 从根本上说，创建型模式解决了 `new MyClass(...)` 调用应该在我们代码的哪里发生，以及创建的对象如何连接在一起的问题。换句话说，这些模式解决了**谁负责创建系统中的每个对象？**这个问题

• Factory 和 Builder 模式是创建型模式的两个代表性示例

### 12.2.1 Factory（工厂模式）

• **问题（Problem）**：你需要创建都是同一抽象的子类或实现类的对象，但你不想让你的代码依赖于确切的类名或它们是如何构建的

• **解决方案（Solution）**：使用一个特殊的"factory"对象或方法，决定创建哪个类并返回一个可直接使用的实例

• **Factory 模式的几种变体**：
  1. **Simple Factory（简单工厂）**模式：使用一个（通常是静态的）方法根据输入参数创建对象。它可以生成共享共同接口或超类的不同具体类型
  2. **Factory Method（工厂方法）**模式：使用继承允许子类决定实例化哪个具体类
  3. **Abstract Factory（抽象工厂）**模式：使用组合将实例化逻辑委托给另一个对象。这创建了一个或多个相关对象的家族

• 在本课程中，我们重点学习 Simple Factory 和 Abstract Factory

#### Simple Factory 示例

• 如果你的程序需要 `Shape` 对象，但不需要知道它们是矩形、圆形、三角形或你可能想在将来包含的任何其他形状，你可以使用 `ShapeFactory` 类来实例化这些类。工厂类使用 `switch` 语句根据输入字符串决定创建哪种形状，客户端代码只需要传入字符串即可获得对应的形状对象

• Simple Factory 的 `getShape` 方法有时可以定义为**static（静态）**，在这种情况下，代码简化为 `Shape shape = ShapeFactory.getShape(userInput);`，因为根本不需要创建 `ShapeFactory` 的实例

#### Abstract Factory 示例

• 使用 Simple Factory 时，我们最终会在 `ShapeFactory.getShape` 方法内部根据请求的形状类型使用条件逻辑。添加新形状时，这意味着我们需要修改这个方法

• Abstract Factory 可以用来将这种条件逻辑完全移出这个方法。这意味着用户将在创建工厂**之前**指定他们想要创建的形状类型

• Abstract Factory 的结构：
  - 首先定义一个抽象类 `ShapeFactory`，定义什么是"形状工厂"
  - 然后为每种想要创建的形状定义子类（如 `RectangleFactory`、`CircleFactory`、`SquareFactory`）
  - 客户端代码选择要使用的工厂来创建它想要的 `Shape`

• 如果我们根据用户输入决定使用哪个工厂，那么 Simple Factory 版本中的条件逻辑会再次出现，但这段逻辑在代码中出现的位置已经改变了。最重要的是，一旦我们确定了要使用哪个工厂，代码的其他地方就不再有任何条件逻辑了

#### Simple Factory 和 Abstract Factory 的比较

• **创建逻辑（Creation logic）**：
  - Simple Factory：全部在一个类中
  - Abstract Factory：分布在各个子类中

• **添加新类型（Adding new types）**：
  - Simple Factory：添加一个新的 if-statement（修改现有代码）
  - Abstract Factory：添加一个新的工厂子类（扩展现有代码）

• **客户端使用（Client usage）**：
  - Simple Factory：客户端通过 String 参数指定类型
  - Abstract Factory：客户端选择工厂

### 12.2.2 Builder（建造者模式）

• **问题（Problem）**：创建一个具有许多部分或选项的复杂对象会使你的代码混乱且难以阅读

• **解决方案（Solution）**：使用一个逐步的"builder"，逐步组装对象，然后给你完成的产品

• Builder 模式的结构：
  - 创建一个"builder"对象
  - 逐步添加部分（通过多次调用方法，如 `append()` 或 `addHeader()`）
  - 获得最终产品（通过调用 builder 的 `build()` 或 `toString()` 方法）

• 你可能在 `StringBuilder` 和 `Okhttp` 的 `Request.Builder` 中见过这个模式。它们都展示了相同的序列：创建 builder，执行一系列步骤来自定义正在创建的对象，然后最终调用以返回对象

• IntelliJ 包含一个重构功能，可以[用 builder 替换构造函数](https://www.jetbrains.com/help/idea/replace-constructor-with-builder.html)

## 12.3 行为型模式（Behavioural Patterns）

• **行为型模式**专注于对象如何交互和通信。它们解决了**职责和行为如何在系统中的对象之间分布，以及这些对象如何通信以完成工作？**这个问题

• Strategy 和 Observer 模式是行为型模式的两个代表性示例

### 12.3.1 Strategy（策略模式）

• **问题（Problem）**：你有几个算法来完成同一个任务，你想在它们之间轻松切换

• **解决方案（Solution）**：在每个类中实现每个算法，使它们可以互换，这样你就可以在不改变使用它的代码的情况下改变算法

• 例如，考虑一个需要 `getDirections` 方法的 `Map` 类，该方法应该根据方向是用于驾驶还是公共交通返回不同的 `String`。我们可以定义一个 `DirectionGenerator` 接口作为 Strategy，让 `DrivingDirections` 和 `TransitDirections` 类实现它。当 `Map` 类被实例化时，它被赋予一个实现 Strategy 的对象

• 在 UML 图中，`Map` 是 Context（上下文），`DirectionGenerator` 是 Strategy 接口，`DrivingDirections` 和 `TransitDirections` 是 Concrete Strategies（具体策略）

• 设置使用哪个 Strategy 通常通过构造函数（如示例中）或 setter（如 UML 类图中）来完成。Strategy 通常对应于可能在多个上下文中有用的代码

### 12.3.2 Observer（观察者模式）

• **问题（Problem）**：程序的多个部分需要在对象改变时做出反应，但你不想在这些部分和被观察的对象之间有紧耦合

• **解决方案（Solution）**：定义一对多的关系：当被观察的对象改变时，所有相关的对象都会收到通知，以便它们可以响应。被观察的对象不需要知道观察它的对象的具体细节

• 例如，考虑我们附加到 `JButton` 组件的 `ActionListener` 对象。当按钮被点击（事件）时，监听器的 `actionPerformed` 方法被调用（反应）

#### ViewModel 示例

• 记住 Clean Architecture 中的 View 部分？每个 View 都有一个对应的 ViewModel，它保存要显示的数据。当 ViewModel 中的数据改变时，View 需要更新自己以反映新数据。这可以使用 Observer 模式完成：每个 View 将观察它的 ViewModel

• 在 UML 类图中，Observable 的工作是在它改变时通知所有它的 Observers。在我们的示例中，ViewModel 是一个 Observable，View 是一个 Observer

• 在 Java 中，这通常通过让 Observable 使用 `java.beans.PropertyChangeSupport` 对象来实现，它管理一个 `PropertyChangeListener` 对象（Observers）列表，这样你就不必自己编写管理 Observers 列表的代码

• 当 Observable 的状态改变时，它调用其 `PropertyChangeSupport` 对象的 `firePropertyChange` 方法，该方法又调用每个 PropertyChangeListener 的 `propertyChange` 方法

• View 实现 `PropertyChangeListener` 接口，当 ViewModel 的状态改变时，View 的 `propertyChange` 方法会被调用，View 可以根据新状态更新自己的字段

## 12.4 结构型模式（Structural Patterns）

• **结构型模式**专注于类和对象如何组合形成更大的系统。与处理**如何创建对象**的创建型模式和处理**对象如何交互和共享职责**的行为型模式不同，结构型模式解决了**如何连接和组织对象以协同工作？**这个问题

• 结构型模式通常解决诸如为复杂的子系统呈现简化的统一接口或适配不兼容的接口等问题。我们将考虑 Adapter 和 Façade 模式作为结构型模式的两个代表性示例

### 12.4.1 Façade（外观模式）

• **问题（Problem）**：子系统向客户端暴露许多类和操作，迫使它们处理不必要的复杂性

• **解决方案（Solution）**：创建一个简单的面向客户端的类（**façade**），为常见任务提供方法，同时隐藏子系统的复杂细节

• 例如，你可能还记得 SOLID 原则幻灯片中"单一职责原则"部分的 `EmployeeFacade` 类，它包含类型为 `EmployeeCalculator`、`EmployeeReporter` 和 `EmployeeSaver` 的变量。当你调用 `employee.calculatePay()` 时，它通过调用 `payCalculator.calculatePay()` 来委托工作给相应的对象，这是一个单行委托

• Façade 类的方法以相同的方式结构化，它们委托给适当的对象。这样，客户端不需要知道底层的复杂性，只需要与简单的 Façade 接口交互

• 在构建 façade 时，创建型模式（如 Builder）可以用于以系统化的方式组装其内部组件

### 12.4.2 Adapter（适配器模式）

• **问题（Problem）**：两个组件无法一起工作，因为它们的接口不匹配。这通常发生在你需要重用为不同上下文设计的现有类时

• **解决方案（Solution）**：引入一个**adapter（适配器）**——一个在预期接口和现有接口之间进行转换的类。适配器暴露你的客户端代码期望的接口，并在内部将调用转发到遗留类，根据需要转换输入和输出

• **类比**：想想 USB-C 转 HDMI 适配器。许多笔记本电脑可以通过 USB-C 输出视频，但你的显示器只接受 HDMI 输入。适配器不会改变笔记本电脑或显示器——它只是在两个接口之间进行转换，使它们能够协同工作

• Adapter 模式可以通过两种方式实现：

#### 使用委托（With Delegation）

• 适配器持有一个对遗留类的引用，并将工作委托给它。例如，如果我们有一个用于彩票程序的 `Ticket` 类，想要在电影票程序中重用它，我们可以创建一个 `MovieTicket` 类，它持有一个 `Ticket` 实例，委托调用给它，并添加新功能（如座位号），而不修改原始的 `Ticket` 类

#### 使用继承（With Inheritance）

• 适配器扩展遗留类并添加代码以与预期接口保持一致。例如，`MovieTicket` 可以扩展 `Ticket`，通过调用 `super.sell()` 重用父类的 sell 方法，并添加额外的行为（如打印座位号）

• 两种方法都可以实现适配，选择哪种方法取决于具体情况和设计约束

## 12.5 总结（Summary）

• 以下是本章涵盖的三类设计模式的简要总结：

| **模式类别** | **焦点** | **关键问题** | **代表性模式** |
|------------|---------|------------|--------------|
| **Creational（创建型）** | 对象创建 | 谁负责创建系统中的每个对象？ | Factory, Builder |
| **Behavioral（行为型）** | 对象交互和通信 | 职责和行为如何在对象之间分布，对象如何通信以完成工作？ | Strategy, Observer |
| **Structural（结构型）** | 对象和类的组织 | 如何连接和组织对象以协同工作？ | Adapter, Façade |

## 12.6 代码示例（Code Examples）

• 演示上述模式及其反模式的可运行代码示例包含在 `code/design_patterns` 目录中。如果你在 IntelliJ 中将 `code` 标记为源根，你可以尝试运行代码

• **提示**：你还可以为代码生成 UML 类图，以帮助可视化模式的结构

## 思考问题

• 在阅读每个设计模式时，思考如何使用我们学习的一个或多个原则来"推导"每个模式

• 你能识别出 Clean Architecture 设计的特定方面，它们让你想起每个 SOLID 原则吗？

• 设计模式和设计原则之间的关系，就像数学中的定理和公理一样，你觉得这个类比如何帮助你理解设计模式的价值？


