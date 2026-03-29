## 一、需要背诵的核心概念 (Zu merkende Kernkonzepte)

### 1. 编程的本质 (Wesen der Programmierung)

编程不是艺术 (Kunst)，而是**手艺 (Handwerk)**。它需要技巧 (Geschick)、纪律 (Disziplin) 和持续练习 (Übung)。

**代码可读性优先于效率**：代码是需求的形式化描述 (formale Beschreibung der Anforderungen)，应尽可能清晰地表达需求。效率是第二优先级。

---

### 2. LeBlanc 定律 (Gesetz von LeBlanc)

> **"以后再改" = "永远不改"** (Später = Niemals)

坏代码会形成恶性循环：坏代码 → 修改困难 → 临时修补 → 代码更差 → 技术债务攀升 → 更多坏代码……

---

### 3. 变量命名九大规则 (Neun Regeln der Variablenbenennung)

基于 Clean Code 第 2 章 (Kapitel 2)。

|编号|规则（中文）|规则（德文）|好例子 [+]|坏例子 [x]|
|---|---|---|---|---|
|1|选择表达目的的名称|Zweckbeschreibende Namen wählen|`daysSinceCreation`, `timeLimitInMs`|`d`, `day`|
|2|避免错误信息|Fehlinformationen vermeiden|`accountsByStudentName`, `students`|`accounts`, `studentList`（非 List 时）|
|3|区分要明显|Unterschiede deutlich machen|`getAccountByName` vs `getAccountById`|`getAccount` vs `getAccountInfo`|
|4|同一概念统一命名|Gleiche Konzepte konsistent benennen|统一使用 `fetch` 或 `get`|混用 `fetch` / `get` / `retrieve`|
|5|可发音的名称|Aussprechbare Namen verwenden|`count`, `current`, `prefix`|`cnt`, `curr`, `prfx`|
|6|可搜索的名称|Suchbare Namen verwenden|`WORK_DAYS_PER_WEEK`|`5`（魔数 magic number）|
|7|避免幽默的名称|Humorige Namen vermeiden|`deleteFolder(path)`|`shinraTensei(path)`|
|8|避免编码前缀|Codierungen vermeiden|`node`, `results`|`p_node`, `l_results`（匈牙利命名法）|
|9|避免心智映射|Mentale Mappings vermeiden|`for (Student student : allStudents)`|`var element = data.get(i)`|

**最佳实践补充**：

|规则|德文|说明|
|---|---|---|
|类名用名词|Klassennamen = Substantive|`CourseName` 而非 `CreateCourseName`；避免 `Data`、`Info`|
|方法名用动词|Methodennamen = Verben|`add(...)` 而非 `addition(...)`；`didAttendCourse(...)` 而非 `courseAttendance(...)`|
|领域名和技术名分开|Domänensprache vs. Fachbegriffe|领域概念用领域词汇，技术概念（算法、数据结构）用技术术语|
|避免冗余上下文|Keine unnötigen Kontexte|`Student.getName()` 而非 `Student.getStudentName()`|

---

### 4. 注释分类 (Kommentar-Klassifikation)

**核心规则**：优先改善代码本身，而非添加注释。每个注释都是对代码不够清晰的承认。

#### 六种有效注释 (Gültige Kommentare)

|编号|类型（中文）|类型（德文）|示例|
|---|---|---|---|
|1|澄清|Klarstellung|`// a < b` 在 `assertTrue(a.compareTo(b) == -1)` 后|
|2|意图说明|Erklärung der Absicht|`// Create large pool of threads to trigger potential race conditions`|
|3|后果警告|Warnung vor Konsequenzen|`// WARNING: This method clears session cache`|
|4|强调重要细节|Verstärkung|`// The trim is important. It removes spaces that break parsing.`|
|5|非功能需求|Nicht-funktionale Anforderung|`// We assume UTF-8 encoding by default.`|
|6|TODO 注释|TODO-Kommentare|`// TODO: Remove after VersionManager update`|

#### 八种坏注释 (Schlechte Kommentare)

