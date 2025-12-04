# 考试知识点总结 - M0到M3
# Exam Study Guide Summary - M0 to M3

## M0: Java and Git

### Which git commands did we discuss during lecture or use in a lab assignment?
### 我们在课程或实验作业中讨论或使用了哪些git命令？

**Answer / 答案：**

我们在课程中讨论和使用的Git命令包括：`git status`用来查看哪些文件被修改了（shows which files have been modified），`git add <files>`用来把文件添加到暂存区（stages files for commit），`git commit -m "<message>"`用来提交更改并附上描述信息（commits changes with a message），`git push`用来把本地更改推送到远程仓库（pushes local changes to remote repository），`git pull`用来从远程仓库拉取最新更改（pulls latest changes from remote repository），`git checkout -b <branch-name>`用来创建并切换到新分支（creates and switches to a new branch），`git merge <branch-name>`用来合并分支（merges a branch）。这些命令构成了基本的Git工作流程，让你能够跟踪代码变更、与团队协作，以及管理不同的功能分支（These commands form the basic Git workflow, allowing you to track code changes, collaborate with teams, and manage different feature branches）。

---

### What are the parts of a Java class? (class declaration, fields, constructor, etc.)
### Java类由哪些部分组成？（类声明、字段、构造函数等）

**Answer / 答案：**

一个Java类由以下几个主要部分组成（A Java class consists of the following main parts）：

1. **类声明（Class Declaration）**：包括访问修饰符如`public`或`private`，以及类名（includes access modifiers like `public` or `private`, and the class name）
2. **字段（Fields）**：也称为实例变量或属性，用来存储对象的状态（also called instance variables or attributes, used to store object state）
3. **构造函数（Constructor）**：用来初始化对象，名字和类名相同，没有返回类型（used to initialize objects, has the same name as the class, no return type）
4. **方法（Methods）**：用来定义类的行为（used to define class behavior）
5. **静态成员（Static Members）**：用`static`关键字标记，属于类本身而不是类的实例（marked with `static` keyword, belong to the class itself rather than instances）

---

### What are the Java naming conventions?
### Java的命名约定是什么？

**Answer / 答案：**

Java的命名约定遵循驼峰命名法（Java naming conventions follow camelCase）：

- **类名（Class Names）**：使用大驼峰（PascalCase），每个单词首字母大写，例如`StudentRecord`（use PascalCase, first letter of each word capitalized, e.g., `StudentRecord`）
- **方法名和变量名（Method and Variable Names）**：使用小驼峰（camelCase），第一个单词小写，后续单词首字母大写，例如`getStudentName`（use camelCase, first word lowercase, subsequent words capitalized, e.g., `getStudentName`）
- **常量（Constants）**：通常全大写，单词之间用下划线分隔，例如`MAX_SIZE`（usually all uppercase with underscores, e.g., `MAX_SIZE`）
- **包名（Package Names）**：通常全小写（usually all lowercase）

---

### How do you declare a class, a method, a variable? (including accessibility modifiers, static, etc.)
### 如何声明类、方法、变量？（包括访问修饰符、static等）

**Answer / 答案：**

**声明类（Declaring a Class）**：
```java
[access modifier] [static] [final] class ClassName {
    // class body
}
```
访问修饰符可以是`public`、`private`、`protected`或不写（包级访问）（Access modifiers can be `public`, `private`, `protected`, or none for package-level access）。

**声明方法（Declaring a Method）**：
```java
[access modifier] [static] [final] [return type] methodName([parameters]) {
    // method body
}
```

**声明变量（Declaring a Variable）**：
```java
[access modifier] [static] [final] [type] variableName [= value];
```

**访问修饰符（Access Modifiers）**：
- `public`：可以从任何地方访问（accessible from anywhere）
- `private`：只能在类内部访问（accessible only within the class）
- `protected`：可以在同一包内或子类中访问（accessible within the same package or subclasses）
- 无修饰符：包级访问（package-level access）

**其他关键字（Other Keywords）**：
- `static`：表示类成员而不是实例成员（indicates class member rather than instance member）
- `final`：用于变量时表示常量，用于方法时表示不能重写，用于类时表示不能被继承（for variables means constant, for methods means cannot be overridden, for classes means cannot be inherited）

---

### What does a constructor do?
### 构造函数的作用是什么？

**Answer / 答案：**

构造函数的作用是初始化新创建的对象，设置对象的初始状态（A constructor initializes newly created objects and sets their initial state）。当你用`new`关键字创建对象时，构造函数会被自动调用（When you create an object using the `new` keyword, the constructor is automatically called）。构造函数的名字必须和类名相同，没有返回类型（The constructor name must match the class name and has no return type）。

