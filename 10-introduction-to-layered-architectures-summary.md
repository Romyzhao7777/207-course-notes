# Chapter 10: Introduction to Layered Architectures - 知识点总结

## 核心概念：低耦合高内聚（Low Coupling, High Cohesion）

• **"Low coupling, high cohesion"** 是软件行业最重要的概念之一，它是组织代码的指导原则，使得程序的不同部分易于理解、测试和独立修改

• 为了实现这个目标，软件通常被组织成**layers（层）**，每一层都有明确的角色，比如管理用户界面、处理数据持久化，或者实现程序的核心逻辑。这些层帮助减少程序各部分之间的依赖，使系统更容易维护和演进

## 策略（Policies）的概念

• 计算机程序可以被视为一组**policies（策略）**——这些规则控制着输入如何转换为输出。也可以理解为关于数据在系统不同点应该如何呈现的规则集合。在计算机科学术语中，一个 policy 提供一组 invariants（不变式）、preconditions（前置条件）和 postconditions（后置条件）

• **策略的层次（Levels of Policies）**：
  - **High-level policies（高层策略）**：远离输入/输出，代表应用程序的核心逻辑
  - **Low-level policies（低层策略）**：靠近输入/输出，处理 UI 交互、文件访问或网络通信等

• 策略的层次指的是它距离输入和输出的距离。按层次分离策略有助于将程序的核心逻辑与它如何与外部世界交互的技术细节隔离开来

• **高层策略的例子**：
  - 当用户借出一本书时，其他用户不能在这本书上放置 hold（预约）
  - 当客户从他们的银行账户取款时，允许最多 $1000 的透支额度

• **低层策略**可能描述用户如何触发事件以及数据如何存储在数据库中

• 在分层架构中，目标是保持高层策略独立于低层策略。例如，在图书馆系统中，一个策略可能规定：如果另一个用户已经在这本书上放置了 hold，那么这本书就不能被续借。这是关于系统应该如何行为的高层决策，无论用户如何与程序交互或数据如何存储。用户是点击"Renew"按钮还是系统从数据库查找信息，这些都是独立的关注点。高层策略本身保持不变。这种分离提高了可测试性，减少了耦合，使系统更容易推理

## 10.1 事件驱动编程（Event-driven Programming）

• 现代程序经常响应用户操作——点击、按键和其他交互。这些被称为**events（事件）**，响应这些事件的程序被称为**event-driven（事件驱动）**

• 当事件发生时，会触发一个叫做**event listener（事件监听器）**的方法。这个方法接收一个包含用户交互细节的 event object（事件对象），比如哪个按钮被点击了或哪个键被按下了。监听器然后调用其他方法来处理事件，形成跨对象的方法调用链

• 这个调用链创建了一个**network of objects（对象网络）**，其中每个方法调用代表一个连接。在运行时，**call stack（调用栈）**追踪这些方法调用，而**heap（堆）**存储涉及的对象。栈底部的方法通常是事件监听器，栈的其余部分反映了由该事件触发的逻辑流程

• 为了支持新的用户交互，我们编写新的事件监听器并定义它们应该如何响应。这连接了用户输入和驱动我们应用程序的逻辑

• **思考问题**：事件监听器是低层策略还是高层策略？（答案是低层策略，因为它靠近输入/输出）

## 10.2 层和耦合（Layers and Coupling）

• 软件开发者花费了几十年的时间来完善如何组织代码。一个广泛采用的策略是将程序组织成**layers（层）**，每一层都有特定的角色——比如管理用户界面、处理数据存储，或实现核心逻辑

• **分层架构的好处**：
  - 一层中的变化不太可能影响其他层，降低了 bug 的风险，使系统更容易维护
  - 通过将相关代码分组在一起，有助于避免 Git 合并冲突
  - 最小化开发者在进行更改时需要接触的文件数量，降低了引入错误的机会
  - 一层内的代码倾向于遵循一致的模式。例如，UI 类通常包含与用户交互相关的事件监听器方法

### 模型（Model）和实体（Entities）

• **Model（模型）**是你选择如何在程序中表示数据的方式，比如创建一个 `Book` 类，这样你就可以使用 `Book` 对象来表示系统的当前状态。这类对象通常被称为**entities（实体）**

• 模型是一个重要的概念，因为实体代表如何思考被操作的数据。对于可测试性和可维护性来说，特别重要的是模型不应该对 UI 层或数据库层有任何依赖。这意味着实体不能提及你在那些层中定义的任何类

• **思考问题**：实体代表什么层次的策略？（答案是高层策略，因为它们代表核心业务逻辑）

### 架构模式（Architecture Patterns）