|编号|类型（中文）|类型（德文）|要点|
|---|---|---|---|
|1|含混不清|Mumbling (Geraune)|模糊注释，引用不明确|
|2|冗余注释|Redundante Kommentare|重复代码已说的内容|
|3|噪音注释|Noise (Geschwätz)|说显而易见的事：`// The scanner`|
|4|误导注释|Irreführende Kommentare|描述与实际行为不一致|
|5|位置标记|Positionsmarkierungen|`////// Constructors ////////`|
|6|括号结束注释|Blockende-Kommentare|`} // endWhile` — 方法太长就该拆分|
|7|注释掉的代码|Auskommentierter Code|删掉！版本控制会保存|
|8|日记注释|Tagebuch-Kommentare|用 `git log` 和 `git blame` 替代|

---

### 5. 函数设计原则 (Prinzipien für Funktionen)

基于 Clean Code 第 3 章 (Kapitel 3)。

|原则（中文）|原则（德文）|说明|
|---|---|---|
|单一抽象层次|Eine Abstraktionsebene|每个方法只在一个抽象层次上运作；代码像报纸一样从上到下阅读|
|UM-ZU 段落|UM-ZU-Absätze|好代码可用"为了……我们……"来描述每一层|
|参数尽量少|Wenig Parameter|参数越多，测试组合越多；类字段也是隐含参数|
|避免副作用|Keine Seiteneffekte|不修改传入参数；查询方法不应偷偷修改状态|
|命令与查询分离|Anweisung und Abfrage trennen|函数要么执行操作 (Command)，要么返回信息 (Query)，不要两者兼做|

**三类副作用**：修改输入参数 (Input-Mutation)、查询中隐藏修改 (Hidden Mutation)、竞态条件 (Race Condition / Lazy Init)。

---

### 6. 对象 vs. 数据结构 (Objekte vs. Datenstrukturen)

|维度|数据结构 (Datenstruktur)|对象 (Objekt)|
|---|---|---|
|数据|暴露 (offen, public)|隐藏 (verborgen, private)|
|行为|在外部 (extern)|在内部 (intern)|
|例子|`CourseAttendance` record + 外部 `GradeProcessor`|`Transcript` 类封装数据和方法|

**迪米特法则 (Law of Demeter)**："不要和陌生人说话。"一个对象只应调用：自身 (`this`)、参数对象、自己创建的对象、直接成员变量的方法。避免 `object.getX().getY().getZ()` 链式调用。解决方案：直接传递所需对象，或使用 **Tell, Don't Ask** 模式。

---

### 7. 类的设计原则 (Prinzipien für Klassen)

基于 Clean Code 第 10 章 (Kapitel 10)。

|原则（中文）|原则（德文/英文）|说明|
|---|---|---|
|单一职责原则|Single-Responsibility Principle (SRP)|一个类只有一个变化原因 (ein Grund zur Änderung)|
|高内聚|Hohe Kohäsion|类内元素关联度高|
|低耦合|Geringe Kopplung|类间依赖程度低|
|依赖注入|Dependency Injection (IoC)|通过接口注入依赖，而非在类内部 new 具体实现；使测试可用 Mock|

**注意**：少代码 ≠ 好设计。不要过度拆分一个逻辑完整的类。

---

### 8. 格式化原则 (Formatierungsregeln)

基于 Clean Code 第 5 章 (Kapitel 5)。

|维度|原则（中文）|原则（德文）|
|---|---|---|
|垂直|报纸隐喻：重要的在上面，细节在下面|Zeitungsmetapher|
|垂直|概念间空行分隔|Leerzeilen zwischen Konzepten|
|垂直|相关概念靠近|Verwandte Konzepte vertikal nah|
|垂直|调用者在被调用者上方|Aufrufer über Aufgerufenem|
|垂直|变量声明靠近使用|Variablen nah an Verwendung|
|水平|行长 80–100 字符|Max 80–100 Zeichen pro Zeile|
|水平|空格增强可读性|Leerzeichen für Lesbarkeit|
|水平|缩进层次清晰|Einrückung für klare Hierarchie|
|团队|团队规则优先于个人偏好|Teamregeln über persönliche Präferenz|

