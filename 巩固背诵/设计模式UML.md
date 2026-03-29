
## 1. Singleton 单例模式

```
┌──────────────────────────────────────────┐
│            ConfigManager                 │
├──────────────────────────────────────────┤
│ - instance: ConfigManager  {static}      │
│ - config: Map<String,String>             │
├──────────────────────────────────────────┤
│ - ConfigManager()                        │
│ + getInstance(): ConfigManager  {static} │
│ + get(key: String): String               │
│ + set(key: String, val: String): void    │
└─────────────────────┬────────────────────┘
                      │ <<creates>>
                      └───────┐
                              │
                              ▲ (自引用: 返回唯一 instance)
```

**要点：** private构造, private static实例, public static getInstance()

---

## 2. Factory Method 工厂方法

```
┌─────────────────────────────┐            ┌──────────────────────────┐
│     Logistics (abstract)    │            │  <<interface>> Transport  │
├─────────────────────────────┤  creates   ├──────────────────────────┤
│                             │- - - - - ->│                          │
├─────────────────────────────┤            ├──────────────────────────┤
│ # createTransport():        │            │ + loadCargo(c): void     │
│     Transport  {abstract}   │            │ + deliver(): void        │
│ + planDelivery(c): void     │            └──────────────────────────┘
└─────────────────────────────┘                   △            △
        △              △                          ┆            ┆
        │              │                          ┆            ┆
        │              │                          ┆            ┆
┌───────┴──────┐ ┌─────┴────────┐   ┌────────────┴──┐ ┌───────┴───────┐
│ RoadLogistics│ │ SeaLogistics │   │    Truck       │ │     Ship      │
├──────────────┤ ├──────────────┤   ├───────────────-┤ ├───────────────┤
│              │ │              │   │                │ │               │
├──────────────┤ ├──────────────┤   ├────────────────┤ ├───────────────┤
│# createTrans │ │# createTrans │   │+ loadCargo()   │ │+ loadCargo()  │
│  port()      │ │  port()      │   │+ deliver()     │ │+ deliver()    │
└──────┬───────┘ └──────┬───────┘   └────────────────┘ └───────────────┘
       │                │                    ▲                 ▲
       │  <<creates>>   │   <<creates>>      ┆                ┆
       └ ─ ─ ─ ─ ─ ─ ─ ┼─ ─ ─ ─ ─ ─ ─ ─ ─ ┘                ┆
                        └ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─┘

图例:  ──▷ 继承(extends)    ─ ─▷ 实现(implements)    ─ ─> 依赖
         △ 实线空心三角        △ 虚线空心三角
```

---

## 3. Builder 建造者模式

```
┌────────────────────────────────┐         ┌─────────────────────────────────┐
│        Computer (Product)      │         │      Computer.Builder           │
├────────────────────────────────┤         ├─────────────────────────────────┤
│ - cpu: String     {final}      │         │ - cpu: String     {final}       │
│ - ram: int        {final}      │         │ - ram: int        {final}       │
│ - storage: String {final}      │         │ - storage: String = "256GB"     │
│ - gpu: String     {final}      │         │ - gpu: String = "集成显卡"       │
│ - hasWifi: boolean             │         │ - cooling: String = "风冷"       │
├────────────────────────────────┤         ├─────────────────────────────────┤
│ - Computer(builder: Builder)   │ <<creates>> │ + Builder(cpu, ram)          │
│ + toString(): String           │<─ ─ ─ ─ ┤ + storage(s): Builder          │
└────────────────────────────────┘         │ + gpu(g): Builder               │
                                           │ + cooling(c): Builder           │
                                           │ + build(): Computer             │
                                           └─────────────────────────────────┘

使用:  new Computer.Builder("i7", 32).storage("1TB").gpu("RTX4090").build();
```

**要点：** setter 返回 this → 链式调用, build() 返回产品

---

## 4. Prototype 原型模式

