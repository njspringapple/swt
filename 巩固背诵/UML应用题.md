
## 一、行为模式 / Verhaltensmuster

---

### Observer 观察者模式

#### 题目1 / Aufgabe 1

**中文：** 设计一个天气预报系统。气象站（WeatherStation）检测到温度变化时，需要自动通知手机App、网站显示屏和电子邮件服务更新天气信息。请画出类图，标明Subject、Observer、attach()、detach()、notify()和update()方法。

**Deutsch:** Entwirf ein Wettervorhersagesystem. Wenn die Wetterstation (WeatherStation) eine Temperaturänderung erkennt, sollen automatisch die Handy-App, die Website-Anzeige und der E-Mail-Service benachrichtigt werden. Zeichne ein Klassendiagramm mit Subject, Observer, attach(), detach(), notify() und update().

#### 题目2 / Aufgabe 2

**中文：** 一个在线拍卖系统中，当商品价格更新时，所有关注该商品的买家都应该收到通知。请用Observer模式画出类图，标明拍卖商品（AuctionItem）和竞拍者（Bidder）之间的关系。

**Deutsch:** In einem Online-Auktionssystem sollen alle Käufer, die ein Produkt beobachten, benachrichtigt werden, wenn sich der Preis ändert. Zeichne ein Klassendiagramm mit dem Observer-Muster, das die Beziehung zwischen AuctionItem und Bidder zeigt.

---

### Strategy 策略模式

#### 题目1 / Aufgabe 1

**中文：** 一个电商系统支持多种支付方式：信用卡、PayPal和微信支付。用户可以在结账时选择不同的支付策略。请画出类图，展示PaymentStrategy接口和各种具体支付类，以及ShoppingCart如何持有策略引用。

**Deutsch:** Ein E-Commerce-System unterstützt verschiedene Zahlungsmethoden: Kreditkarte, PayPal und WeChat Pay. Der Benutzer kann beim Checkout eine Zahlungsstrategie wählen. Zeichne ein Klassendiagramm mit dem PaymentStrategy-Interface, den konkreten Zahlungsklassen und wie ShoppingCart die Strategie-Referenz hält.

#### 题目2 / Aufgabe 2

**中文：** 一个导航应用支持多种路线规划算法：最短路径、最快路径和避开收费站路径。请用Strategy模式画出类图，展示Navigator类如何在运行时切换不同的路线策略。

**Deutsch:** Eine Navigations-App unterstützt verschiedene Routenplanungsalgorithmen: kürzester Weg, schnellster Weg und Mautstraßen vermeiden. Zeichne ein Klassendiagramm mit dem Strategy-Muster, das zeigt, wie die Navigator-Klasse zur Laufzeit zwischen verschiedenen Routenstrategien wechseln kann.

---

### Visitor 访问者模式

#### 题目1 / Aufgabe 1

**中文：** 一个文档编辑器包含不同类型的元素：文本段落（Paragraph）、图片（Image）和表格（Table）。你需要实现导出功能，可以将文档导出为HTML或PDF格式。请用Visitor模式画出类图，展示ExportVisitor如何访问不同元素。

**Deutsch:** Ein Dokumenteditor enthält verschiedene Elementtypen: Textabsatz (Paragraph), Bild (Image) und Tabelle (Table). Du sollst eine Exportfunktion implementieren, die das Dokument als HTML oder PDF exportieren kann. Zeichne ein Klassendiagramm mit dem Visitor-Muster, das zeigt, wie ExportVisitor verschiedene Elemente besucht.

#### 题目2 / Aufgabe 2

**中文：** 一个动物园管理系统有不同的动物：狮子（Lion）、大象（Elephant）和猴子（Monkey）。兽医（Vet）和饲养员（Feeder）需要对每种动物执行不同的操作。请用Visitor模式画出类图，标明accept()和visit()方法。

