# ATC Voices (Aircraft and ATC)
`ATC4/PORT/Airport Modification/Airport Folders/Airport Folder(stage)/atcvoice.ini` is the voice selection configuration file, and they look like this:

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

## For Aircraft

```ini
[GGT8447]
ship=SHIP_TKS

[GIA]
ship=SHIP_JAY
```
They will look like this. Assuming there is a `SHIP_KNN` folder and voice files in the `ATC4\PORT\RJTT2\VOICE\ATC` path, it should look like this:
```ini
[FlightNumber]
ship=SHIP_KNN
```

## For ATC
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
If there is an `ATC_KNN` folder and voice files in the `ATC4\PORT\RJTT2\VOICE\ATC` path, it should look like this:
```ini
[BASEVOICE]
ship=SHIP_KNN
DEL=ATC_KNN
; The rest is omitted
```

## Other Notes
- Voice folder names are `SHIP_XXX` and `ATC_XXX`, where `XXX` is your desired name. Note that Chinese characters and spaces should not be used; it is recommended to use English and numbers.
- The file structure of the voice folder should be the same as other voice folders.
- Voice files should be `wav`, `mono`, `Signed 16-bit PCM`, `22050Hz`, otherwise they may not play properly (you can use `ffmpeg`, which is likely installed on your computer as it's needed by most video or music software - you can use the `everything` search tool to find it).