---

### When is the default constructor provided?
### 什么时候提供默认构造函数？

**Answer / 答案：**

如果你没有定义任何构造函数，Java会自动提供一个默认的无参构造函数，它会调用父类的无参构造函数（If you don't define any constructors, Java automatically provides a default no-argument constructor that calls the parent class's no-argument constructor）。但如果你定义了任何构造函数，Java就不会再提供默认构造函数了（However, if you define any constructor, Java will no longer provide the default constructor）。

---

### What does "super();" do?
### "super();"的作用是什么？

**Answer / 答案：**

`super()`用来调用父类的构造函数（`super()` is used to call the parent class constructor）。它必须是子类构造函数中的第一条语句（It must be the first statement in the subclass constructor）。如果不显式调用`super()`，Java会隐式调用父类的无参构造函数（If you don't explicitly call `super()`, Java will implicitly call the parent class's no-argument constructor）。如果父类没有无参构造函数，你必须显式调用`super(...)`并传入适当的参数（If the parent class has no no-argument constructor, you must explicitly call `super(...)` with appropriate arguments）。

---

## M1: More Java and Git

### What are keywords that we have seen in the Java quizzes and the lecture and lab activities? (including self, new, throw, throws, etc.)
### 我们在Java测验、课程和实验活动中看到了哪些关键字？（包括self、new、throw、throws等）

**Answer / 答案：**

重要的Java关键字包括（Important Java keywords include）：

- `this`：引用当前对象，在方法中可以用来区分实例变量和参数（refers to the current object, can distinguish instance variables from parameters in methods）
- `new`：创建新对象（creates a new object）
- `throw`：抛出异常（throws an exception）
- `throws`：用在方法声明中，表示该方法可能抛出异常（used in method declarations to indicate the method may throw exceptions）
- `static`：表示类成员（indicates class member）
- `abstract`：定义抽象类或抽象方法（defines abstract classes or methods）
- `extends`：表示继承关系（indicates inheritance）
- `implements`：表示实现接口（indicates interface implementation）
- `final`：表示不可修改（indicates immutability）
- `@Override`：注解，标记重写的方法（annotation marking overridden methods）

注意：Java中没有`self`关键字，Python中使用`self`，Java中使用`this`（Note: Java doesn't have a `self` keyword; Python uses `self`, Java uses `this`）。

---

### How do overloading, overriding, and shadowing work?
### 重载、重写和隐藏是如何工作的？

**Answer / 答案：**

**重载（Overloading）**：发生在同一个类中，多个方法有相同的名字但参数列表不同（occurs within the same class, multiple methods have the same name but different parameter lists）。编译器根据参数类型和数量来决定调用哪个方法（The compiler determines which method to call based on parameter types and count）。

**重写（Overriding）**：发生在继承关系中，子类重新定义父类的方法，方法签名必须相同（occurs in inheritance, subclass redefines parent class method, method signature must be the same）。通常配合`@Override`注解使用（Usually used with `@Override` annotation）。

**隐藏（Shadowing）**：通常指的是字段隐藏，当子类定义了和父类同名的字段时，子类的字段会隐藏父类的字段（usually refers to field hiding, when a subclass defines a field with the same name as the parent class, the subclass field hides the parent class field）。这不是推荐的做法（This is not recommended practice）。

---

### How does inheritance work in Java?
### Java中的继承是如何工作的？

**Answer / 答案：**

继承在Java中通过`extends`关键字实现（Inheritance in Java is implemented using the `extends` keyword）。子类会继承父类的所有`public`和`protected`成员（Subclasses inherit all `public` and `protected` members from the parent class）。Java只支持单继承，一个类只能有一个父类，但可以实现多个接口（Java supports single inheritance only; a class can have only one parent class but can implement multiple interfaces）。继承关系创建了is-a关系，比如`Dog extends Animal`意味着Dog is an Animal（Inheritance creates an is-a relationship, e.g., `Dog extends Animal` means Dog is an Animal）。子类可以访问父类的非`private`成员，可以重写父类的方法，也可以添加新的方法和字段（Subclasses can access non-`private` members of the parent class, can override parent methods, and can add new methods and fields）。

---

### What is the difference between an abstract class and an interface?
### 抽象类和接口的区别是什么？

**Answer / 答案：**

**抽象类（Abstract Class）**：
- 用`abstract`关键字定义（defined with `abstract` keyword）
- 可以包含抽象方法和具体方法（can contain abstract and concrete methods）
- 可以有实例变量（can have instance variables）
- 可以有构造函数（can have constructors）
- 不能被实例化（cannot be instantiated）
- 一个类只能继承一个抽象类（a class can extend only one abstract class）