**Deutsch:** Ein Zoo-Verwaltungssystem hat verschiedene Tiere: Löwe (Lion), Elefant (Elephant) und Affe (Monkey). Der Tierarzt (Vet) und der Pfleger (Feeder) müssen bei jedem Tier unterschiedliche Aktionen durchführen. Zeichne ein Klassendiagramm mit dem Visitor-Muster und markiere accept() und visit().

---

### Chain of Responsibility 责任链模式

#### 题目1 / Aufgabe 1

**中文：** 公司的请假审批系统：员工请假1天由组长审批，2-3天由经理审批，超过3天由总监审批。请用责任链模式画出类图，展示Handler如何持有下一个处理者的引用。

**Deutsch:** Das Urlaubsgenehmigungssystem einer Firma: 1 Tag Urlaub wird vom Teamleiter genehmigt, 2-3 Tage vom Manager, mehr als 3 Tage vom Direktor. Zeichne ein Klassendiagramm mit dem Chain-of-Responsibility-Muster, das zeigt, wie Handler die Referenz zum nächsten Bearbeiter hält.

#### 题目2 / Aufgabe 2

**中文：** 一个客服系统处理用户问题：首先由AI机器人尝试回答，如果无法解决则转给初级客服，最后转给高级客服。请画出责任链模式的类图，标明handleRequest()方法和successor引用。

**Deutsch:** Ein Kundenservice-System bearbeitet Benutzeranfragen: Zuerst versucht ein AI-Bot zu antworten, wenn das nicht klappt, wird an den Junior-Support weitergeleitet, dann an den Senior-Support. Zeichne ein Klassendiagramm mit handleRequest() und successor-Referenz.

---

### Iterator 迭代器模式

#### 题目1 / Aufgabe 1

**中文：** 一个音乐播放器的播放列表支持两种遍历方式：顺序播放和随机播放。请用Iterator模式画出类图，展示Playlist如何创建不同的SongIterator（SequentialIterator和ShuffleIterator）。

**Deutsch:** Eine Musik-Player-Playlist unterstützt zwei Durchlaufarten: sequentiell und zufällig. Zeichne ein Klassendiagramm mit dem Iterator-Muster, das zeigt, wie Playlist verschiedene SongIterator erstellt (SequentialIterator und ShuffleIterator).

#### 题目2 / Aufgabe 2

**中文：** 一个社交媒体应用需要遍历用户的好友列表。好友可以按添加时间顺序遍历，也可以按亲密度排序遍历。请画出Iterator模式的类图，标明hasNext()、next()和createIterator()方法。

**Deutsch:** Eine Social-Media-App muss die Freundesliste eines Benutzers durchlaufen. Freunde können nach Hinzufügedatum oder nach Vertrautheit sortiert werden. Zeichne ein Klassendiagramm mit hasNext(), next() und createIterator().

---

### Mediator 中介者模式

#### 题目1 / Aufgabe 1

**中文：** 一个聊天室系统中，多个用户（User）之间不直接通信，而是通过聊天室（ChatRoom）转发消息。请用Mediator模式画出类图，展示ChatRoom如何协调各个User之间的消息传递。

**Deutsch:** In einem Chatroom-System kommunizieren mehrere Benutzer (User) nicht direkt miteinander, sondern über den Chatroom. Zeichne ein Klassendiagramm mit dem Mediator-Muster, das zeigt, wie ChatRoom die Nachrichtenübermittlung zwischen Usern koordiniert.

#### 题目2 / Aufgabe 2

**中文：** 机场的航班调度系统：多架飞机（Aircraft）的起降不是直接协调，而是通过控制塔（ControlTower）统一调度。请用Mediator模式画出类图，标明Mediator和Colleague的关系。

**Deutsch:** Das Flugplanungssystem eines Flughafens: Mehrere Flugzeuge (Aircraft) koordinieren Start und Landung nicht direkt, sondern über den Kontrollturm (ControlTower). Zeichne ein Klassendiagramm mit Mediator und Colleague.