```
                 ┌──────────────────────────────────┐
                 │   <<interface>>                   │
                 │   GameUnitPrototype               │
                 ├──────────────────────────────────-┤
                 │                                   │
                 ├───────────────────────────────────┤
                 │ + clone(): GameUnitPrototype       │
                 └───────────────────────────────────┘
                          △                    ▲
                          ┆                    │ prototypes 0..*
                          ┆                    │
          ┌───────────────┴────┐    ┌──────────┴──────────────────┐
          │      Goblin        │    │    PrototypeRegistry        │
          ├────────────────────┤    ├─────────────────────────────┤
          │ - hp: int          │    │ - prototypes:               │
          │ - attack: int      │    │     Map<String, Prototype>  │
          │ - armor: String    │    ├─────────────────────────────┤
          │ - texture: byte[]  │    │ + register(key, p): void    │
          ├────────────────────┤    │ + getClone(key): Prototype  │
 clone()  │ + clone():         │    └─────────────────────────────┘
 ┌──────> │   GameUnitPrototype│
 │        └────────────────────┘
 │              │
 └──────────────┘  (自引用: clone 返回自身副本)
```

---

## 5. Adapter 适配器模式

```
┌────────────────────┐      ┌──────────────────────────┐
│   OrderService     │      │   <<interface>> Logger    │
│    (Client)        │      │      (Target)             │
├────────────────────┤      ├──────────────────────────-┤
│ - logger: Logger   │─────>│                           │
├────────────────────┤      ├───────────────────────────┤
│ + placeOrder()     │      │ + log(msg): void          │
└────────────────────┘      │ + error(msg): void        │
                            └───────────────────────────┘
                                        △
                                        ┆ implements
                                        ┆
                            ┌───────────┴───────────────┐
                            │   FancyLoggerAdapter      │
                            │       (Adapter)           │
                            ├───────────────────────────┤
                            │ - adaptee:                │
                            │    FancyThirdPartyLogger  │──────────┐
                            ├───────────────────────────┤          │
                            │ + log(msg): void          │          │
                            │ + error(msg): void        │          │
                            └───────────────────────────┘          │
                                                                   │
                                                                   ▼
                                               ┌───────────────────────────────┐
                                               │  FancyThirdPartyLogger        │
                                               │       (Adaptee)               │
                                               ├───────────────────────────────┤
                                               │                               │
                                               ├───────────────────────────────┤
                                               │ + writeInfo(text, level): void│
                                               │ + writeError(text, level):void│
                                               └───────────────────────────────┘
```

**要点：** Adapter 实现 Target 接口 + 持有 Adaptee 引用 → 方法中转换调用

---

## 6. Decorator 装饰器模式

```
                    ┌───────────────────────────┐
                    │   <<interface>> Beverage   │
                    │       (Component)          │
                    ├───────────────────────────-┤
                    │                            │
                    ├────────────────────────────┤
                    │ + getDescription(): String │
                    │ + getCost(): double        │
                    └────────────────────────────┘
                       △         △            ▲
                       │         ┆            │ beverage
                       │         ┆            │
          ┌────────────┘         ┆            │
          │                      ┆            │
┌─────────┴────────┐  ┌─────────┴──────────────────┐
│    Espresso      │  │  CondimentDecorator         │
│(ConcreteComp.)   │  │  (abstract Decorator)       │
├──────────────────┤  ├────────────────────────────-┤
│                  │  │ # beverage: Beverage ────────┘
├──────────────────┤  ├─────────────────────────────┤
│+ getDescription()│  │ + getDescription(): String  │
│+ getCost()       │  │ + getCost(): double         │
└──────────────────┘  └─────────────────────────────┘
                          △          △          △
                          │          │          │
              ┌───────────┘          │          └───────────┐
              │                      │                      │
   ┌──────────┴──────┐  ┌───────────┴─────┐  ┌─────────────┴───┐
   │  MilkDecorator  │  │  SugarDecorator │  │  CreamDecorator │
   ├─────────────────┤  ├─────────────────┤  ├─────────────────┤
   │                 │  │                 │  │                 │
   ├─────────────────┤  ├─────────────────┤  ├─────────────────┤
   │+getDescription()│  │+getDescription()│  │+getDescription()│
   │+getCost()       │  │+getCost()       │  │+getCost()       │
   └─────────────────┘  └─────────────────┘  └─────────────────┘

使用: Beverage b = new CreamDecorator(new MilkDecorator(new Espresso()));
```