**接口（Interface）**：
- 用`interface`关键字定义（defined with `interface` keyword）
- 在Java 8之前只能包含抽象方法，现在可以包含`default`方法和`static`方法（before Java 8 could only contain abstract methods, now can contain `default` and `static` methods）
- 接口中的变量默认是`public static final`的（variables in interfaces are `public static final` by default）
- 不能有实例变量（cannot have instance variables）
- 不能有构造函数（cannot have constructors）
- 一个类可以实现多个接口（a class can implement multiple interfaces）

---

### When would you want to use each?
### 什么时候使用抽象类，什么时候使用接口？

**Answer / 答案：**

**使用抽象类（Use Abstract Class）**：当你想要提供一些默认实现，或者想要定义一些共享的实例变量时（when you want to provide some default implementations or define shared instance variables）。

**使用接口（Use Interface）**：当你想要定义一组行为契约，或者想要实现多重继承的效果时（when you want to define a set of behavioral contracts or achieve multiple inheritance effects）。

---

### What are the java.swing classes we used during lecture and lab?
### 我们在课程和实验中使用了哪些java.swing类？

**Answer / 答案：**

我们使用的Java Swing类包括（Java Swing classes we used include）：

- `JFrame`：顶层窗口容器，用来创建应用程序的主窗口（top-level window container for creating the main application window）
- `JPanel`：面板容器，用来组织其他组件，可以嵌套使用（panel container for organizing other components, can be nested）
- `JButton`：按钮组件，用户可以点击它来触发操作（button component that users can click to trigger actions）
- `JLabel`：标签组件，用来显示文本或图标（label component for displaying text or icons）
- `JTextField`：文本输入框，用户可以输入单行文本（text input field for single-line text input）

---

### What do they correspond to visually when you look at the GUI?
### 它们在GUI中视觉上对应什么？

**Answer / 答案：**

- `JFrame`：整个窗口（the entire window）
- `JPanel`：窗口内的一个区域（an area within the window）
- `JButton`：按钮（a button）
- `JLabel`：文本标签（a text label）
- `JTextField`：输入框（an input field）

我们通常使用嵌套的`JPanel`配合`BoxLayout`来组织界面布局（We typically use nested `JPanel`s with `BoxLayout` to organize the interface layout）。

---

### How do you translate a UML diagram into code or code into a UML diagram using the symbols on this slide?
### 如何使用幻灯片上的符号将UML图转换为代码或将代码转换为UML图？

**Answer / 答案：**

**UML符号（UML Symbols）**：
- 类用矩形表示，分为三部分：类名、属性、方法（classes are represented by rectangles with three sections: class name, attributes, methods）
- 继承关系用带空心三角箭头的实线表示，箭头指向父类（inheritance is shown with a solid line with a hollow triangle arrow pointing to the parent class）
- 实现接口用带空心三角箭头的虚线表示，箭头指向接口（interface implementation is shown with a dashed line with a hollow triangle arrow pointing to the interface）
- 关联关系用实线箭头表示（associations are shown with solid arrows）
- 依赖关系用虚线箭头表示（dependencies are shown with dashed arrows）

**从UML到代码（UML to Code）**：识别类的结构、字段、方法，以及类之间的关系，然后用Java语法实现（identify class structure, fields, methods, and relationships between classes, then implement using Java syntax）。

**从代码到UML（Code to UML）**：提取类的信息，识别关系类型，然后用UML符号表示出来（extract class information, identify relationship types, then represent using UML symbols）。

---

### How do we use git branches?
### 我们如何使用git分支？

**Answer / 答案：**

我们使用以下命令来操作Git分支（We use the following commands to work with Git branches）：

- `git checkout -b <branch-name>`：创建并切换到新分支（creates and switches to a new branch）
- `git checkout <branch-name>`：切换到指定分支（switches to the specified branch）
- `git branch`：查看所有分支（lists all branches）
- `git merge <branch-name>`：合并指定分支到当前分支（merges the specified branch into the current branch）

分支让我们可以在不影响主分支的情况下开发新功能，完成后再合并回去（Branches allow us to develop new features without affecting the main branch, then merge back when complete）。

---

### What is a pull request, and what are the steps to creating one?
### 什么是pull request，创建pull request的步骤是什么？

**Answer / 答案：**

Pull Request是GitHub等平台上的一个功能，用来请求把某个分支的更改合并到主分支（A Pull Request is a feature on platforms like GitHub to request merging changes from a branch into the main branch）。