---

### State 状态模式

#### 题目1 / Aufgabe 1

**中文：** 一个自动售货机有三种状态：等待投币（IdleState）、已投币（HasCoinState）和售出商品（SoldState）。不同状态下，投币和按下购买按钮的行为不同。请用State模式画出类图。

**Deutsch:** Ein Verkaufsautomat hat drei Zustände: Warten auf Münze (IdleState), Münze eingeworfen (HasCoinState) und Produkt ausgegeben (SoldState). In jedem Zustand verhält sich der Automat bei Münzeinwurf und Kaufknopf anders. Zeichne ein Klassendiagramm mit dem State-Muster.

#### 题目2 / Aufgabe 2

**中文：** 一个订单系统的订单有多种状态：新建（NewOrder）、已支付（Paid）、已发货（Shipped）、已完成（Completed）。请用State模式画出类图，展示Order如何持有State引用，以及状态如何切换。

**Deutsch:** Ein Bestellsystem hat verschiedene Bestellzustände: Neu (NewOrder), Bezahlt (Paid), Versendet (Shipped), Abgeschlossen (Completed). Zeichne ein Klassendiagramm, das zeigt, wie Order die State-Referenz hält und wie Zustände wechseln.

---

### Memento 备忘录模式

#### 题目1 / Aufgabe 1

**中文：** 一个文本编辑器需要实现撤销（Undo）功能。每次编辑后保存编辑器状态，用户可以撤销到之前的状态。请用Memento模式画出类图，标明Originator（Editor）、Memento和Caretaker（History）。

**Deutsch:** Ein Texteditor soll eine Rückgängig-Funktion (Undo) haben. Nach jeder Bearbeitung wird der Zustand gespeichert, der Benutzer kann zum vorherigen Zustand zurückkehren. Zeichne ein Klassendiagramm mit Originator (Editor), Memento und Caretaker (History).

#### 题目2 / Aufgabe 2

**中文：** 一个游戏需要存档功能：玩家可以保存游戏进度，之后可以读取存档恢复到保存时的状态。请用Memento模式画出类图，展示Game、GameSave和SaveManager之间的关系。

**Deutsch:** Ein Spiel braucht eine Speicherfunktion: Der Spieler kann den Spielstand speichern und später laden. Zeichne ein Klassendiagramm mit dem Memento-Muster, das die Beziehung zwischen Game, GameSave und SaveManager zeigt.

---

## 二、结构模式 / Strukturmuster

---

### Adapter 适配器模式

#### 题目1 / Aufgabe 1

**中文：** 你的应用使用XML格式处理数据，但现在需要接入一个只能输出JSON的第三方库。请用Adapter模式画出类图，展示如何创建一个JsonToXmlAdapter让旧代码能够使用新的JSON库。

**Deutsch:** Deine Anwendung verarbeitet Daten im XML-Format, aber jetzt musst du eine Drittanbieter-Bibliothek einbinden, die nur JSON ausgibt. Zeichne ein Klassendiagramm mit dem Adapter-Muster, das zeigt, wie ein JsonToXmlAdapter erstellt wird.

#### 题目2 / Aufgabe 2

**中文：** 一个绘图程序使用圆形接口Circle（包含draw()方法），但你有一个旧的椭圆类LegacyOval（包含render()方法）需要集成。请用Adapter模式画出类图，展示OvalAdapter如何让LegacyOval适配Circle接口。

**Deutsch:** Ein Zeichenprogramm verwendet das Circle-Interface (mit draw()), aber du hast eine alte LegacyOval-Klasse (mit render()), die integriert werden muss. Zeichne ein Klassendiagramm, das zeigt, wie OvalAdapter die LegacyOval an das Circle-Interface anpasst.

---

### Proxy 代理模式

#### 题目1 / Aufgabe 1

**中文：** 一个图片查看器需要显示高清大图。由于图片加载很慢，你希望在图片加载完成前先显示一个占位图。请用Proxy模式画出类图，展示ImageProxy如何控制对RealImage的访问。