**要点：** Decorator 实现相同接口 + 持有 Component 引用（自关联） → 套娃式包装

---

## 7. Decorator 考试原题版：Window 窗口系统

```
                    ┌──────────────────────────┐
                    │  <<interface>> Window     │
                    │     (Component)           │
                    ├──────────────────────────-┤
                    │                           │
                    ├───────────────────────────┤
                    │ + draw(): void            │
                    │ + getDescription(): String│
                    └───────────────────────────┘
                       △               △           ▲
                       │               ┆           │ window
                       │               ┆           │
            ┌──────────┘               ┆           │
            │                          ┆           │
 ┌──────────┴───────┐   ┌─────────────┴────────────────┐
 │   SimpleWindow   │   │    WindowDecorator (abstract) │
 ├──────────────────┤   ├──────────────────────────────-┤
 │                  │   │ # window: Window ─────────────┘
 ├──────────────────┤   ├───────────────────────────────┤
 │ + draw()         │   │ + draw(): void                │
 │ + getDescription │   │ + getDescription(): String    │
 └──────────────────┘   └───────────────────────────────┘
                            △         △          △
                            │         │          │
              ┌─────────────┘         │          └──────────────┐
              │                       │                         │
  ┌───────────┴────────┐ ┌───────────┴────────┐ ┌──────────────┴───────┐
  │TitleBarDecorator   │ │StatusBarDecorator  │ │ ScrollBarDecorator   │
  ├────────────────────┤ ├────────────────────┤ ├──────────────────────┤
  │                    │ │                    │ │                      │
  ├────────────────────┤ ├────────────────────┤ ├──────────────────────┤
  │+ draw()            │ │+ draw()            │ │+ draw()              │
  │+ getDescription()  │ │+ getDescription()  │ │+ getDescription()    │
  └────────────────────┘ └────────────────────┘ └──────────────────────┘
```

---

## 8. Facade 外观模式

```
                            ┌──────────────────────────────┐
      ┌───────────┐        │     HomeTheaterFacade         │
      │  Client   │        │         (Facade)              │
      ├───────────┤        ├──────────────────────────────-┤
      │           │───────>│ - curtain: CurtainController  │
      ├───────────┤        │ - light: LightController      │
      │+ main()   │        │ - projector: Projector        │
      └───────────┘        │ - amp: Amplifier              │
                           │ - player: BluRayPlayer        │
                           ├───────────────────────────────┤
                           │ + watchMovie(movie): void     │
                           │ + endMovie(): void            │
                           └───────────────────────────────┘
                              │     │      │      │     │
                              │     │      │      │     │
                              ▼     ▼      ▼      ▼     ▼
┌─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ┐
│                        Subsystem                                    │
│ ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌───────────┐ │
│ │ Curtain  │ │  Light   │ │Projector │ │Amplifier │ │BluRay     │ │
│ │Controller│ │Controller│ │          │ │          │ │Player     │ │
│ ├──────────┤ ├──────────┤ ├──────────┤ ├──────────┤ ├───────────┤ │
│ │+close()  │ │+dim()    │ │+on()     │ │+on()     │ │+play()    │ │
│ │+open()   │ │+on()     │ │+off()    │ │+off()    │ │+off()     │ │
│ └──────────┘ └──────────┘ │+setWide()│ │+setVol() │ └───────────┘ │
│                           └──────────┘ └──────────┘               │
└ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ┘
```

**要点：** Facade 封装子系统复杂交互，提供简化入口。Client 只依赖 Facade。