**创建Pull Request的步骤（Steps to create a Pull Request）**：
1. 在本地创建并切换到新分支（create and switch to a new branch locally）
2. 进行开发并提交更改（develop and commit changes）
3. 把分支推送到远程仓库（push the branch to the remote repository）
4. 在GitHub等平台上创建Pull Request（create a Pull Request on the platform like GitHub）
5. 填写描述信息（fill in description information）
6. 等待代码审查（wait for code review）
7. 审查通过后合并到主分支（merge into main branch after review approval）

---

## M2: SOLID and Design

### What do we mean by "high cohesion, low coupling"?
### "高内聚，低耦合"是什么意思？

**Answer / 答案：**

**高内聚（High Cohesion）**：一个模块内部的元素紧密相关，共同完成一个明确的目标（elements within a module are closely related and work together to achieve a clear goal）。

**低耦合（Low Coupling）**：模块之间的依赖关系尽可能少，一个模块的变化不会影响其他模块（minimal dependencies between modules, changes in one module don't affect others）。

高内聚低耦合让代码更容易理解、测试和维护（High cohesion and low coupling make code easier to understand, test, and maintain）。

---

### What does it mean for class A to depend on class B?
### 类A依赖类B意味着什么？

**Answer / 答案：**

当类A依赖类B时，意味着类A需要使用类B的功能（When class A depends on class B, it means class A needs to use class B's functionality）。这种依赖关系在代码中表现为类A中有类B的引用，或者类A的方法参数或返回类型是类B（This dependency is shown in code as class A having a reference to class B, or class A's method parameters or return types being class B）。依赖关系可以是直接的，比如类A直接创建类B的实例，也可以是间接的，比如类A通过接口依赖类B（Dependencies can be direct, such as class A directly creating an instance of class B, or indirect, such as class A depending on class B through an interface）。

---

### What are each of the SOLID principles and how can you summarize each one?
### SOLID原则有哪些，如何总结每个原则？

**Answer / 答案：**

**S - 单一职责原则（Single Responsibility Principle, SRP）**：一个类应该只有一个改变的理由（a class should have only one reason to change）。一个类应该只负责一个功能领域（a class should be responsible for only one functional area）。

**O - 开闭原则（Open/Closed Principle, OCP）**：类应该对扩展开放，对修改关闭（classes should be open for extension but closed for modification）。应该通过继承或组合来添加新功能，而不是修改现有代码（should add new functionality through inheritance or composition rather than modifying existing code）。

**L - 里氏替换原则（Liskov Substitution Principle, LSP）**：子类应该能够替换父类，在任何使用父类的地方都可以使用子类，而不会破坏程序的功能（subclasses should be substitutable for their parent classes, can be used anywhere the parent class is used without breaking program functionality）。

**I - 接口隔离原则（Interface Segregation Principle, ISP）**：不应该强迫客户端依赖它们不使用的接口，应该把大接口拆分成小接口（clients should not be forced to depend on interfaces they don't use, large interfaces should be split into smaller ones）。

**D - 依赖倒置原则（Dependency Inversion Principle, DIP）**：高层模块不应该依赖低层模块，两者都应该依赖抽象（high-level modules should not depend on low-level modules, both should depend on abstractions）。应该依赖接口而不是具体实现（should depend on interfaces rather than concrete implementations）。

---

### How do you identify code that violates each principle?
### 如何识别违反每个原则的代码？

**Answer / 答案：**

**违反SRP（Violating SRP）**：一个类做了太多不同的事情，比如一个类既处理用户界面又处理数据库操作（a class does too many different things, e.g., a class handles both user interface and database operations）。

**违反OCP（Violating OCP）**：添加新功能需要修改现有类，比如用if-else来判断不同类型（adding new features requires modifying existing classes, e.g., using if-else to check different types）。

**违反LSP（Violating LSP）**：子类改变了父类的行为，比如子类的方法抛出了父类没有的异常（subclass changes parent class behavior, e.g., subclass method throws exceptions the parent class doesn't）。

**违反ISP（Violating ISP）**：接口太大，包含了客户端不需要的方法（interface is too large, contains methods clients don't need）。

**违反DIP（Violating DIP）**：高层类直接依赖低层类，而不是依赖接口（high-level classes directly depend on low-level classes rather than interfaces）。

---

### Why is it useful to follow each of the SOLID principles?
### 为什么遵循每个SOLID原则是有用的？

**Answer / 答案：**

**SRP的好处（Benefits of SRP）**：让类更容易理解和维护，每个类职责单一（makes classes easier to understand and maintain, each class has a single responsibility）。

