#TimeLine

命令一览

```
# xxx - xxx

################ tts ################
define speaker "tts" "Microsoft Huihui Desktop" 0 100

################ config ################
alertall "xxx" before 3 speak "tts" "xxx"
hideall "xxx"

################ main ################
0 "--重置--" sync /Removing combatant xxx/ window 10000 jump 0

# Phase 1
1 "--开始--" sync /xxx/ window 10000
...
```

#### func
- **define speaker:** `define speaker "tts" "Microsoft Huihui Desktop" 0 100`
- **alertall:** `alertall "xxx" before 3 speak "tts" "xxx"`
- **hideall:** `hideall "xxx"`

#### prop
- **duration:** `duration 5`
- **sync:** `sync /xxx/`
- **window:** `window 2,2`
- **jump:** `jump 0`

<br />

## 自动加载

如果将时间轴文件命名为区域名称，则可以在移动区域后自动加载文件。

```
须佐之男歼殛战.txt
```

<br />

## 同步

- `sync` 正则匹配日志
- `duration` 施法时间


```
666 "破浪斩" duration 4 sync /须佐之男正在发动“破浪斩”/ window 2, 2
```

#### 增加删除对象

- `Added new combatant`
- `Removing combatant`

```
666 "天之丛云" sync /Added new combatant 天之丛云/ window 10
```

#### 发动技能

- `xxx正在发动“xxx”`
- `xxx发动了“xxx”`

```
333 "八咫镜" sync /须佐之男发动了“八咫镜”/ window 2, 2
...
666 "云间放电" duration 2 sync /雷云正在发动“云间放电”/ window 2, 2
```

<br />

## 误差调整

- `window` 前误差, 后误差

一般为前后误差2秒，默认为5秒

```
window 2, 2
```

#### 阶段性调整

一般调阶段时请将误差设为`10000`

```
1 "--开始--" sync /欢庆吧！跳舞吧！/ window 10000
...
666 "--Phase 2--" sync /有意思，真有意思！/ window 10000
```

<br />

## 跳转

- `jump` 跳转时间

#### 循环

```
333 "岩户隐" sync /须佐之男发动了“岩户隐”/ window 2, 2
...
666 "岩户隐" sync /须佐之男发动了“岩户隐”/ window 100 jump 333
```

#### 重置

- 使用 `Removing combatant` 判断Boss重置
- 如果指定了0秒，将在起始位置进入待机状态。

```
0 "--重置--" sync /Removing combatant 须佐之男/ window 10000 jump 0
```

<br />

## 提示

- tts 语音报幕提示

```
define speaker "tts" "Microsoft Huihui Desktop" 0 100
alertall "强击" before 3 speak "tts" "T死刑"
```
- 提示音

```
define alertsound "提示音" "提示音.wav"
alertall "强击" before 3 sound "提示音"
```

<br />

## 隐藏

隐藏不需要的提示，一般可作为T，奶，DPS单独配置用。

```
hideall "xxx"
```

## 示例

- 须佐之男歼殛战.txt