**Chunking & Beacons**：人类短期记忆约 7±2 个 Chunks。Beacons 是代码中帮助快速定位的视觉锚点（如循环结构、return 语句、变量初始化）。

---

### 9. 错误处理 (Fehlerbehandlung)

基于 Clean Code 第 7 章 (Kapitel 7)。

#### 两大错误类型

|类型（中文）|类型（德文）|例子|
|---|---|---|
|编程错误 (Bug)|Programmierfehler|除零、空指针、前置条件违反|
|环境错误|Fehler durch Umgebung|用户输入无效、网络超时、权限不足、文件缺失|

#### 错误通信机制

|机制|语言|优点|缺点|
|---|---|---|---|
|返回值 (Return Values)|C, Go, Rust|显式控制流|容易忘记检查|
|受检异常 (Checked Exceptions)|Java|编译器强制|传播开销大，违反抽象|
|非受检异常 (Unchecked Exceptions)|Java, Python, C#|灵活、代码更整洁|可能被遗忘|

#### 处理策略

|策略（中文）|策略（德文）|适用场景|
|---|---|---|
|不捕获 Bug|Bugs nicht fangen|编程错误应修复代码，不应 catch|
|重试|Retry (Exponential Backoff)|网络超时等临时故障|
|回退|Fallback|缓存 → 数据库 → 默认值|
|熔断器|Circuit Breaker|超过最大尝试次数后回退或失败|

#### 最佳实践

|实践（中文）|实践（德文）|
|---|---|
|不返回 null|Keine Null zurückgeben — 用 `Optional` 或抛异常|
|不传递 null|Keine Null übergeben — 用 `Objects.requireNonNull()`|
|传递上下文|Kontext kommunizieren — 异常消息包含 URL、ID 等|
|好的异常命名|Gute Exception-Namen — `ConnectionFailure` 而非 `ConnectionFailureException`|

---

### 10. 风险管理三类风险 (Drei Risikokategorien)

|类型（中文）|类型（德文）|定义|例子|
|---|---|---|---|
|项目风险|Projektrisiko|威胁项目进度|核心成员离职、硬件故障、模拟器不兼容|
|产品风险|Produktrisiko|威胁产品质量|软件无法实时运行、传感器数据不准|
|商业风险|Geschäftsrisiko|威胁商业成功|超时超预算导致资助中断|

**风险应对策略**：避免策略 (Vermeidungsstrategie) 减少风险源、最小化策略 (Minimierungsstrategie) 降低风险影响。

---

### 11. 代码改进五大方向 (Fünf Verbesserungsrichtungen)

针对 Bubble Sort 练习总结的通用改进方向：

|方向（中文）|方向（德文）|说明|
|---|---|---|
|降低嵌套深度|Verschachtelungstiefe reduzieren|简化 if-else 结构，合并到循环条件中|
|简化循环逻辑|Schleifenlogik vereinfachen|去除冗余 break/continue|
|引入临时变量|Temporäre Variablen einführen|避免重复 `list.get(index)`，提高可读性|
|消除重复|Duplikation reduzieren|将交换逻辑提取为 `swap()` 方法|
|统一格式|Konsistente Formatierung|缩进和空行保持一致|

---

## 二、中德对照练习题 (Übungsfragen Chinesisch-Deutsch)

### 题目 1：效率 vs. 可读性 (Effizienz vs. Verständlichkeit)

**Q:** 讨论：效率和可读性，哪个更重要？  
**Q (DE):** Diskutieren Sie: Was ist wichtiger — Effizienz oder Verständlichkeit von Code?

**A:** 可读性始终优先。代码是需求在机器可读形式中的形式化描述，应尽可能清晰地表达需求。效率是第二优先级。  
**A (DE):** Die Verständlichkeit hat immer Vorrang. Code ist die formale Beschreibung der Anforderungen in maschinenlesbarer Form. Erst mit zweiter Priorität sollte Code auch effizient sein.

