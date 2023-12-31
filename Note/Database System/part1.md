# 第一章

### 文件处理系统

传统的操作系统所支持的，永久记录被存储在多个不同的文件中，通过编写不同的应用程序来将记录从有关文件中取出或加入到适当的文件中

**弊端**：

1. 数据的冗余和不一致
    - 不同的文件可能有不同的结构，不同的程序可能采用不同的程序设计语言
    - 相同的信息可能在几个文件重复存储，除了导致存储和访问的开销增大外，还可能导致数据不一致性

2. 数据访问困难
    - 传统的文件处理环境不支持以一种方便而高效的方式去获取所需数据

3. 数据孤立
    - 数据分散在不同的文件中，这些文件可能具有不同的格式

4. 完整性问题
    - 数据库中所存储数据的值可能必须满足某些特定的一致性约束，但当新的约束加入时，很难通过修改程序来体现这些新的约束，尤其是当约束涉及不同文件中多个数据项时

5. 原子性问题
    - 在传统的文件处理系统中，保持原子性（要么全部发生，要么根本不发生）是很难做到的

6. 并发访问异常
    - 由于数据可能被多个不同的应用程序访问，这些程序相互之间事先又没有协调，管理就很难进行

7. 安全性问题
    - 并非数据库系统的所有用户都可以访问所有数据，但是由于应用程序总是即席地加入到文件处理系统中来，这样的安全性约束很难实现

### 数据抽象

- **物理层**：最低层次的抽象，描述数据实际上时怎样存储的

- **逻辑层**：比物理层层次稍高的抽象，描述数据库中存储什么数据及这些数据间存在什么关系。虽然逻辑层的简单结构的实现可能涉及复杂的物理层结构，但逻辑层的用户不必知道这样的复杂性，这称作**物理数据独立性**

- **视图层**：最高层次的抽象，只描述整个数据库的某个部分，系统可以为同一数据库提供多个视图

### 实例和模式

特定时刻存储在数据库中的信息的集合称作数据库的一个**实例**，而数据库的总体设计称作数据库**模式**

**数据模式**：根据不同的抽象层次，数据库系统可以分为几种不同的模式

- 物理模式：在物理层描述数据库的设计
- 逻辑模式：在逻辑层描述数据库的设计
- 子模式：数据库在视图层也可以有几种模式，有时称为子模式，描述了数据库的不同视图

因为程序员使用逻辑模式来构造数据库应用程序，所以逻辑模式是目前最重要的一种模式  
物理模式隐藏在逻辑模式下，并且通常可以在应用程序丝毫不受影响的情况下被轻易更改  
如果应用程序不依赖于物理模式，它们就被称为是具有**物理数据独立性**

### 数据模型

数据库结构的基础是**数据模型**，数据模型是一种描述数据、数据联系、数据语义以及一致性约束的概念工具的集合，数据模型可被划分为四类：

1. 关系模型：关系模型用表的集合来表示数据和数据间的联系，每个表有多个列，每列有唯一的列名

2. 实体-联系模型：基于“现实世界由一组称作实体的基本对象以及这些对象间的联系构成”

3. 基于对象的数据模型：可以看成是E-R模型增加了封装、函数和对象标识等概念后的扩展

4. 半结构化数据模型：允许那些相同类型的数据项含有不同的属性集的数据定义。这和“数据模型中所有某种特定类型的数据必须有相同的属性集”形成对比

### 数据库语言

数据库提供**数据定义语言**来定义数据库模式，**数据操纵语言**来表达数据库的查询和更新，它们并不是两种分离的语言，相反，它们简单的构成了单一的数据库语言（如SQL语言）的不同部分

**数据操纵语言（DML）**：使用户可以访问或操纵那些按照某种适当的数据模型组织起来的数据

- 过程化DML：要求用户指定需要什么数据以及如何获得这些数据

- 声明式DML（非过程化DML）：只要求用户指定需要什么数据，而不指明如何获得

- **查询**：是要求对信息进行检索的语句，DML中涉及信息检索的部分称作**查询语言**

**数据定义语言（DDL）**：说明数据库模式和数据的其他特性的语言

### 数据存储和查询

数据库系统由几个子系统构成：

**存储管理器**：在数据库系统中负责在数据库中存储的低层数据与应用程序以及向系统提交的查询之间提供接口的部件，负责与文件管理器进行交互。存储管理器将各种DML语句翻译为底层文件系统命令。存储管理部件包括：

- 权限及完整性管理器
- 事务管理器
- 文件管理器
- 缓冲区管理器

**查询处理器**：查询处理器组件包括：

- DDL解释器：解释DDL语句并将这些定义记录在数据字典中
- DML编译器：将查询语句中的DML语句翻译为一个执行方案
- 查询执行引擎：执行由DML编译器产生的低级指令

### 数据库体系结构

- 两层体系结构：应用程序驻留在客户机上，通过查询语言表达式来调用服务器上的数据库系统功能

- 三层体系结构：客户机只作为一个前端且不包含任何直接的数据库调用，客户端通常通过一个表单界面与应用服务器进行通信，而应用服务器与数据库系统通信以访问数据，更适合大型应用和互联网上的应用