---

## 9. Proxy 代理模式

```
   ┌───────────┐         ┌───────────────────────────┐
   │  Client   │────────>│    <<interface>> Image     │
   ├───────────┤         │     (Subject)              │
   │           │         ├───────────────────────────-┤
   └───────────┘         │                            │
                         ├────────────────────────────┤
                         │ + display(): void          │
                         └────────────────────────────┘
                                △            △
                                ┆            ┆
                   implements   ┆            ┆  implements
                                ┆            ┆
               ┌────────────────┴──┐   ┌─────┴──────────────────┐
               │   ImageProxy      │   │    HugeImage           │
               │    (Proxy)        │   │   (Real Subject)       │
               ├───────────────────┤   ├────────────────────────┤
               │ - realImage:      │   │ - imageData: byte[]    │
               │     HugeImage ────┼──>│ - filename: String     │
               │ - filename: String│   ├────────────────────────┤
               ├───────────────────┤   │ + display(): void      │
               │ + display(): void │   │ - loadFromDisk(): void │
               └───────────────────┘   └────────────────────────┘

Proxy.display() {
    if (realImage == null)
        realImage = new HugeImage(filename);  // 懒加载!
    realImage.display();
}
```

**要点：** Proxy 与 RealSubject 实现同一接口; Proxy 控制访问（延迟/权限/远程）

---

## 10. Composite 组合模式（考试原题：Term 数学表达式）

```
                   ┌────────────────────────────┐
                   │    Term (abstract/interface)│ ◄─────────────┐
                   ├────────────────────────────┤               │
                   │                            │               │
                   ├────────────────────────────┤               │
                   │ + evaluate(): int          │               │
                   └────────────────────────────┘               │
                    △         △            △                    │
                    │         │            ┆                    │
          ┌─────── ┘         │            ┆                    │
          │                  │            ┆ implements          │
          │                  │            ┆                    │
┌─────────┴──────┐ ┌────────┴─────────┐  ┆                    │
│   Literal      │ │  Parenthesized   │  ┆                    │
│   (Leaf)       │ │                  │  ┆                    │
├────────────────┤ ├──────────────────┤  ┆                    │
│ - value: int   │ │ - term: Term  ───┼──┼────────────────────┤
├────────────────┤ ├──────────────────┤  ┆                    │
│ + evaluate()   │ │ + evaluate()     │  ┆                    │
└────────────────┘ └──────────────────┘  ┆                    │
                                         ┆                    │
                  ┌──────────────────────┴─────────┐          │
                  │     BinaryOp (abstract)         │          │
                  │     (Composite)                 │          │
                  ├────────────────────────────────-┤          │
                  │ - left: Term  ──────────────────┼──────────┤
                  │ - right: Term ──────────────────┼──────────┘
                  ├─────────────────────────────────┤
                  │ + evaluate(): int               │
                  └─────────────────────────────────┘
                     △        △          △          △
                     │        │          │          │
          ┌──────────┘        │          │          └──────────┐
          │                   │          │                     │
  ┌───────┴──────┐ ┌─────────┴──┐ ┌─────┴────────┐ ┌─────────┴───┐
  │  Addition    │ │Subtraction │ │Multiplication│ │  Division   │
  ├──────────────┤ ├────────────┤ ├──────────────┤ ├─────────────┤
  │              │ │            │ │              │ │             │
  ├──────────────┤ ├────────────┤ ├──────────────┤ ├─────────────┤
  │+ evaluate()  │ │+ evaluate()│ │+ evaluate()  │ │+ evaluate() │
  └──────────────┘ └────────────┘ └──────────────┘ └─────────────┘

Addition.evaluate()  = left.evaluate() + right.evaluate()
Literal.evaluate()   = value
Parenthesized.eval() = term.evaluate()
```

---

## 11. Strategy 策略模式（考试原题：画 UML）