**Deutsch:** Ein Bildbetrachter soll hochauflösende Bilder anzeigen. Da das Laden langsam ist, soll zuerst ein Platzhalterbild angezeigt werden. Zeichne ein Klassendiagramm mit dem Proxy-Muster, das zeigt, wie ImageProxy den Zugriff auf RealImage kontrolliert.

#### 题目2 / Aufgabe 2

**中文：** 一个文档管理系统需要权限控制：只有管理员才能访问机密文档。请用Proxy模式画出类图，展示DocumentProxy如何在访问RealDocument之前检查用户权限。

**Deutsch:** Ein Dokumentenverwaltungssystem braucht Zugriffskontrolle: Nur Admins dürfen auf vertrauliche Dokumente zugreifen. Zeichne ein Klassendiagramm, das zeigt, wie DocumentProxy vor dem Zugriff auf RealDocument die Berechtigungen prüft.

---

### Facade 外观模式

#### 题目1 / Aufgabe 1

**中文：** 一个家庭影院系统包含多个子系统：DVD播放器、投影仪、音响和灯光控制。用户只想按一个按钮就开始看电影。请用Facade模式画出类图，展示HomeTheaterFacade如何封装这些子系统。

**Deutsch:** Ein Heimkinosystem besteht aus mehreren Subsystemen: DVD-Player, Projektor, Soundanlage und Lichtsteuerung. Der Benutzer möchte mit einem Knopfdruck einen Film starten. Zeichne ein Klassendiagramm, das zeigt, wie HomeTheaterFacade diese Subsysteme kapselt.

#### 题目2 / Aufgabe 2

**中文：** 一个网上购物系统后台涉及多个服务：库存检查、支付处理、物流安排和邮件通知。请用Facade模式画出类图，展示OrderFacade如何为客户端提供一个简单的placeOrder()接口。

**Deutsch:** Ein Online-Shopping-System hat mehrere Backend-Services: Bestandsprüfung, Zahlungsabwicklung, Logistik und E-Mail-Benachrichtigung. Zeichne ein Klassendiagramm, das zeigt, wie OrderFacade dem Client eine einfache placeOrder()-Schnittstelle bietet.

---

### Decorator 装饰器模式

#### 题目1 / Aufgabe 1

**中文：** 一个咖啡店系统：基础咖啡可以添加不同的配料（牛奶、糖、奶油），每种配料都会增加价格。请用Decorator模式画出类图，展示如何动态地给Coffee添加配料而不修改原始Coffee类。

**Deutsch:** Ein Café-System: Dem Basiskaffee können verschiedene Zutaten hinzugefügt werden (Milch, Zucker, Sahne), jede Zutat erhöht den Preis. Zeichne ein Klassendiagramm mit dem Decorator-Muster, das zeigt, wie Zutaten dynamisch hinzugefügt werden, ohne die Coffee-Klasse zu ändern.

#### 题目2 / Aufgabe 2

**中文：** 一个通知系统的基础功能是发送消息。你可以动态添加不同的发送渠道：短信、邮件、微信推送。请用Decorator模式画出类图，展示如何组合多种通知方式。

**Deutsch:** Ein Benachrichtigungssystem sendet grundlegend Nachrichten. Du kannst dynamisch verschiedene Kanäle hinzufügen: SMS, E-Mail, WeChat-Push. Zeichne ein Klassendiagramm, das zeigt, wie verschiedene Benachrichtigungsarten kombiniert werden.

---

### Composite 组合模式

#### 题目1 / Aufgabe 1

**中文：** 一个文件系统中，文件夹可以包含文件和其他文件夹。你需要统一计算任意节点（文件或文件夹）的大小。请用Composite模式画出类图，展示File、Folder和FileSystemComponent之间的关系。

