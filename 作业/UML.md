
```
=================================== MODEL ====================================

 ┌──────────────────────────────┐  0..*  ┌──────────────────────────────┐
 │        <<abstract>>          │◇─────>│        <<interface>>          │
 │        Observable            │        │          Observer             │
 ├──────────────────────────────┤        ├──────────────────────────────┤
 │ -observers: List<Observer>   │        │ +update(src: Observable)     │
 ├──────────────────────────────┤        └──────────────────────────────┘
 │ +addObserver(o: Observer)    │                      △
 │ +removeObserver(o: Observer) │                      ┊ implements
 │ +notifyObservers()           │                      ┊
 └──────────────────────────────┘                      ┊
               △                                       ┊
               │ extends                               ┊
 ┌─────────────┴────────────────┐                      ┊
 │          Distance            │                      ┊
 ├──────────────────────────────┤                      ┊
 │ -distanceKm: double          │                      ┊
 ├──────────────────────────────┤                      ┊
 │ +getDistanceKm(): double     │                      ┊
 │ +setDistanceKm(v: double)    │                      ┊
 │ +getDistanceMiles(): double  │                      ┊
 └──────────────────────────────┘                      ┊
               ▲        ▲                              ┊
               │        │                              ┊
===============│========│==============================┊===================
               │        │                              ┊
               │        │     CONTROLLER               ┊
               │        │                              ┊
 ┌─────────────┘        └─────────────┐                ┊
 │  -model                    -model  │                ┊
 │                                    │                ┊
 ┌──────────────────────────┐  ┌──────┴─────────────────────┐     ┊
 │    MetricController      │  │      MilesController       │     ┊
 ├──────────────────────────┤  ├────────────────────────────┤     ┊
 │ -model: Distance         │  │ -model: Distance           │     ┊
 ├──────────────────────────┤  ├────────────────────────────┤     ┊
 │ +setKm(val: double)      │  │ +setMiles(val: double)     │     ┊
 └──────────────────────────┘  └────────────────────────────┘     ┊
               ▲                          ▲                       ┊
               │                          │                       ┊
===============│==========================│=======================┊=========
               │                          │                       ┊
               │ -controller              │ -controller           ┊
               │          VIEW            │                       ┊
               │                          │                       ┊
 ┌─────────────┴────────────┐  ┌──────────┴─────────────┐  ┌─────┴──────────────┐
 │       MetricView         │  │       MilesView        │  │   DistanceLabel    │
 │   <<implements Observer>>│  │ <<implements Observer>> │  │<<implements Observer>>│
 ├──────────────────────────┤  ├────────────────────────┤  ├────────────────────┤
 │ -controller: MetricCtrl  │  │ -controller: MilesCtrl │  │                    │
 ├──────────────────────────┤  ├────────────────────────┤  ├────────────────────┤
 │ +update(src: Observable) │  │ +update(src: Observable)│  │ +update(src)       │
 │ +onSliderChanged()       │  │ +onSliderChanged()     │  └────────────────────┘
 └──────────────────────────┘  └────────────────────────┘


===========================================================================
                          关系总览（简化）
===========================================================================

                      notifyObservers()
        Distance ─────────────────────────> <<Observer>>
         (Model)                            (interface)
           ▲                                     △
           │ setDistanceKm()                     ┊ implements
           │                                     ┊
  ┌────────┴─────────┐      user action   ┌─────┴──────────┐
  │   Controllers    │<───────────────────│     Views       │
  └──────────────────┘  ctrl.setKm/Miles  └────────────────┘

        循环: View ──> Controller ──> Model ──> View(Observer)
```

**9 条关系明细：**

|编号|从|到|类型|说明|
|---|---|---|---|---|
|1|Distance|Observable|继承 `─▷`|Distance 是 Observable|
|2|Observable|Observer|聚合 `◇─>` 0..*|持有观察者列表|
|3|MetricView|Observer|实现 `···▷`|View 接收 Model 通知|
|4|MilesView|Observer|实现 `···▷`|同上|
|5|DistanceLabel|Observer|实现 `···▷`|同上|
|6|MetricController|Distance|关联 `──>`|-model（写入）|
|7|MilesController|Distance|关联 `──>`|-model（写入）|
|8|MetricView|MetricController|关联 `──>`|-controller（转发用户操作）|
|9|MilesView|MilesController|关联 `──>`|-controller（转发用户操作）|

**完整数据流（以拖动公里 Slider 为例）：**

```
① 用户拖动 MetricView 的 Slider
        │
        ▼
② MetricView.onSliderChanged() 被触发
        │
        ▼
③ 调用 controller.setKm(value)
        │
        ▼
④ MetricController 调用 model.setDistanceKm(value)
        │
        ▼
⑤ Distance.setDistanceKm() 内部调用 notifyObservers()
        │
        ├──────────────────┬──────────────────┐
        ▼                  ▼                  ▼
⑥ MetricView          MilesView         DistanceLabel
   .update(src)        .update(src)      .update(src)
        │                  │                  │
        ▼                  ▼                  ▼
⑦ src→getDistanceKm() src→getDistMiles() 显示两种单位
   更新Slider=20       更新Slider≈12.4    "20km = 12.4mi"
```

**与原图对比，修正了三个关键问题：**

原图中 View（Slider）没有任何途径通知 Controller → 现在 View 持有 `-controller` 引用，通过 `onSliderChanged()` 调用 Controller。两个 Controller 都明确持有 `-model: Distance` 引用指向同一个 Model 实例。View 通过 `update(src: Observable)` 的参数获取 Model 数据，不需要额外存储 Model 引用，保持了 View 对 Model 的最小依赖——View 只依赖 Observer 接口和 Observable 基类，Model 核心完全不依赖 GUI。