```
┌──────────────────────────────┐         ┌──────────────────────────────┐
│        Context               │         │  <<interface>> Strategy      │
│     (CashRegister)           │         │   (PaymentStrategy)          │
├──────────────────────────────┤         ├──────────────────────────────┤
│ - strategy: Strategy  ───────┼────────>│                              │
├──────────────────────────────┤         ├──────────────────────────────┤
│ + setStrategy(s: Strategy)   │         │ + algorithm(): void          │
│ + execute(): void            │         │   (pay(amount): void)        │
└──────────────────────────────┘         └──────────────────────────────┘
                                                △          △
                                                ┆          ┆
                                     implements ┆          ┆ implements
                                                ┆          ┆
                                  ┌─────────────┴──┐  ┌────┴──────────────┐
                                  │ConcreteStrategyA│  │ConcreteStrategyB  │
                                  │ (CashPayment)  │  │(CreditCardPayment)│
                                  ├────────────────┤  ├───────────────────┤
                                  │                │  │                   │
                                  ├────────────────┤  ├───────────────────┤
                                  │+ algorithm()   │  │+ algorithm()      │
                                  └────────────────┘  └───────────────────┘

Context.execute() {
    strategy.algorithm();   // 委托给策略对象
}
```

**要点：** Context 持有 Strategy 接口引用，运行时可通过 setStrategy() 替换

---

## 12. Observer 观察者模式（考试原题：画 UML）

```
┌────────────────────────────────────┐         ┌──────────────────────────┐
│            Subject                 │         │  <<interface>> Observer   │
│         (NewsAgency)               │         ├──────────────────────────┤
├────────────────────────────────────┤  0..*   │                          │
│ - observers: List<Observer>  ──────┼────────>├──────────────────────────┤
├────────────────────────────────────┤         │ + update(data): void     │
│ + subscribe(o: Observer): void     │         └──────────────────────────┘
│ + unsubscribe(o: Observer): void   │                  △          △
│ + notifyObservers(): void          │                  ┆          ┆
└────────────────────────────────────┘       implements ┆          ┆
                                                        ┆          ┆
                                          ┌─────────────┴──┐ ┌─────┴────────────┐
                                          │ PhoneDisplay   │ │   WebDisplay     │
                                          │(ConcreteObs.)  │ │ (ConcreteObs.)   │
                                          ├────────────────┤ ├──────────────────┤
                                          │                │ │                  │
                                          ├────────────────┤ ├──────────────────┤
                                          │+ update(data)  │ │+ update(data)    │
                                          └────────────────┘ └──────────────────┘

Subject.notifyObservers() {
    for (Observer o : observers)
        o.update(data);
}
```

**要点：** Subject 持有 `List<Observer>` (0..*)，subscribe/unsubscribe 管理列表

---

## 13. Iterator 迭代器模式

```
┌──────────────────────────────┐              ┌──────────────────────────────┐
│  <<interface>> BookCollection│              │  <<interface>> BookIterator  │
│     (Aggregate)              │   <<creates>>│     (Iterator)               │
├──────────────────────────────┤              ├──────────────────────────────┤
│                              │─ ─ ─ ─ ─ ─ >│                              │
├──────────────────────────────┤              ├──────────────────────────────┤
│+ createIterator():           │              │ + hasNext(): boolean         │
│    BookIterator              │              │ + next(): String             │
└──────────────────────────────┘              └──────────────────────────────┘
          △              △                            △              △
          ┆              ┆                            ┆              ┆
          ┆              ┆                            ┆              ┆
┌─────────┴────────┐ ┌───┴──────────────┐  ┌─────────┴──────┐ ┌─────┴────────────┐
│ ShelfCollection  │ │ RecommendedColl. │  │ ShelfIterator  │ │RecommendedIter.  │
├──────────────────┤ ├──────────────────┤  ├────────────────┤ ├──────────────────┤
│- books: String[] │ │- books:LinkedList│  │- books: String[]│ │- iter: Iterator  │
├──────────────────┤ ├──────────────────┤  │- index: int    │ ├──────────────────┤
│+ createIterator()│ │+ createIterator()│  ├────────────────┤ │+ hasNext()       │
└──────────────────┘ └──────────────────┘  │+ hasNext()     │ │+ next()          │
       │                    │              │+ next()        │ └──────────────────┘
       │   <<creates>>      │              └────────────────┘
       └ ─ ─ ─ ─ ─ ─ ─ ─ ─>│ <<creates>>
                            └ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─>
```

