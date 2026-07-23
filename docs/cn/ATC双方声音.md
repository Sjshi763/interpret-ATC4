# ATC双方声音
`ATC4/PORT/机场改档机场/改档文件夹分区/改档文件夹(stage)/atcvoice.ini` 是有其集体的配音选择文件,他们看起来会像这样

```ini
[GGT8150]
ship=SHIP_TKS

[GGT8447]
ship=SHIP_TKS

[GIA]
ship=SHIP_JAY

[PAL]
ship=SHIP_JAY

[SIA]
ship=SHIP_JAY

[THA]
ship=SHIP_JAY

[BASEVOICE]
ship=SHIP_KNK,SHIP_KMT,SHIP_UNK,SHIP_KTK,SHIP_YKY,SHIP_KWJ
DEL=ATC_YZM
GND=ATC_IMN
TWR=ATC_MNT
APP=ATC_OKZ
DEP=ATC_KBM
control=ATC_MNT
```

## 在机体

```ini
[GGT8447]
ship=SHIP_TKS

[GIA]
ship=SHIP_JAY
```
他们会像这样
假设`ATC4\PORT\RJTT2\VOICE\ATC`路径有`SHIP_KNN`文件夹和配音文件那么它应该看起来像这样
```ini
[航班号]
ship=SHIP_KNN
```
## 在ATC
```ini
[BASEVOICE]
ship=SHIP_KNK,SHIP_KMT,SHIP_UNK,SHIP_KTK,SHIP_YKY,SHIP_KWJ
DEL=ATC_YZM
GND=ATC_IMN
TWR=ATC_MNT
APP=ATC_OKZ
DEP=ATC_KBM
control=ATC_MNT
```
在`ATC4\PORT\RJTT2\VOICE\ATC`路径有`ATC_KNN`文件夹和配音文件那么它应该看起来像这样
```ini
[BASEVOICE]
ship=SHIP_KNN
DEL=ATC_KNN
; 剩下的省略
```

## 其他
- 配音文件夹的名字是`SHIP_XXX`和`ATC_XXX`，其中`XXX`是你想要的名字，注意不要使用中文和空格，建议使用英文和数字
- 配音文件夹的文件结构应该与其他的配音文件夹相同
- 配音文件应该是`wav`、`单声道`、`Signed 16-bit PCM`、`22050Hz`，否则可能会出现无法播放的情况（可以试用`ffmpeg`这个你电脑大概率有的软件来处理，因为大部分视频或音乐软件需要，会一起安装，只是你找不到，你可以搜`everything`使用教程来找到）