**OCP的好处（Benefits of OCP）**：让系统更容易扩展，添加新功能不需要修改现有代码，降低了引入bug的风险（makes systems easier to extend, adding new features doesn't require modifying existing code, reduces risk of introducing bugs）。

**LSP的好处（Benefits of LSP）**：保证了继承关系的正确性，让多态能够正常工作（ensures correctness of inheritance relationships, enables polymorphism to work properly）。

**ISP的好处（Benefits of ISP）**：减少了不必要的依赖，让系统更灵活（reduces unnecessary dependencies, makes systems more flexible）。

**DIP的好处（Benefits of DIP）**：让系统更容易测试和维护，可以轻松替换实现（makes systems easier to test and maintain, can easily replace implementations）。

---

### What is a user story and who is the target audience?
### 什么是用户故事，目标受众是谁？

**Answer / 答案：**

用户故事是从用户角度描述系统功能的简短描述（A user story is a brief description of system functionality from the user's perspective），通常格式是"作为...，我想要...，以便..."（usually in the format "As a..., I want..., so that..."）。用户故事的目标受众是开发团队、产品经理、测试人员等所有参与项目的人（The target audience includes development teams, product managers, testers, and all project participants），它帮助大家理解用户需求（it helps everyone understand user requirements）。用户故事应该是可测试的、可实现的、有价值的（User stories should be testable, implementable, and valuable）。

---

### How can we identify stakeholders in our program?
### 如何识别程序中的利益相关者？

**Answer / 答案：**

识别利益相关者需要思考谁会使用这个系统，谁会受到系统的影响，谁会对系统有需求（Identifying stakeholders requires thinking about who will use the system, who will be affected by the system, and who will have requirements for the system）。利益相关者可能包括最终用户、系统管理员、业务分析师、开发团队、管理层等（Stakeholders may include end users, system administrators, business analysts, development teams, management, etc.）。识别利益相关者有助于理解系统的真正需求（Identifying stakeholders helps understand the true requirements of the system）。

---

### What is an API and how do you use one in Java?
### 什么是API，如何在Java中使用API？

**Answer / 答案：**

API是应用程序编程接口，定义了不同软件组件之间如何交互（An API is an Application Programming Interface that defines how different software components interact）。在Java中，API通常指的是类或接口提供的方法集合，告诉你可以调用哪些方法，需要传递什么参数，会返回什么结果（In Java, an API usually refers to the set of methods provided by a class or interface, telling you which methods you can call, what parameters to pass, and what results will be returned）。使用API时，你需要查看文档了解可用的方法，创建相应的对象，然后调用方法（When using an API, you need to check documentation to understand available methods, create appropriate objects, then call methods）。Java标准库提供了大量API，比如`String`类、`ArrayList`类等（The Java standard library provides many APIs, such as the `String` class, `ArrayList` class, etc.）。

---

### What is JSON and how is it relevant to an API?
### 什么是JSON，它与API有什么关系？

**Answer / 答案：**

JSON是JavaScript对象表示法，是一种轻量级的数据交换格式，用文本表示结构化数据（JSON is JavaScript Object Notation, a lightweight data interchange format that represents structured data as text）。JSON在API中非常重要，因为很多Web API使用JSON格式来传输数据（JSON is very important in APIs because many Web APIs use JSON format to transmit data）。当你调用API时，服务器可能返回JSON格式的数据，你需要解析这些数据（When you call an API, the server may return data in JSON format, and you need to parse this data）。在Java中，可以使用库如Jackson或Gson来解析和生成JSON数据（In Java, you can use libraries like Jackson or Gson to parse and generate JSON data）。

---

## M3: Clean Architecture

### What is a use case and who is the target audience?
### 什么是用例，目标受众是谁？

**Answer / 答案：**

用例是从系统角度描述系统如何响应用户请求的详细描述（A use case is a detailed description from the system's perspective of how the system responds to user requests），它描述了系统执行的一系列步骤来完成某个功能（it describes a series of steps the system executes to complete a function）。用例的目标受众主要是开发人员和系统分析师（The target audience is primarily developers and systems analysts），它帮助理解系统的行为（it helps understand system behavior）。用例通常包括前置条件、主要流程、替代流程、后置条件等（Use cases typically include preconditions, main flow, alternative flows, postconditions, etc.）。

---

### How do you translate a user story to a set of 1 or more use cases?
### 如何将用户故事转换为一个或多个用例？

**Answer / 答案：**