**要点：** Collection 创建对应的 Iterator; 客户端只用 hasNext()/next() 统一遍历

---

## 14. State 状态模式

```
┌──────────────────────────────────┐        ┌──────────────────────────────────┐
│      VendingMachine              │        │  <<interface>> VendingState      │
│       (Context)                  │        ├──────────────────────────────────┤
├──────────────────────────────────┤        │                                  │
│ - currentState: VendingState ────┼───────>├──────────────────────────────────┤
│ - balance: int                   │        │+ insertCoin(machine, amt): void  │
├──────────────────────────────────┤        │+ selectProduct(machine): void    │
│ + setState(s: VendingState): void│        │+ dispense(machine): void         │
│ + insertCoin(amount): void       │        └──────────────────────────────────┘
│ + selectProduct(): void          │              △            △            △
│ + dispense(): void               │              ┆            ┆            ┆
└──────────────────────────────────┘              ┆            ┆            ┆
                                       ┌──────────┴──┐  ┌──────┴───────┐ ┌──┴──────────┐
Context.insertCoin(amt) {              │WaitingFor   │  │CoinInserted  │ │ Dispensing  │
  currentState.insertCoin(this, amt);  │CoinState    │  │State         │ │ State       │
}                                      ├─────────────┤  ├──────────────┤ ├─────────────┤
                                       │             │  │              │ │             │
                                       ├─────────────┤  ├──────────────┤ ├─────────────┤
                                       │+insertCoin()│  │+insertCoin() │ │+dispense()  │
                                       │+selectProd()│  │+selectProd() │ │+insertCoin()│
                                       │+dispense()  │  │+dispense()   │ │+selectProd()│
                                       └─────────────┘  └──────────────┘ └─────────────┘

ConcreteState 内部可以调用 machine.setState(newState) → 自动切换状态!
```

**State vs Strategy：** 结构相同，但 State 是对象自己切换行为，Strategy 是客户端主动选择

---

## 15. Visitor 访问者模式

```
┌──────────────────────────────┐              ┌──────────────────────────────────┐
│  <<interface>> Building      │    uses      │  <<interface>> BuildingVisitor   │
│     (Element)                │─ ─ ─ ─ ─ ─ >│       (Visitor)                  │
├──────────────────────────────┤              ├──────────────────────────────────┤
│                              │              │                                  │
├──────────────────────────────┤              ├──────────────────────────────────┤
│+ accept(v: BuildingVisitor)  │              │+ visitHouse(h: House): void      │
│   : void                     │              │+ visitShop(s: Shop): void        │
└──────────────────────────────┘              └──────────────────────────────────┘
          △            △                              △              △
          ┆            ┆                              ┆              ┆
          ┆            ┆                              ┆              ┆
┌─────────┴──────┐ ┌───┴──────────┐     ┌────────────┴────┐  ┌──────┴──────────────┐
│    House       │ │    Shop      │     │  TaxVisitor     │  │FireInspectionVisitor│
│   (Element)    │ │   (Element)  │     │(ConcreteVisitor)│  │ (ConcreteVisitor)   │
├────────────────┤ ├──────────────┤     ├─────────────────┤  ├─────────────────────┤
│- area: double  │ │-revenue:     │     │                 │  │                     │
│                │ │  double      │     ├─────────────────┤  ├─────────────────────┤
├────────────────┤ ├──────────────┤     │+visitHouse(h)   │  │+visitHouse(h)       │
│+ accept(v)     │ │+ accept(v)   │     │+visitShop(s)    │  │+visitShop(s)        │
└────────────────┘ └──────────────┘     └─────────────────┘  └─────────────────────┘

双重分派 (Double Dispatch):
  House.accept(v) { v.visitHouse(this); }   ← 第1次: 根据 Element 类型
  TaxVisitor.visitHouse(h) { ... }          ← 第2次: 根据 Visitor 类型
```