**Deutsch:** In einem Dateisystem können Ordner Dateien und andere Ordner enthalten. Du musst die Größe jedes Knotens (Datei oder Ordner) einheitlich berechnen. Zeichne ein Klassendiagramm mit File, Folder und FileSystemComponent.

#### 题目2 / Aufgabe 2

**中文：** 一个公司组织结构：部门可以包含员工和子部门。你需要统一计算任意部门的总薪资。请用Composite模式画出类图，展示Employee、Department和OrganizationComponent之间的关系。

**Deutsch:** Eine Unternehmensstruktur: Abteilungen können Mitarbeiter und Unterabteilungen enthalten. Du musst das Gesamtgehalt jeder Abteilung einheitlich berechnen. Zeichne ein Klassendiagramm mit Employee, Department und OrganizationComponent.

---

## 三、创建模式 / Erzeugungsmuster

---

### Singleton 单例模式

#### 题目1 / Aufgabe 1

**中文：** 一个应用程序需要一个全局的配置管理器（ConfigManager），整个系统只能有一个实例。请用Singleton模式画出类图，标明private构造函数、private static实例字段和public static getInstance()方法。

**Deutsch:** Eine Anwendung braucht einen globalen Konfigurationsmanager (ConfigManager), von dem es nur eine Instanz geben darf. Zeichne ein Klassendiagramm mit private Konstruktor, private static Instanzfeld und public static getInstance().

#### 题目2 / Aufgabe 2

**中文：** 一个日志系统需要一个全局的日志记录器（Logger），确保所有模块都写入同一个日志文件。请用Singleton模式画出类图，并说明为什么这里适合使用单例。

**Deutsch:** Ein Logging-System braucht einen globalen Logger, damit alle Module in dieselbe Logdatei schreiben. Zeichne ein Klassendiagramm mit dem Singleton-Muster und erkläre, warum hier Singleton geeignet ist.

---

### Factory Method 工厂方法模式

#### 题目1 / Aufgabe 1

**中文：** 一个物流系统支持不同的运输方式：卡车（Truck）和轮船（Ship）。不同的物流公司创建不同的运输工具。请用Factory Method模式画出类图，展示Logistics（Creator）和Transport（Product）的关系。

**Deutsch:** Ein Logistiksystem unterstützt verschiedene Transportarten: LKW (Truck) und Schiff (Ship). Verschiedene Logistikunternehmen erstellen unterschiedliche Transportmittel. Zeichne ein Klassendiagramm mit Logistics (Creator) und Transport (Product).

#### 题目2 / Aufgabe 2

**中文：** 一个游戏中有不同类型的敌人：僵尸（Zombie）和吸血鬼（Vampire）。不同的关卡工厂创建不同类型的敌人。请用Factory Method模式画出类图，标明createEnemy()方法。

**Deutsch:** In einem Spiel gibt es verschiedene Gegnertypen: Zombie und Vampir. Verschiedene Level-Factories erstellen unterschiedliche Gegner. Zeichne ein Klassendiagramm mit der createEnemy()-Methode.

---

### Builder 建造者模式

#### 题目1 / Aufgabe 1

**中文：** 一个餐厅订单系统需要构建复杂的套餐：包含主食、饮料、甜点和配菜，有些是可选的。请用Builder模式画出类图，展示MealBuilder如何分步构建Meal对象，以及Director如何控制构建顺序。

**Deutsch:** Ein Restaurant-Bestellsystem muss komplexe Menüs zusammenstellen: Hauptgericht, Getränk, Dessert und Beilage, manche sind optional. Zeichne ein Klassendiagramm, das zeigt, wie MealBuilder schrittweise ein Meal-Objekt baut und wie Director die Reihenfolge steuert.

#### 题目2 / Aufgabe 2

**中文：** 一个汽车制造系统需要组装不同配置的汽车：引擎类型、座椅数量、GPS导航（可选）、天窗（可选）。请用Builder模式画出类图，展示CarBuilder和Car之间的关系。