从用户故事到用例的转换需要分析用户故事，识别系统需要执行的操作，然后为每个操作创建用例（Translating user stories to use cases requires analyzing the user story, identifying operations the system needs to perform, then creating a use case for each operation）。一个用户故事可能对应一个或多个用例，取决于用户故事的复杂程度（A user story may correspond to one or more use cases, depending on the complexity of the user story）。比如用户故事"作为用户，我想要登录系统，以便访问我的账户"可能对应一个"登录"用例（For example, the user story "As a user, I want to log in to the system so I can access my account" may correspond to one "Login" use case），而"作为用户，我想要管理我的订单"可能对应多个用例，如"查看订单"、"创建订单"、"取消订单"等（while "As a user, I want to manage my orders" may correspond to multiple use cases such as "View Orders", "Create Order", "Cancel Order", etc.）。

---

### What are the layers of Clean Architecture?
### Clean Architecture有哪些层？

**Answer / 答案：**

Clean Architecture分为四层（Clean Architecture consists of four layers）：

1. **实体层（Entities Layer）**：最内层，包含企业业务规则，这些规则是系统的核心，不依赖于外部因素（innermost layer, contains enterprise business rules, the core of the system, independent of external factors）
2. **用例层（Use Cases Layer）**：第二层，包含应用业务规则，这些规则是特定于应用程序的，描述系统如何响应用户的交互（second layer, contains application business rules, specific to the application, describes how the system responds to user interactions）
3. **接口适配器层（Interface Adapters Layer）**：第三层，包含将数据从一种格式转换为另一种格式的代码，比如Controller、Presenter、ViewModel等（third layer, contains code that converts data from one format to another, such as Controller, Presenter, ViewModel, etc.）
4. **框架和驱动层（Frameworks and Drivers Layer）**：最外层，包含与外部世界交互的代码，比如用户界面、数据库、Web框架等（outermost layer, contains code that interacts with the external world, such as user interfaces, databases, Web frameworks, etc.）

---

### Which layer contains the Enterprise Business Rules and what are they?
### 哪一层包含企业业务规则，它们是什么？

**Answer / 答案：**

企业业务规则在实体层（Enterprise Business Rules are in the Entities layer）。这些规则是业务领域的核心规则，不依赖于任何特定的应用程序或技术（These rules are core business domain rules, independent of any specific application or technology）。比如在银行系统中，"账户余额不能为负"就是一个企业业务规则（For example, in a banking system, "account balance cannot be negative" is an enterprise business rule）。

---

### Which layer contains the Application Business Rules and what are they?
### 哪一层包含应用业务规则，它们是什么？

**Answer / 答案：**

应用业务规则在用例层（Application Business Rules are in the Use Cases layer）。这些规则是特定于应用程序的，描述系统如何响应用户的交互（These rules are application-specific and describe how the system responds to user interactions）。比如"用户登录时需要验证密码"就是一个应用业务规则（For example, "user login requires password verification" is an application business rule）。

---

### Which layer adapts elements outside of the program so that they can interact with the main part of the program?
### 哪一层适配程序外部的元素，使它们能够与程序的主要部分交互？

**Answer / 答案：**

接口适配器层负责适配外部元素，让它们能够与系统核心交互（The Interface Adapters layer is responsible for adapting external elements so they can interact with the system core）。这一层包含Controller，负责接收用户输入并转换为系统可以理解的格式（This layer contains Controller, responsible for receiving user input and converting it to a format the system can understand）；Presenter，负责将系统输出转换为用户界面可以显示的格式（Presenter, responsible for converting system output to a format the user interface can display）；ViewModel，负责保存视图需要显示的数据（ViewModel, responsible for storing data the view needs to display）；还有Data Access接口的实现，负责与数据库交互（and implementations of Data Access interfaces, responsible for interacting with databases）。

---

### What are the roles of and interfaces implemented by each kind of class in Clean Architecture?
### Clean Architecture中每种类型的类的角色和实现的接口是什么？

**Answer / 答案：**

- **Entity（实体）**：业务实体，包含企业业务规则，位于实体层（business entity, contains enterprise business rules, located in Entities layer）
- **Use Case Interactor（用例交互器）**：执行应用业务规则，位于用例层，实现Input Boundary接口，通过接口与外部层交互（executes application business rules, located in Use Cases layer, implements Input Boundary interface, interacts with external layers through interfaces）
- **Controller（控制器）**：接收用户输入，调用Use Case，位于接口适配器层，实现Input Boundary接口的调用（receives user input, calls Use Case, located in Interface Adapters layer, calls Input Boundary interface）
- **Presenter（展示器）**：接收Use Case的输出，更新ViewModel，位于接口适配器层，实现Output Boundary接口（receives Use Case output, updates ViewModel, located in Interface Adapters layer, implements Output Boundary interface）
- **View（视图）**：显示信息给用户，位于框架和驱动层（displays information to users, located in Frameworks and Drivers layer）
- **Data Access（数据访问）**：实现数据持久化，位于框架和驱动层，实现Data Access Interface（implements data persistence, located in Frameworks and Drivers layer, implements Data Access Interface）