---

## 16. Memento 备忘录模式（考试原题：Speiseplan）

```
┌───────────────────────────────────────┐
│     Speiseplan  (Originator)          │
├───────────────────────────────────────┤
│ - montag: Gericht                     │
│ - dienstag: Gericht                   │
│ - mittwoch: Gericht                   │
│ - donnerstag: Gericht                 │     <<creates>>
│ - freitag: Gericht                    │─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ┐
├───────────────────────────────────────┤                          │
│ + save(): SpeiseplanSnapshot          │                          ▼
│ + restore(s: SpeiseplanSnapshot): void│     ┌────────────────────────────────┐
└───────────────────────────────────────┘     │ SpeiseplanSnapshot  (Memento)  │
                                              ├────────────────────────────────┤
                                              │ - montag: Gericht              │
                                              │ - dienstag: Gericht            │
┌───────────────────────────────────────┐     │ - mittwoch: Gericht            │
│   SpeiseplanManager  (Caretaker)      │     │ - donnerstag: Gericht          │
├───────────────────────────────────────┤     │ - freitag: Gericht             │
│ - snapshots:                          │     │ - savedAt: DateTime            │
│    Map<DateTime, Memento>  ───────────┼────>├────────────────────────────────┤
├───────────────────────────────────────┤     │ + getMontag(): Gericht         │
│ + save(plan: Speiseplan): void        │  *  │ + getDienstag(): Gericht       │
│ + restore(plan, date): void           │     │ + getSavedAt(): DateTime       │
└───────────────────────────────────────┘     └────────────────────────────────┘
                                                          △
                                                          ┆ implements
                                                          ┆
                                              ┌───────────┴──────────────────┐
                                              │  <<interface>> Memento       │
                                              ├──────────────────────────────┤
                                              │                              │
                                              ├──────────────────────────────┤
                                              │ + getDate(): DateTime        │
                                              └──────────────────────────────┘

角色对应:
  Originator = Speiseplan        → 创建 Snapshot + 从 Snapshot 恢复
  Memento    = SpeiseplanSnapshot → 不可变状态副本，只有 getter
  Caretaker  = SpeiseplanManager  → 管理 Snapshot 集合，不知道内部细节
```

---

## 17. Chain of Responsibility 责任链模式

```
                  ┌──────────────────────────────────────────┐
                  │     Approver  (abstract Handler)         │
                  ├──────────────────────────────────────────┤
                  │ # nextApprover: Approver  ───────────────┼──┐
                  ├──────────────────────────────────────────┤  │
                  │ + setNext(next: Approver): void          │  │
                  │ + approve(amount, desc): void  {abstract}│  │ 自引用
                  │ # passToNext(amount, desc): void         │  │ (next)
                  └──────────────────────────────────────────┘  │
                       △            △            △              │
                       │            │            │              │
                       │            │            │              │
          ┌────────────┘            │            └──────────┐   │
          │                         │                       │   │
 ┌────────┴──────────┐ ┌───────────┴──────────┐ ┌──────────┴───┴──────┐
 │   TeamLeader      │ │ DepartmentManager    │ │  GeneralManager     │
 ├───────────────────┤ ├──────────────────────┤ ├─────────────────────┤
 │                   │ │                      │ │                     │
 ├───────────────────┤ ├──────────────────────┤ ├─────────────────────┤
 │+ approve(amt,desc)│ │+ approve(amt, desc)  │ │+ approve(amt, desc) │
 └─────────┬─────────┘ └──────────┬───────────┘ └─────────────────────┘
           │    next               │    next
           └ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─>└ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─>

请求方向:  TeamLeader ──> DepartmentManager ──> GeneralManager
           <500 自己批       <5000 自己批          <50000 自己批
```