**Deutsch:** Ein Autoproduktionssystem muss Autos mit verschiedenen Konfigurationen zusammenbauen: Motortyp, Sitzanzahl, GPS (optional), Schiebedach (optional). Zeichne ein Klassendiagramm mit CarBuilder und Car.

---

### Prototype 原型模式

#### 题目1 / Aufgabe 1

**中文：** 一个图形编辑器中，用户可以复制已有的图形（圆形、矩形）来创建新图形，而不是从头创建。请用Prototype模式画出类图，展示Shape接口的clone()方法以及Circle和Rectangle如何实现它。

**Deutsch:** In einem Grafikeditor kann der Benutzer vorhandene Formen (Kreis, Rechteck) kopieren, anstatt sie neu zu erstellen. Zeichne ein Klassendiagramm mit der clone()-Methode im Shape-Interface und wie Circle und Rectangle sie implementieren.

#### 题目2 / Aufgabe 2

**中文：** 一个游戏中有大量相似的怪物，创建新怪物时可以复制现有怪物模板然后修改部分属性。请用Prototype模式画出类图，展示Monster类如何实现clone()方法。

**Deutsch:** In einem Spiel gibt es viele ähnliche Monster. Beim Erstellen neuer Monster kann man eine Vorlage kopieren und einzelne Eigenschaften ändern. Zeichne ein Klassendiagramm, das zeigt, wie die Monster-Klasse clone() implementiert.


## MVC 模式 / Model-View-Controller

#### 题目1 / Aufgabe 1

**中文：** 设计一个简单的学生成绩管理系统。Model存储学生姓名和成绩，View负责在界面上显示学生信息，Controller处理用户的操作（如添加成绩、修改成绩）。请画出MVC模式的类图，标明：

- Model（StudentModel）：包含name、score属性和getter/setter方法
- View（StudentView）：包含displayStudentDetails()方法
- Controller（StudentController）：持有Model和View的引用，包含updateScore()和updateView()方法
- 用箭头标明三者之间的依赖关系

**Deutsch:** Entwirf ein einfaches Notenverwaltungssystem für Studenten. Das Model speichert Name und Note des Studenten, die View zeigt die Studenteninformationen auf der Oberfläche an, der Controller verarbeitet Benutzeraktionen (Note hinzufügen, Note ändern). Zeichne ein MVC-Klassendiagramm mit:

- Model (StudentModel): Attribute name, score und getter/setter-Methoden
- View (StudentView): Methode displayStudentDetails()
- Controller (StudentController): hält Referenzen auf Model und View, enthält updateScore() und updateView()
- Markiere die Abhängigkeiten zwischen den drei Komponenten mit Pfeilen

---

#### 题目2 / Aufgabe 2

**中文：** 设计一个简单的音乐播放器应用。请用MVC模式画出类图，包含：

- Model（MusicModel）：存储当前歌曲名称、播放状态（播放/暂停）、音量
- View（PlayerView）：显示歌曲信息、播放按钮状态、音量条
- Controller（PlayerController）：处理用户点击播放/暂停按钮、调节音量的操作

请标明：

1. 各个类的主要属性和方法
2. Controller如何更新Model
3. Model变化后如何通知View更新（可以结合Observer模式）

**Deutsch:** Entwirf eine einfache Musik-Player-Anwendung. Zeichne ein MVC-Klassendiagramm mit:

- Model (MusicModel): speichert aktuellen Songnamen, Wiedergabestatus (Play/Pause), Lautstärke
- View (PlayerView): zeigt Songinfo, Play-Button-Status, Lautstärkeregler
- Controller (PlayerController): verarbeitet Benutzerklicks auf Play/Pause und Lautstärkeregelung

Markiere:

1. Die wichtigsten Attribute und Methoden jeder Klasse
2. Wie der Controller das Model aktualisiert
3. Wie das Model die View über Änderungen benachrichtigt (kann mit Observer-Muster kombiniert werden)