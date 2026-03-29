[Iterator](https://refactoring.guru/design-patterns/iterator)


## 一、行为模式

### 1. Observer

![[observer.png]]
- **场景**：**一对多** 依赖，状态变化时 **通知** 所有观察者
- **特征**：Subject维护Observer列表、提供attach/detach/notify、Observer定义update()
### 2. Strategy

![[strategy.png]]
- **场景**：定义一系列 **可互换** 的算法
- **特征**：Strategy接口定义algorithm()、Context持有Strategy引用、运行时可切换
### 3. Visitor

![[vsitor.png]]
- **场景**：对 **不同类型** 元素执行 **不同操作**，不修改元素类
- **特征**：Visitor定义visit(ConcreteElementX)、Element定义accept(Visitor)调用visitor.visit(this)
### 4. Chain of Responsibility

![[chainofresponsibility.png]]
- **场景**：多个处理者 **依次** 处理请求
- **特征**：Handler持有下一个Handler引用、处理或传递给successor
### 5. Iterator

![[iterator.png]]
- **场景**：**顺序访问** 集合元素而 **不暴露** 内部结构
- **特征**：Iterator定义hasNext()/next()、Aggregate定义createIterator()

### 6. Mediator

![[mediator.png]]
- **场景**：多个对象之间解耦，**通过中介通信**
- **特征**：Mediator持有所有Colleague引用、Colleague只认识Mediator
### 7. State

![[state.png]]
- **场景**：对象行为 **随内部状态** 改变
- **特征**：Context持有State引用、State定义handle()、状态切换时替换State对象
### 8. Memento

![[memento.png]]
- **场景**：**保存和恢复** 对象状态
- **特征**：Originator创建Memento保存状态、Caretaker保管Memento、Originator从Memento恢复

## 二、结构模式

### 1. Adapter

![[adapter 1.png]]
- **场景**：让接口 **不兼容** 的类能一起工作
- **特征**：Adapter持有Adaptee引用、实现Target接口、方法内调用adaptee的方法

### 2. Proxy

![[proxy.png]]
- **场景**：**控制** 对对象的 **访问**
- **特征**：Proxy和RealSubject实现同一接口、Proxy持有RealSubject引用、方法内加控制逻辑

### 3. Facade

![[facade.png]]
- **场景**：为复杂子系统提供 **简单统一入口**
- **特征**：Facade类封装多个子系统对象、对外提供简化的高层方法
### 4. Decorator

![[decorator.png]]
- **场景**：**动态** 给对象 **添加职责**
- **特征**：Decorator持有Component引用并实现Component接口、方法内调原对象再加增强
### 5. Composite

![[composite.png]]
- **场景**：**树形** 结构，统一处理单个对象和组合
- **特征**：Component定义通用接口、Leaf是叶子、Composite包含children列表

## 三、构建模式

### 1. Singleton

![[singleton 1.png]]

- **场景**：系统中某个类 **只能有一个实例** 的
- **特征**：
	1. **private 构造函数** → 禁止外部 new
	2. **private static 实例字段** → 唯一实例
	3. **public static getInstance() 方法** → 全局访问点，懒加载
### 2. Factory

![[factory.png]]

- **场景**：让 **子类决定** 创建哪种具体对象
- **特征**：抽象Creator定义factoryMethod()、ConcreteCreator重写返回具体Product

### 3. Builder

![[builder.png]]
- **场景**：**分步** 骤构造复杂对象
- **特征**：Builder接口定义buildPartX()、Director控制构建顺序、最后getResult()

### 4. Prototype

![[e338e9a8-d551-46dd-816d-fc740c12a05e.png]]
- **场景**：通过复制已有对象创建新对象
- **特征**：Prototype接口定义clone()、具体类实现深/浅拷贝