• 以下是几种**architecture patterns（架构模式）**，或者思考程序组织的方式。如果你开始关注软件设计博客，你会遇到这些。它们大致按流行的时间顺序排列：
  - **model view controller (MVC)**
  - **model view presenter (MVP)**
  - **model view viewmodel (MVVM)**
  - **ports and adapters architecture**
  - **onion architecture**
  - **hexagonal architecture**
  - **clean architecture**（本课程将重点关注的）

• 它们都旨在帮助保持低耦合和高内聚，它们都有在不引入耦合的情况下跨层的技术。它们在"model"的含义和事件处理方式上有细微的变化，但核心概念——它代表问题域数据——是共享的

### 所有架构模式中都出现的方法

• 你需要编写一个**event listener method（事件监听器方法）**来处理用户交互。这个方法必须在 UI 层中

• 事件监听器方法将调用 controller/presenter/viewmodel 层中的方法，该方法将调用操作问题域数据的方法。在某个地方，会有代码从数据库、文件或网络保存和读取数据

## 10.3 模型视图控制器（MVC）架构模式

• MVC 架构模式是第一个在软件行业被广泛采用的模式

• **MVC 的典型流程**：
  - 用户与 View 交互，创建一个事件
  - Java 系统调用 View 对象中的监听器方法
  - View 立即调用 Controller 中的方法来处理事件
  - Controller 操作 Model
  - Model 从数据库获取任何必要的数据
  - Model 调用 View 对象中的方法，让它知道有更新
  - Controller 决定显示哪个屏幕
  - View 调用 Model 的 getter 方法并更新 UI

• MVC 的问题：MVC 架构模式存在**circular dependencies（循环依赖）**和 View 与 Model 之间的**tight coupling（紧耦合）**，这使得它难以测试和维护

## 10.4 模型视图展示器（MVP）架构模式

• MVP 架构模式是为了解决 MVC 的问题而开发的

• **MVP 与 MVC 的区别**：Presenter 在很大程度上扮演与 MVC 中 Controller 相同的角色，但 View 和 Model 不相互依赖

• **MVP 的典型流程**：
  - 用户与 View 交互，创建一个事件
  - Java 系统调用 View 对象中的监听器方法
  - View 立即调用 Presenter 中的方法来处理事件
  - Presenter 操作 Model
  - Model 从数据库获取任何必要的数据
  - Model 调用 Presenter 对象中的方法，让它知道有更新
  - Presenter 调用 View 中的方法来更新用户界面

## 10.5 更细粒度的分层架构

• 其他架构——ports and adapters、onion、hexagonal 和 clean——都是同一主题的变体。它们都有一个代表问题域数据和逻辑的**core layer（核心层）**，它们都有围绕该核心层的层来处理用户交互、数据库、文件和网络

• **Domain Layer（领域层）**：核心层通常被称为领域层，它包含实体和**business logic（业务逻辑）**。业务逻辑是实现问题域规则的代码，比如计算学生的 GPA 或确定用户是否有权限访问资源

### Clean Architecture（清洁架构）

• **Clean Architecture 由四层组成**：

  1. **Entities（实体层）**：代表问题域数据和逻辑的核心层（最高层策略）
  2. **Use Cases（用例层）**：包含应用特定业务规则的层（中等层策略）
  3. **Interface Adapters（接口适配器层）**：包含将数据从对用例和实体最方便的格式转换为对外部层（如用户界面）最方便的格式的代码的层（较低层策略）
  4. **Frameworks and Drivers（框架和驱动层）**：包含与用户和任何数据库进行外部交互的代码的层（最低层策略）

• **Clean Architecture 中的组件映射**：
  - Model 在 Entities 层中
  - Controller/Presenter/ViewModel 代码在 Interface Adapter 层中
  - View 和 database 都在 Frameworks and Drivers 层中
  - Use Case 层包含特定于单个用户交互的对象。每个都有一个 Controller 调用的方法，以尽可能多地处理用户交互

• **术语说明**：在 Clean Architecture 书中，"Enterprise Business Rules"（企业业务规则）和"Application Business Rules"（应用业务规则）的术语用于我们上面更非正式地称为"Entities"和"Use Cases"层的内容

• 我们将在下一章更详细地探索 Clean Architecture，因为它将是本课程重点关注的架构

## 思考问题

• 在你的代码中，"policy"可能是什么样子？它是一个方法、一个类、一个由条件强制执行的规则，还是其他什么？

• 回想一下，计算机架构也有分层结构，正如我们之前看到的，应用程序构建在操作系统之上，操作系统构建在硬件之上。你会发现层的概念出现在许多系统设计上下文中。以这种方式组织系统有什么特点使其成为如此常见的设计？