---

### 题目 2：识别排序算法 (Sortieralgorithmus erkennen)

**Q:** 以下代码实现了哪种排序算法？其工作原理是什么？

```java
while (hasSwapped) {
    hasSwapped = false;
    for (int index = 0; index < list.size() - 1; index++) {
        if (list.get(index) > list.get(index + 1)) {
            swap(list, index, index + 1);
            hasSwapped = true;
        }
    }
}
```

**Q (DE):** Welchen Sortieralgorithmus implementiert der obige Code?

**A:** 冒泡排序 (Bubble Sort)。它反复遍历列表，比较相邻元素，将较大的元素向右"冒泡"。  
**A (DE):** Der Code implementiert den Bubble Sort Algorithmus. Er durchläuft die Liste wiederholt und vergleicht benachbarte Elemente, wobei größere Elemente nach rechts „blubbern".

---

### 题目 3：注释分类判断 (Kommentar-Kategorie bestimmen)

**Q:** 以下注释属于哪种有效注释类型？

```java
// Create large pool of threads to trigger potential race conditions
for (int i = 0; i < 1000; i++) {
    new Thread(createDateUsingSystemTimezone()).start();
}
```

**Q (DE):** Zu welcher Kategorie gültiger Kommentare gehört der obige Kommentar?

**A:** 意图说明 (Erklärung der Absicht)。

---

### 题目 4：注释分类判断 — 澄清 (Klarstellung)

**Q:** 以下注释属于哪种有效注释类型？

```java
assertTrue(a.compareTo(b) == -1); // a < b
```

**Q (DE):** Zu welcher Kategorie gültiger Kommentare gehört dieser Kommentar?

**A:** 澄清 (Klarstellung)。

---

### 题目 5：识别坏注释 — 噪音 (Noise erkennen)

**Q:** 以下注释属于哪种坏注释类型？为什么？

```java
for (int i = 0; i < 1000; i++) {
    // create a new thread and start it
    new Thread(createDateUsingSystemTimezone()).start();
}
```

**Q (DE):** Zu welcher Kategorie schlechter Kommentare gehört dieser Kommentar?

**A:** 噪音注释 (Noise / Geschwätz)。注释只是重复了代码已经清楚表达的内容。  
**A (DE):** Noise (Geschwätz). Der Kommentar wiederholt nur, was der Code bereits klar ausdrückt.

---

### 题目 6：识别坏注释 — 冗余 (Redundanz erkennen)

**Q:** 以下注释属于哪种坏注释类型？

```java
/** The upper bound of the interval */
private long upperBound;
```

**Q (DE):** Zu welcher Kategorie schlechter Kommentare gehört dieser Kommentar?

**A:** 冗余注释 (Redundanter Kommentar)。变量名 `upperBound` 已充分表达了含义。

---

### 题目 7：识别坏注释 — 含混不清 (Mumbling erkennen)

**Q:** 以下注释属于哪种坏注释类型？为什么？

```java
private void processData() {
    try {
        readFromCSV();
    } catch (IOException e) {
        // csv cannot be processed twice
    }
}
```

**Q (DE):** Zu welcher Kategorie schlechter Kommentare gehört dieser Kommentar?

**A:** 含混不清 (Mumbling / Geraune)。读者无法理解"不能处理两次"是什么意思——是读取会失败？还是数据会被破坏？需要什么后续操作？  
**A (DE):** Mumbling (Geraune). Der Leser kann nicht verstehen, was „cannot be processed twice" konkret bedeutet und was als Konsequenz passieren soll.

---

### 题目 8：识别坏注释 — 误导 (Irreführend erkennen)

**Q:** 以下注释属于哪种坏注释类型？

```java
// Returns the union of this interval and the other interval.
applyUnion(Interval other) {
    this.lowerBound = Math.min(this.lowerBound, other.lowerBound);
    this.upperBound = Math.max(this.upperBound, other.upperBound);
    return this;
}
```

