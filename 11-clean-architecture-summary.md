# Chapter 11: Clean Architecture - 知识点总结

## 核心规则：依赖必须向内（Dependency Rule）

• **Dependency Rule（依赖规则）**：系统中的所有依赖都要指向更内层的高阶策略，不能让核心实体依赖外围框架。所有外层实现（frameworks/drivers）都只通过接口依赖内层，从而保持内核纯净，方便替换细节。  
• **Dependency Inversion Principle（依赖反转原则）**：信息可以从内层流向外层，是因为内层定义接口、外层实现接口，实现方式被反转；这样即使流程向外跑，依赖方向依旧朝内。

## Clean Architecture Engine（CA 引擎）

• **典型场景 UML（Typical Scenario UML）**：通过 View、Controller、Use Case Interactor、Presenter、Data Access 等组件拼装成“CA engine”，所有指针都朝向内层接口，体现依赖反转。  
• **结构目标（Architecture Goal）**：让用例逻辑和实体规则成为系统核心，外层实现仅是可替换细节，满足高内聚、低耦合，让系统在测试或部署时能随时换掉框架或数据源。

## Clean Architecture 的层次（Layers in CA）

### Frameworks and Drivers（框架与驱动层）

• **View**：负责展示信息、响应用户操作，依赖 ViewModel 来读取要展示的数据，更新通过监听 ViewModel 变化完成。  
• **Data Access**：实现 Use Case 层定义的 Data Access Interface，读写外部数据库或文件，并创建临时实体供用例使用。

### Interface Adapters（接口适配器层）

• **Controller**：把原始用户输入转换为业务需要的格式（例如字符串转日期），封装成 Input Data，通过 Input Boundary 启动对应 Use Case。  
• **Presenter**：接收 Use Case 返回的 Output Data，把结果转换成 View 所需的字符串或数字，更新 ViewModel。  
• **View Model**：保存 View 显示所需的全部数据，View 通过它读取状态，Presenter 更新它。

### Use Cases（用例层）

• **Use Case Interactor**：执行应用特定业务流程，按需通过 Data Access Interface 读取或持久化数据，操纵实体，完成后产出 Output Data。  
• **Input Data / Output Data**：Input Data 由 Controller 构建供 Use Case 使用；Output Data 由 Use Case 生成供 Presenter 格式化。  
• **Input Boundary / Output Boundary / Data Access Interface**：这些接口都属于 Use Case 层，分别由 Controller、Presenter、Data Access 实现，完全描述系统核心行为，其他层只是细节实现。

### Entities（实体层）

• **Entity**：封装企业级业务规则（Enterprise Business Rules），例如 ACORN 系统中 Student 实体 enforce “同学期最多 7 门课”的约束。实体代表领域模型，在架构最内圈，保持与外部实现无关。

## CA Engine 的执行流程（Flow of Control）

• **Step 1 View -> Controller**：用户与 View 交互触发事件，View 把输入交给 Controller。  
• **Step 2 Controller -> Input Boundary**：Controller 组装 Input Data，通过 Input Boundary 调用 Use Case。  
• **Step 3 Use Case -> Data Access Interface**：Use Case Interactor 如需数据就调用 Data Access Interface 读取或写入持久化层。  
• **Step 4 Data Access -> Database**：具体的 Data Access 实现访问真实数据库或外部存储。  
• **Step 5 Use Case -> Entities**：Use Case 使用实体的方法执行业务规则，必要时反复与数据访问交互。  
• **Step 6 Use Case -> Output Boundary**：Use Case 完成后创建 Output Data，通过 Output Boundary 交给 Presenter。  
• **Step 7 Presenter -> View Model**：Presenter 更新 ViewModel，View 监听到变化后刷新界面；流程结束时 Controller 不会接收到返回值，暗示 Input Boundary 方法常设计为 void 或异步。

## Main Component（主组件/Driver）

• **装配职责（Assembly Responsibility）**：Main 负责实例化所有组件并按照依赖方向注入引用（View 拥有 Controller，Controller 拥有 Input Boundary，Use Case 持有 Data Access Interface 等）。  
• **可配置性（Configurability）**：不同场景可以换不同实现，例如测试环境用假的 Data Access 实现，生产环境用真实数据库，同一套内核可以通过不同 driver 装配来适配需求。

## SOLID 原则的影子（SOLID Echoes）

• **SRP/Single Responsibility**：各层只承担自己的职责，View 专注交互，Use Case 专注业务。  
• **OCP/Open-Closed**：通过接口和依赖反转，外层实现可替换不动核心。  
• **LSP/Liskov**：所有实现必须遵守内层定义的接口契约，确保替换无痛。  
• **ISP/Interface Segregation**：Input/Output/Data Access 接口都很小巧，调用者只依赖必要方法。  
• **DIP/Dependency Inversion**：核心原则落地，让高层策略不依赖具体实现，保证架构稳定。