---

### Which layer contains each class?
### 每个类位于哪一层？

**Answer / 答案：**

- **Entity**：实体层（Entities layer）
- **Use Case Interactor**：用例层（Use Cases layer）
- **Controller、Presenter、ViewModel**：接口适配器层（Interface Adapters layer）
- **View、Data Access**：框架和驱动层（Frameworks and Drivers layer）

---

### How can you identify the role of a class by looking at the code?
### 如何通过查看代码识别类的角色？

**Answer / 答案：**

通过查看代码可以识别类的角色（You can identify a class's role by examining the code）：

- **Entity类**：通常包含业务逻辑方法，不依赖外部框架（typically contains business logic methods, doesn't depend on external frameworks）
- **Use Case Interactor**：通常实现某个用例，依赖Entity和Data Access接口（typically implements a use case, depends on Entity and Data Access interfaces）
- **Controller**：通常有处理用户输入的方法，依赖Use Case接口（typically has methods to handle user input, depends on Use Case interfaces）
- **Presenter**：通常有更新ViewModel的方法，依赖Use Case接口和ViewModel（typically has methods to update ViewModel, depends on Use Case interfaces and ViewModel）
- **View**：通常有显示UI的方法，依赖ViewModel（typically has methods to display UI, depends on ViewModel）
- **Data Access**：通常有读写数据的方法，实现Data Access接口（typically has methods to read/write data, implements Data Access interface）

---

### What is the Clean Architecture Dependency Rule?
### Clean Architecture的依赖规则是什么？

**Answer / 答案：**

Clean Architecture的依赖规则是依赖必须指向内层（The Clean Architecture Dependency Rule states that dependencies must point inward），也就是说，外层可以依赖内层，但内层不能依赖外层（meaning outer layers can depend on inner layers, but inner layers cannot depend on outer layers）。信息可以从内层流向外层，但依赖方向必须向内（Information can flow from inner layers to outer layers, but dependency direction must be inward）。这个规则通过依赖倒置原则实现，内层定义接口，外层实现接口，这样即使信息向外流动，依赖方向依然向内（This rule is implemented through the Dependency Inversion Principle: inner layers define interfaces, outer layers implement interfaces, so even though information flows outward, dependency direction remains inward）。

---

### How is it related to the "D" in SOLID?
### 它与SOLID中的"D"有什么关系？

**Answer / 答案：**

依赖规则与SOLID中的依赖倒置原则DIP密切相关（The Dependency Rule is closely related to the Dependency Inversion Principle (DIP) in SOLID）。DIP说高层模块不应该依赖低层模块，两者都应该依赖抽象（DIP states that high-level modules should not depend on low-level modules, both should depend on abstractions）。在Clean Architecture中，内层定义接口，外层实现接口，这正是DIP的体现（In Clean Architecture, inner layers define interfaces, outer layers implement interfaces, which is exactly the embodiment of DIP）。通过这种方式，内层不依赖外层的具体实现，只依赖接口，实现了依赖倒置（In this way, inner layers don't depend on outer layer implementations, only on interfaces, achieving dependency inversion）。

---

### Which of the SOLID principles are necessarily followed by any program that adheres to Clean Architecture?
### 遵循Clean Architecture的程序必然遵循哪些SOLID原则？

**Answer / 答案：**

遵循Clean Architecture的程序必然遵循SOLID的某些原则（Programs adhering to Clean Architecture necessarily follow certain SOLID principles）：

- **依赖倒置原则DIP**：必须遵循，因为依赖规则就是DIP的体现（must follow, because the Dependency Rule is the embodiment of DIP）
- **单一职责原则SRP**：必须遵循，因为每层、每个类都有明确的职责（must follow, because each layer and class has clear responsibilities）
- **开闭原则OCP**：必须遵循，因为可以通过实现接口来扩展功能而不修改现有代码（must follow, because functionality can be extended by implementing interfaces without modifying existing code）
- **里氏替换原则LSP**：必须遵循，因为所有实现必须遵守接口契约（must follow, because all implementations must adhere to interface contracts）
- **接口隔离原则ISP**：也应该遵循，接口应该小而专注（should also follow, interfaces should be small and focused）

---

### How do you test a Use Case Interactor?
### 如何测试Use Case Interactor？

**Answer / 答案：**