**Q (DE):** Zu welcher Kategorie schlechter Kommentare gehört dieser Kommentar?

**A:** 冗余注释 (Redundanter Kommentar)。方法名 `applyUnion` 和参数 `Interval other` 已经清楚表达了意图，注释只是重复了方法签名的信息。  
**A (DE):** Redundanter Kommentar. Der Methodenname `applyUnion` und der Parameter `Interval other` drücken die Absicht bereits klar aus.

---

### 题目 9：魔数消除 (Magische Zahlen eliminieren)

**Q:** 如何通过常量消除以下代码中的注释？

```java
// add to list if the status of the cell is flagged
if (x[0] == 4) list1.add(x);
```

**Q (DE):** Wie können Sie mit Hilfe von Konstanten den Kommentar im obigen Code unnötig machen?

**A:** 用命名常量替换魔数：

```java
if (cell[STATUS_FIELD] == FLAGGED) flaggedCells.add(cell);
```

**A (DE):** Ersetzen Sie die magischen Zahlen durch sprechende Konstanten: `STATUS_FIELD`, `FLAGGED`.

---

### 题目 10：方法提取消除注释 (Methode extrahieren)

**Q:** 如何通过提取方法来消除以下代码中的注释？

```java
// Print debug information if necessary
if (printDebugLogs) {
    System.out.println("Looked at " + x);
    // ...
}
```

**Q (DE):** Wie kann man den Kommentar durch geschicktes Auslagern in eine neue Methode ersetzen?

**A:** 提取为 `debugLog(cell)` 方法：

```java
if (cell[STATUS_FIELD] == FLAGGED) flaggedCells.add(cell);
debugLog(cell);
```

**A (DE):** Extrahieren Sie den Debug-Code in eine eigene Methode `debugLog(int[] cell)`.

---

### 题目 11：格式化修复 (Formatierung korrigieren)

**Q:** 格式化以下代码，使其可读：

```java
public boolean isPalindrome(char[] word)
{ int back = word.length- 1; int front = 0;
while(front < back) if (word[front] != word[back]) return false; else
{front = front + 1; back = back- 1;} return true;
```

**Q (DE):** Der obenstehende Code ist schwer lesbar. Formatieren Sie den Code.

**A:**

```java
public boolean isPalindrome(char[] word) {
    int back = word.length - 1;
    int front = 0;

    while (front < back) {
        if (word[front] != word[back]) {
            return false;
        } else {
            front = front + 1;
            back = back - 1;
        }
    }

    return true;
}
```

---

### 题目 12：为什么要节制使用注释？(Warum Kommentare sparsam einsetzen?)

**Q:** 用自己的话解释为什么要节制使用注释。  
**Q (DE):** Erklären Sie in eigenen Worten: Warum ist es wichtig, Kommentare sparsam und überlegt einzusetzen?

**A:** 三个原因：(1) 注释是代码表达能力不足的信号——如果需要注释，说明代码本身不够清晰，应优先改善代码。(2) 注释会过时——时间越久、距离代码越远，注释错误的概率越大。(3) 开发者往往不维护注释——不准确的注释比没有注释更糟糕，因为它们会误导读者。  
**A (DE):** (1) Kommentare sind ein Zeichen schlechten Codes — besser ist selbsterklärender Code. (2) Kommentare veralten leicht — je älter, desto wahrscheinlicher falsch. (3) Entwickler pflegen Kommentare oft nicht — ungenaue Kommentare sind schlimmer als keine.

---

### 题目 13：JavaDoc 强制讨论 (JavaDoc-Pflicht diskutieren)

**Q:** 讨论：是否应该在软件项目中强制要求所有 public 方法添加 JavaDoc？  
**Q (DE):** Sollte in einem Softwareprojekt eine Regel „alle public-Methoden müssen mit JavaDoc versehen sein" durchgesetzt werden?

**A:**

正方 (Pro)：所有公共 API 都有文档；用户通过 IDE 获得上下文；不会遗漏重要 API。