```
# 须佐之男歼殛战 - 须佐之男

################ TTS ################

define speaker "tts" "Microsoft Huihui Desktop" 0 100
#define speaker "tts" "Microsoft Hanhan Desktop" 0 100
#define speaker "tts" "Microsoft Lili" 0 100

################ Config #####################

alertall "强击" before 3 speak "tts" "T死刑"
alertall "破浪斩" before 0 speak "tts" "T死刑"
alertall "祈请" before 2 speak "tts" "AOE"

alertall "--骰子--" before 0 speak "tts" "骰子"
alertall "--骰子/AOE--" before 0 speak "tts" "骰子AOE连招"
alertall "--紫色点名--" before 2 speak "tts" "紫色点名"
alertall "--雷云--" before 2 speak "tts" "雷云"
alertall "--紫色点名/雷云--" before 2 speak "tts" "紫色点名 雷云连招"
alertall "--骰子/分摊--" before 0 speak "tts" "骰子 击退 分摊 连招"
alertall "--骰子/AOE x2--" before 2 speak "tts" "双重骰子AOE连招"
alertall "--紫色点名/雷云/AOE x2--" before 2 speak "tts" "紫色点名 雷云 AOE 连招"

################ Main ################

0 "--重置--" sync /Removing combatant 须佐之男/ window 10000 jump 0

#Phase 1 -
1 "--开始--" sync /欢庆吧！跳舞吧！/ window 10000
10 "强击" sync /须佐之男发动了“强击”/ window 2, 2

13 "--骰子--"
13 "祸泡附身" sync /须佐之男发动了“祸泡附身”/ window 2, 2
20 "--骰子 x4--"

32 "--红色点名--"
37 "八咫镜" sync /须佐之男发动了“八咫镜”/ window 2, 2
38 "断海" duration 5 sync /须佐之男正在发动“断海”/ window 2, 2
49 "强击" sync /须佐之男发动了“强击”/ window 2, 2

52 "--骰子/AOE--"
52 "祸泡附身" sync /须佐之男发动了“祸泡附身”/ window 2, 2
56 "螺旋海峡" duration 3 sync /须佐之男正在发动“螺旋海峡”/ window 2, 2
58 "--骰子 x4--"

70 "--雷云--"
70 "雷云"
72 "--红色点名--"
78 "八咫镜" sync /须佐之男发动了“八咫镜”/ window 2, 2
79 "云间放电" duration 2 sync /雷云正在发动“云间放电”/ window 2, 2
79 "断海" duration 5 sync /须佐之男正在发动“断海”/ window 2, 2
89 "强击" sync /须佐之男发动了“强击”/ window 2, 2

#Phase 2 -
94 "--Phase 2--" sync /有意思，真有意思！/ window 10000
118 "天之丛云" sync /Added new combatant 天之丛云/ window 10
118 "紫电"
121 "紫电"
124 "紫电"
127 "紫电"

200 "天之丛云" sync /Added new combatant 天之丛云/ window 80, 0
200 "紫电"
203 "紫电"
206 "紫电"
209 "紫电"

#Phase 3 -
300 "--Phase 3--" sync /哇啊啊啊！/ window 10000
304 "天之丛云"

321 "破浪斩" duration 4 sync /须佐之男正在发动“破浪斩”/ window 10

328 "--紫色点名--"
328 "--紫色点名--"
333 "闪电" sync /须佐之男发动了“闪电”/ window 2, 2
334 "--紫色点名--"
338 "闪电" sync /须佐之男发动了“闪电”/ window 2, 2
339 "--紫色点名--"
344 "闪电" sync /须佐之男发动了“闪电”/ window 2, 2
345 "--紫色点名--"
349 "闪电" sync /须佐之男发动了“闪电”/ window 2, 2

355 "祈请" duration 3 sync /须佐之男正在发动“祈请”/ window 10
359 "祈请 (1)"
361 "祈请 (2)"

367 "--雷云--"
367 "雷云)"
369 "--红色点名--"
375 "八咫镜" sync /须佐之男发动了“八咫镜”/ window 2, 2
375 "断海" duration 5 sync /须佐之男正在发动“断海”/ window 2, 2
375 "云间放电" duration 2 sync /雷云正在发动“云间放电”/ window 2, 2

385 "破浪斩" duration 4 sync /须佐之男正在发动“破浪斩”/ window 2, 2

392 "--紫色点名/雷云--"
392 "--紫色点名--"
395 "雷云)"
397 "闪电" sync /须佐之男发动了“闪电”/ window 2, 2
398 "--紫色点名--"
403 "云间放电" duration 2 sync /雷云正在发动“云间放电”/ window 2, 2
403 "闪电" sync /须佐之男发动了“闪电”/ window 2, 2
403 "--紫色点名--"
408 "闪电" sync /须佐之男发动了“闪电”/ window 2, 2
409 "--紫色点名--"
414 "闪电" sync /须佐之男发动了“闪电”/ window 2, 2

416 "祈请" duration 3 sync /须佐之男正在发动“祈请”/ window 2, 2
421 "祈请 (1)"
423 "祈请 (2)"
425 "祈请 (3)"

431 "岩户隐" sync /须佐之男发动了“岩户隐”/ window 2, 2
432 "天之岩户 x4 "
441 "岩户闭合" duration 15
443 "螺旋海峡" duration 2 sync /须佐之男正在发动“螺旋海峡”/ window 2, 2
448 "破浪斩" duration 4 sync /须佐之男正在发动“破浪斩”/ window 2, 2

459 "--Jump Robe--"
459 "--紫色点名 --"
465 "闪电" sync /须佐之男发动了“闪电”/ window 2, 2
466 "--紫色点名 --"
472 "闪电" sync /须佐之男发动了“闪电”/ window 2, 2
472 "--紫色点名 --"
478 "闪电" sync /须佐之男发动了“闪电”/ window 2, 2
479 "--紫色点名 --"
485 "闪电" sync /须佐之男发动了“闪电”/ window 2, 2

487 "祈请" duration 3 sync /须佐之男正在发动“祈请”/ window 2, 2
491 "祈请 (1)"
493 "祈请 (2)"
495 "祈请 (3)"

502 "--骰子/分摊--"
502 "祸泡附身" sync /须佐之男发动了“祸泡附身”/ window 2, 2
504 "--红色点名--"
509 "--骰子 x4--"
510 "八咫镜" sync /须佐之男发动了“八咫镜”/ window 2, 2
510 "断海" duration 5 sync /须佐之男正在发动“断海”/ window 2, 2

517 "螺旋海峡" duration 2 sync /须佐之男正在发动“螺旋海峡”/ window 2, 2
525 "破浪斩" duration 4 sync /须佐之男正在发动“破浪斩”/ window 2, 2

535 "--紫色点名 --"
541 "闪电" sync /须佐之男发动了“闪电”/ window 2, 2
541 "--紫色点名 --"
547 "闪电" sync /须佐之男发动了“闪电”/ window 2, 2
548 "--紫色点名 --"
554 "闪电" sync /须佐之男发动了“闪电”/ window 2, 2
554 "--紫色点名 --"
560 "闪电" sync /须佐之男发动了“闪电”/ window 2, 2

563 "祈请" duration 3 sync /须佐之男正在发动“祈请”/ window 2, 2
568 "祈请 (1)"
570 "祈请 (2)"
572 "祈请 (3)"

574 "--骰子/AOE x2--"
574 "祸泡附身" sync /须佐之男发动了“祸泡附身”/ window 2, 2
578 "螺旋海峡" duration 2 sync /须佐之男正在发动“螺旋海峡”/ window 2, 2
581 "--骰子 x4--"
583 "螺旋海峡" duration 2 sync /须佐之男正在发动“螺旋海峡”/ window 2, 2

593 "破浪斩" duration 4 sync /须佐之男正在发动“破浪斩”/ window 2, 2

601 "--紫色点名/雷云/AOE x2--"
601 "--紫色点名--"
604 "雷云"
605 "闪电" sync /须佐之男发动了“闪电”/ window 2, 2
606 "--紫色点名--"
607 "螺旋海峡" duration 2 sync /须佐之男正在发动“螺旋海峡”/ window 2, 2
611 "闪电" sync /须佐之男发动了“闪电”/ window 2, 2
611 "云间放电" duration 2 sync /雷云正在发动“云间放电”/ window 2, 2
612 "--紫色点名--"
616 "闪电" sync /须佐之男发动了“闪电”/ window 2, 2
617 "螺旋海峡" duration 2 sync /须佐之男正在发动“螺旋海峡”/ window 2, 2
617 "--紫色点名--"
622 "闪电" sync /须佐之男发动了“闪电”/ window 2, 2

627 "--红色点名--"
632 "八咫镜" sync /须佐之男发动了“八咫镜”/ window 2, 2
633 "云间放电" duration 2 sync /雷云正在发动“云间放电”/ window 2, 2
633 "断海" duration 5 sync /须佐之男正在发动“断海”/ window 2, 2

641 "祈请" duration 3 sync /须佐之男正在发动“祈请”/ window 2, 2
645 "祈请 (1)"
647 "祈请 (2)"
649 "祈请 (3)"

656 "岩户隐" sync /须佐之男发动了“岩户隐”/ window 100 jump 431
658 "天之岩户 x4 "
666 "岩户闭合" duration 15
```