测试Use Case Interactor时，需要模拟它的依赖（When testing a Use Case Interactor, you need to mock its dependencies）。通常需要模拟Data Access接口，因为Use Case Interactor通过这个接口访问数据（Typically need to mock the Data Access interface, because the Use Case Interactor accesses data through this interface）。还需要模拟Output Boundary，因为Use Case Interactor通过这个接口输出结果（Also need to mock the Output Boundary, because the Use Case Interactor outputs results through this interface）。在单元测试中，我们创建这些接口的模拟实现，设置期望的行为，然后测试Use Case Interactor的逻辑是否正确（In unit tests, we create mock implementations of these interfaces, set expected behaviors, then test whether the Use Case Interactor's logic is correct）。

---

### Which classes are "mocked" by a unit test in order to test a Use Case Interactor?
### 为了测试Use Case Interactor，单元测试需要模拟哪些类？

**Answer / 答案：**

为了测试Use Case Interactor，单元测试通常需要模拟以下类（To test a Use Case Interactor, unit tests typically need to mock the following classes）：

- **Data Access接口的实现**：因为Use Case Interactor通过这个接口访问数据（implementation of Data Access interface, because the Use Case Interactor accesses data through this interface）
- **Output Boundary接口的实现（通常是Presenter）**：因为Use Case Interactor通过这个接口输出结果（implementation of Output Boundary interface (usually Presenter), because the Use Case Interactor outputs results through this interface）

通过模拟这些依赖，我们可以独立测试Use Case Interactor的业务逻辑，而不需要真实的数据库或UI组件（By mocking these dependencies, we can independently test the Use Case Interactor's business logic without needing real databases or UI components）。

---

### How can we determine which use cases are required in a program based on its user stories?
### 如何根据用户故事确定程序中需要的用例？

**Answer / 答案：**

根据用户故事确定需要的用例，需要分析每个用户故事，识别系统需要执行的操作（To determine required use cases from user stories, analyze each user story and identify operations the system needs to perform）。每个操作对应一个用例（Each operation corresponds to a use case）。比如用户故事"作为用户，我想要查看我的订单列表"对应"查看订单列表"用例（For example, the user story "As a user, I want to view my order list" corresponds to the "View Order List" use case），用户故事"作为用户，我想要取消订单"对应"取消订单"用例（the user story "As a user, I want to cancel an order" corresponds to the "Cancel Order" use case）。有些复杂的用户故事可能对应多个用例，需要仔细分析（Some complex user stories may correspond to multiple use cases and require careful analysis）。

---

### What is the flow of information through the Clean Architecture — how does information get from the user at the keyboard/mouse into the program, get modified, get stored within and outside of the program, and cause the appropriate changes to the User Interface?
### Clean Architecture中信息的流动是什么——信息如何从用户的键盘/鼠标进入程序，被修改，在程序内外存储，并导致用户界面的相应变化？

**Answer / 答案：**

信息在Clean Architecture中的流动如下（The flow of information through Clean Architecture is as follows）：

1. **用户输入（User Input）**：用户通过键盘或鼠标与View交互（User interacts with View through keyboard/mouse）
2. **View → Controller**：View接收用户输入后调用Controller的方法（View receives user input and calls Controller's method）
3. **Controller → Use Case**：Controller将输入转换为Input Data，通过Input Boundary调用Use Case Interactor（Controller converts input to Input Data, calls Use Case Interactor through Input Boundary）
4. **Use Case → Data Access**：Use Case Interactor执行业务逻辑，可能需要通过Data Access Interface读取或写入数据（Use Case Interactor executes business logic, may need to read/write data through Data Access Interface）
5. **Data Access → Database**：Data Access实现访问数据库或外部存储（Data Access implementation accesses database or external storage）
6. **Use Case → Entity**：Use Case Interactor操作Entity执行业务规则（Use Case Interactor operates on Entity to execute business rules）
7. **Use Case → Presenter**：Use Case Interactor完成后创建Output Data，通过Output Boundary传递给Presenter（Use Case Interactor creates Output Data after completion, passes it to Presenter through Output Boundary）
8. **Presenter → ViewModel**：Presenter将Output Data转换为ViewModel可以使用的格式，更新ViewModel（Presenter converts Output Data to format usable by ViewModel, updates ViewModel）
9. **ViewModel → View**：View监听到ViewModel的变化后更新用户界面（View detects ViewModel changes and updates the user interface）

整个流程中，依赖方向始终向内，信息可以向外流动，但代码依赖指向内层（Throughout this process, dependency direction always points inward; information can flow outward, but code dependencies point inward）。