反方 (Con)：可能产生冗余文档；强制性会导致敷衍文档；参数名已足够说明时文档多余；重要 API 也可在 Code Review 中要求文档。

---

### 题目 14：项目风险举例 (Projektrisiko nennen)

**Q:** 在大学机器人臂控制软件项目中，举一个项目风险的例子。  
**Q (DE):** Nennen Sie ein Beispiel für ein Projektrisiko im Roboterarm-Szenario.

**A:** 学生助理的高流动率导致项目延迟 (Hohe Fluktuation von studentischen Hilfskräften sorgt für zeitlichen Verzug)。其他例子：科研人员离职、模拟器与真实机器臂接口不一致、硬件故障。

---

### 题目 15：产品风险举例 (Produktrisiko nennen)

**Q:** 举一个可能影响软件质量的产品风险。  
**Q (DE):** Nennen Sie ein Beispiel für ein Produktrisiko.

**A:** 软件无法在机器人臂上实时运行 (Die Software kann nicht in Echtzeit auf dem Roboterarm ausgeführt werden)。另一个例子：传感器数据不精确。

---

### 题目 16：商业风险举例 (Geschäftsrisiko nennen)

**Q:** 举一个可能影响项目成功的商业风险。  
**Q (DE):** Nennen Sie ein Beispiel für ein Geschäftsrisiko.

**A:** 超出时间和成本框架，导致后续资助被取消 (Der Zeit- und Kostenrahmen wird überschritten und das Projekt wird nicht weiter gefördert)。

---

### 题目 17：风险应对策略 (Risikostrategien)

**Q:** 针对"学生助理高流动率"这一项目风险，提出应对策略。  
**Q (DE):** Nennen Sie eine geeignete Strategie zum Umgang mit der hohen Fluktuation von studentischen Hilfskräften.

**A:**

避免策略 (Vermeidungsstrategie)：减少对学生助理的依赖，例如通过自动化任务或使用正式员工。

最小化策略 (Minimierungsstrategie)：通过定期会议、更长的合同或更好的融入来加强学生对项目的归属感。

---

### 题目 18：抽象层次 (Abstraktionsebenen)

**Q:** 为什么以下代码违反了"单一抽象层次"原则？

```java
public void registerStudent(String name, String matNr) {
    if (name == null || name.trim().isEmpty()) { throw ...; }
    Pattern p = Pattern.compile("^\\d{7}$");
    if (!p.matcher(matNr).matches()) { throw ...; }
    if (databaseContainsStudent(name)) { throw ...; }
    persistStudent(name, matNr);
    sendWelcomeEmail(name);
}
```

**Q (DE):** Warum verletzt der obige Code das Prinzip „eine Abstraktionsebene pro Methode"?

**A:** 正则表达式验证属于低层抽象，而 `databaseContainsStudent` 和 `persistStudent` 属于高层抽象。两个层次混在同一方法中。应将验证逻辑提取到 `validateStudentData(...)` 等独立方法中。  
**A (DE):** Regex-Validierung ist Low-Level, während `databaseContainsStudent` und `persistStudent` High-Level sind. Verschiedene Abstraktionsebenen sind in einer Methode gemischt.

---

### 题目 19：副作用识别 (Seiteneffekte erkennen)

**Q:** 以下代码有什么副作用问题？

```java
void updateStudentsBasedOnContext(Context context, List<Student> students) {
    /* modify students */
}
```

**Q (DE):** Welchen Seiteneffekt hat der obige Code?

**A:** 方法修改了作为输入参数传入的 `students` 列表，调用者可能不知道列表被修改了。应返回新列表而非修改传入参数。  
**A (DE):** Die Methode modifiziert die als Parameter übergebene `students`-Liste. Der Aufrufer erwartet das möglicherweise nicht. Besser: eine neue Liste zurückgeben.

---

### 题目 20：命令与查询分离 (Command-Query-Separation)

**Q:** 为什么以下代码违反了命令与查询分离原则？如何改进？

```java
if (students.remove(student)) {
    System.out.println("Student removed");
}
```