**要点：** 每个 Handler 有 nextHandler 引用; 不能处理就 passToNext()

---

## 18. Mediator 中介者模式

```
                  ┌──────────────────────────────────┐
                  │  <<interface>> ChatMediator       │
                  │         (Mediator)                │
                  ├──────────────────────────────────-┤
                  │                                   │
                  ├───────────────────────────────────┤
                  │ + sendMessage(msg, sender): void  │
                  │ + addUser(user: User): void       │
                  └───────────────────────────────────┘
                          △                  ▲
                          ┆                  │ mediator
                          ┆                  │
               ┌──────────┴──────────┐   ┌───┴──────────────────────┐
               │     ChatRoom        │   │       User               │
               │ (ConcreteMediator)  │   │    (Colleague)           │
               ├─────────────────────┤   ├──────────────────────────┤
               │ - users: List<User> │   │ - name: String           │
               │   │                 │   │ - mediator: ChatMediator │
               ├───┼─────────────────┤   ├──────────────────────────┤
               │ + sendMessage()     │   │ + sendMessage(msg): void │
               │ + addUser()         │   │ + receive(msg, from):void│
               └───┼─────────────────┘   └──────────────────────────┘
                   │                              ▲
                   │        users 0..*            │
                   └──────────────────────────────┘

User.sendMessage(msg) {
    mediator.sendMessage(msg, this);   // 通过中介者发送，不直接联系其他 User
}

ChatRoom.sendMessage(msg, sender) {
    for (User u : users)
        if (u != sender) u.receive(msg, sender);   // 中介者统一分发
}
```

**Mediator vs Observer：** Observer 一对多通知; Mediator 多对多协调

---

## 19. Interpreter 解释器模式

```
                    ┌────────────────────────────┐
                    │  <<interface>> Expression   │◄─────────────────┐
                    ├────────────────────────────-┤                  │
                    │                             │                  │
                    ├─────────────────────────────┤                  │
                    │ + interpret(): int           │                  │
                    └─────────────────────────────┘                  │
                       △          △           △                     │
                       ┆          ┆           ┆                     │
                       ┆          ┆           ┆                     │
          ┌────────────┘          ┆           └─────────────┐       │
          ┆                       ┆                         ┆       │
┌─────────┴──────────┐ ┌─────────┴──────────┐ ┌────────────┴─────┐ │
│  NumberExpression   │ │  AddExpression     │ │SubtractExpression│ │
│  (Terminal)         │ │  (Non-Terminal)    │ │  (Non-Terminal)  │ │
├─────────────────────┤ ├────────────────────┤ ├──────────────────┤ │
│ - number: int       │ │ - left: Expression─┼─┼──────────────────┼─┤
├─────────────────────┤ │ - right:Expression─┼─┼──────────────────┼─┘
│ + interpret(): int  │ ├────────────────────┤ ├──────────────────┤
│   → return number   │ │ + interpret(): int │ │ + interpret():int│
└─────────────────────┘ │  → left.interpret()│ │ → left - right   │
                        │    + right.interpr.│ └──────────────────┘
                        └────────────────────┘

语法树示例: (3 + 5) * 2
         MultiplyExpr
          /         \
    AddExpr        NumberExpr(2)
    /      \
NumberExpr(3) NumberExpr(5)

interpret() → (3+5)*2 = 16
```

---

## 图例总结 | Legende

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  ────▷     继承 (extends)         实线 + 空心三角
  ─ ─ ▷     实现 (implements)      虚线 + 空心三角
  ────>      关联 (association)     实线箭头
  ─ ─ >      依赖 (dependency)     虚线箭头  <<creates>>
  ◆────>     组合 (composition)    实心菱形
  ◇────>     聚合 (aggregation)    空心菱形

可见性:
  +  public
  -  private
  #  protected

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```