**Q (DE):** Warum verletzt der obige Code das Command-Query-Separation-Prinzip?

**A:** `remove` 同时是 Command（删除元素）和 Query（返回是否成功）。应分开：

```java
if (students.contains(student)) {    // Query
    students.remove(student);         // Command
    System.out.println("Student removed");
}
```

---

### 题目 21：SRP 判断 (SRP-Verletzung erkennen)

**Q:** 一个 `Employee` 类同时包含 `calculatePay()`、`generateReport()`、`save()` 方法，这违反了什么原则？  
**Q (DE):** Eine `Employee`-Klasse enthält `calculatePay()`, `generateReport()` und `save()`. Welches Prinzip wird verletzt?

**A:** 违反了单一职责原则 (SRP)。三个方法分别对应不同的变化原因（工资规则、报告格式、数据库结构），应拆分为 `PayrollCalculator`、`Reporter`、`Repository` 三个类。  
**A (DE):** Das Single-Responsibility Principle (SRP). Jede Methode hat einen anderen Änderungsgrund und sollte in eine eigene Klasse ausgelagert werden.

---

### 题目 22：迪米特法则 (Law of Demeter)

**Q:** `course.getDepartment().getSecretary().getContact().getEmail()` 违反了什么法则？给出两种解决方案。  
**Q (DE):** Welches Prinzip verletzt `course.getDepartment().getSecretary().getContact().getEmail()`?

**A:** 违反迪米特法则 (Law of Demeter)。  
方案 A（直接传递）：调用者获取 Contact 并直接传入 — `enrollStudent(student, course, secretaryContact)`。  
方案 B（Tell, Don't Ask）：每层只告诉直接伙伴做事 — `course.sendEnrollmentNotification(student)`，由 Course 委托给 Department，再委托给 Secretary。

---

### 题目 23：不返回 null (Keine Null zurückgeben)

**Q:** 如何改进以下可能返回 null 的代码？

```java
public Student getStudentById(String id) {
    return studentDatabase.get(id);  // could be null
}
```

**Q (DE):** Wie kann man den obigen Code verbessern, der möglicherweise null zurückgibt?

**A:** 方案一：使用 `Optional`：

```java
public Optional<Student> getStudentById(String id) {
    return Optional.ofNullable(studentDatabase.get(id));
}
```

方案二：抛出异常：

```java
if (student == null) {
    throw new StudentNotFound("Student with ID " + id + " not found.");
}
```

---

### 题目 24：Checked vs. Unchecked Exception

**Q:** Checked Exception 的传播问题是什么？  
**Q (DE):** Was ist das Problem bei der Propagation von Checked Exceptions?

**A:** 如果底层方法抛出 `IOException`，整个调用链上每一层都必须声明 `throws IOException`。这违反了抽象原则 (Abstraktionsverletzung)：上层不应关心底层的 IO 细节。如果底层将来不再抛出该异常，所有调用者都得修改。  
**A (DE):** Jede Schicht muss `throws IOException` deklarieren — eine Abstraktionsverletzung. Die obere Schicht sollte sich nicht um IO-Details kümmern müssen.

---

### 题目 25：报纸隐喻 (Zeitungsmetapher)

**Q:** 什么是代码的"报纸隐喻"？  
**Q (DE):** Was besagt die Zeitungsmetapher für Code-Formatierung?

**A:** 代码结构应像报纸文章：标题（类名/方法名）在最上面，然后是摘要（高层公共方法），最后是细节（低层私有方法）。从上到下阅读，抽象度递减。  
**A (DE):** Code soll wie ein Zeitungsartikel aufgebaut sein: Überschrift (Name) → Zusammenfassung (High-Level-Methoden) → Details (Low-Level-Methoden). Von oben nach unten, Abstraktionsgrad abnehmend.

---

## 三、高频德语术语速记表 (Vokabelliste Clean Code)

|德文|中文|英文|
|---|---|---|
|Sauberer Code / Clean Code|整洁代码|Clean Code|
|Verständlichkeit|可读性/可理解性|Readability|
|Effizienz|效率|Efficiency|
|Handwerk|手艺|Craftsmanship|
|Variablenbenennung|变量命名|Variable naming|
|Zweckbeschreibend|表达目的的|Purpose-revealing|
|Fehlinformation|错误信息/误导|Disinformation|
|Aussprechbar|可发音的|Pronounceable|
|Suchbar|可搜索的|Searchable|
|Magische Zahl|魔数|Magic number|
|Mentales Mapping|心智映射|Mental mapping|
|Ungarische Notation|匈牙利命名法|Hungarian notation|
|Kommentar|注释|Comment|
|Redundanter Kommentar|冗余注释|Redundant comment|
|Geschwätz / Noise|噪音注释|Noise comment|
|Irreführender Kommentar|误导注释|Misleading comment|
|Geraune / Mumbling|含混不清的注释|Mumbling|
|Tagebuch-Kommentar|日记注释|Journal comment|
|Auskommentierter Code|注释掉的代码|Commented-out code|
|Positionsmarkierung|位置标记|Banner comment|
|Klarstellung|澄清|Clarification|
|Erklärung der Absicht|意图说明|Intent explanation|
|Warnung vor Konsequenzen|后果警告|Warning|
|Verstärkung|强调|Amplification|
|Formatierung|格式化|Formatting|
|Vertikale Formatierung|垂直格式化|Vertical formatting|
|Horizontale Formatierung|水平格式化|Horizontal formatting|
|Zeitungsmetapher|报纸隐喻|Newspaper metaphor|
|Einrückung|缩进|Indentation|
|Teamregeln|团队规则|Team rules|
|Chunking|组块化|Chunking|
|Beacons|信标/锚点|Beacons|
|Abstraktionsebene|抽象层次|Abstraction level|
|Seiteneffekt|副作用|Side effect|
|Nebeneffekt|副作用（同义）|Side effect|
|Anweisung (Command)|命令|Command|
|Abfrage (Query)|查询|Query|
|Verschachtelungstiefe|嵌套深度|Nesting depth|
|Schleifenlogik|循环逻辑|Loop logic|
|Duplikation|重复/冗余|Duplication|
|Refactoring|重构|Refactoring|
|Bubble Sort|冒泡排序|Bubble Sort|
|Benachbarte Elemente|相邻元素|Adjacent elements|
|Objekt|对象|Object|
|Datenstruktur|数据结构|Data structure|
|Gesetz von Demeter|迪米特法则|Law of Demeter|
|Single-Responsibility Principle (SRP)|单一职责原则|Single Responsibility Principle|
|Kohäsion|内聚|Cohesion|
|Kopplung|耦合|Coupling|
|Dependency Injection (DI)|依赖注入|Dependency Injection|
|Inversion of Control (IoC)|控制反转|Inversion of Control|
|Schnittstelle / Interface|接口|Interface|
|Fehlerbehandlung|错误处理|Error handling|
|Programmierfehler|编程错误|Programming error / Bug|
|Umgebungsfehler|环境错误|Environment error|
|Ausnahme / Exception|异常|Exception|
|Checked Exception|受检异常|Checked exception|
|Unchecked Exception|非受检异常|Unchecked exception|
|Rückgabewert|返回值|Return value|
|Wiederholung / Retry|重试|Retry|
|Rückfallebene / Fallback|回退|Fallback|
|Schutzschalter / Circuit Breaker|熔断器|Circuit breaker|
|Projektrisiko|项目风险|Project risk|
|Produktrisiko|产品风险|Product risk|
|Geschäftsrisiko|商业风险|Business risk|
|Vermeidungsstrategie|避免策略|Avoidance strategy|
|Minimierungsstrategie|最小化策略|Mitigation strategy|
|Fluktuation|流动率/人员变动|Fluctuation / Turnover|
|Technische Schulden|技术债务|Technical debt|
|Gesetz von LeBlanc|LeBlanc 定律|LeBlanc's Law|
|Principle of Least Astonishment|最小惊讶原则|Principle of Least Astonishment|