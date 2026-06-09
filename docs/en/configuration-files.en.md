![](https://i.waifu.pics/3DpVCc3.jpg)

# Configuration Files

## State

### Placement

State files are usually inside `Game root\PORT\RJTT2\SCENARIO\`. If you make changes, we recommend placing them in your own stage folder, such as `Game root\PORT\RJCC\SCENARIO\0015_Snoooww Stage`. Otherwise, you may break the official stages.

### Content

The following is an example of taxi clearance requests for departure aircraft, arrival aircraft, and towing aircraft, with explanations.

```Ini
; 出発と到着とトーイング機のタキシング許可リクエスト【0025S】 
[TAXI_REQ_INIT] 
{($SHIP_MODE == 1) && ($SHIP_PUSHBACK == 0)} "SHIP:@LGND, @SCSN, @NSPT, request_taxi, information 
@XATS.:東京グランド管制、こちらは@SCSN。@NSPT に駐機しています。走行許可を要請します。空港情報は@XATS
を取得しています。" 
{($SHIP_MODE == 1) && ($SHIP_PUSHBACK == 1)} #STATE(TAXI_REQ_INIT_DEPARTURE) 
{$SHIP_MODE == 2} "SHIP:@LGND, @SCSN, @NHPT, @NSPT.:東京グランド管制、こちらは@SCSN です。@NHPT にい
ます。@NSPT に入ります。" 
{($SHIP_MODE  ==  3)  &&  ($SHIP_PUSHBACK  ==  0)}  "SHIP:@ZEVE[gh,23]  GND,  @SCSN,  @NSPT,  to  @RRWY, 
request_towing.:*グランド、こちら@SCSN、@NSPT です。@RRWY へトーイング許可願います。" 
{($SHIP_MODE == 3) && ($SHIP_PUSHBACK == 1)} "SHIP:@ZEVE[gh,5] GND, @SCSN, pushback complete, request 
towing.:*グランド、こちら@SCSN、プッシュバック完了しました。トーイング許可願います。" 
{$SHIP_MODE == 2}  #STATE(TOW_REQ_LOOP) 
{$SHIP_MODE == 3}  #STATE(TOW_REQ_LOOP) 
;
```

```Ini
; 出発と到着とトーイング機のタキシング指示 
[TAXI_REQ_LOOP:Waiting to taxi:走行許可できます] 
{$USERFLAG06 == 0} #SUBCODE(@98,TAXI_REQ_LOOP,1,60) 
{$USERFLAG05 == 0} #SUBCODE(@98,TAXI_REQ_LOOP,3,4) 
{$SHIP_MODE == 1} <TAXI_RUNWAY> 
{$SHIP_MODE == 2} <TAXI_SPOT> 
<TAXI_STAND_BY> 
```

This is a configuration file following INI syntax.

```Ini
; 出発と到着とトーイング機のタキシング許可リクエスト【0025S】 
```

The `;` in the first line marks that line as a comment. Commented parts are not loaded into the game, so you can write almost anything there. However, if the comment is too random, you may not be able to find the section you need later. My suggestion is to write something related, such as:

```Ini
; Departure aircraft clearance
```

This helps avoid losing track of where a problem is. Most file editors, including Windows Notepad, can find the section you want by searching for this text.

```Ini
[TAXI_REQ_INIT] 
```

The second line is a configuration entry like this. It is the name of the control parameter.

> Add a suitable image here later.

This controls some aircraft states. For example, the `TAXI_REQ_INIT` above displays `Pushing back` in English and `プッシュバック中` in Japanese.

If you want to modify the parameters loaded by a state file, see the control parameter command code [here](/en/examples/state.en.md).

## Command

### Placement

Command files are placed in the same location as state files. By default, they are in `ATC4\PORT\RJTT2\SCENARIO`.

If you make changes, we still strongly recommend putting them in your own stage folder, such as `ATC4\PORT\RJCC\SCENARIO\0015_Snoooww Stage`. Otherwise, you may break the official stages.

### Content

```Ini
; 出発機の走行許可 
<TAXI_RUNWAY:*Start taxiing:走行許可> 
  #EXECUTE(MAP_TAXI_SELECT) 
  {$USERFLAG06= 1} #STATE(SNA_PUSHBACK_END) 
  #STATE(TAXI_REQ_LOOP) 
  #STATE(%TAXI_RUNWAY) 
```

Like state files, command files control what is executed after the player selects an option. The syntax is also the same as state files. For example, if the state file has `<TAXI_RUNWAY>`, the command file must have `<TAXI_RUNWAY:English:Japanese>`. Otherwise, the game will crash immediately after the player clicks that button.

## Application

```Ini
;  出発と到着とトーイング機のタキシング許可リクエスト【0025S】 
[TAXI_REQ_INIT] 
{($SHIP_MODE == 1) && ($SHIP_PUSHBACK == 0)} "SHIP:@LGND, @SCSN, @NSPT, request_taxi, information 
@XATS.:東京グランド管制、こちらは@SCSN。@NSPT に駐機しています。走行許可を要請します。空港情報は
@XATS を取得しています。" 
{($SHIP_MODE == 1) && ($SHIP_PUSHBACK == 1)} #STATE(TAXI_REQ_INIT_DEPARTURE) 
{$SHIP_MODE == 2} "SHIP:@LGND, @SCSN, @NHPT, @NSPT.:東京グランド管制、こちらは@SCSN です。
@NHPT にいます。@NSPT に入ります。" 
{($SHIP_MODE == 3) && ($SHIP_PUSHBACK == 0)} "SHIP:@ZEVE[gh,23] GND, @SCSN, @NSPT, to @RRWY, 
request_towing.:*グランド、こちら@SCSN、@NSPT です。@RRWY  へトーイング許可願います。" 
{($SHIP_MODE == 3) && ($SHIP_PUSHBACK == 1)} "SHIP:@ZEVE[gh,5] GND, @SCSN, pushback complete, request 
towing.:*グランド、こちら@SCSN、プッシュバック完了しました。トーイング許可願います。" 
{$SHIP_MODE == 2}    #STATE(TOW_REQ_LOOP) 
{$SHIP_MODE == 3}    #STATE(TOW_REQ_LOOP) 
;
```

```Ini
;  出発と到着とトーイング機のタキシング指示 
[TAXI_REQ_INIT_DEPARTURE] 
#MESSAGE(Preparation_for_taxiing:走行準備中) 
#WAIT(90) 
"SHIP:@LGND, @SCSN, request_taxi.:東京グランド管制、こちらは@SCSN です。地上走行許可を要請します。" 
#STATE(TAXI_REQ_LOOP) 
;
```

```Ini
;  出発と到着とトーイング機のタキシング指示 
[TAXI_REQ_LOOP:Waiting to taxi:走行許可できます] 
{$USERFLAG06 == 0} #SUBCODE(@98,TAXI_REQ_LOOP,1,60) 
{$USERFLAG05 == 0} #SUBCODE(@98,TAXI_REQ_LOOP,3,4) 
{$SHIP_MODE == 1} <TAXI_RUNWAY> 
{$SHIP_MODE == 2} <TAXI_SPOT> 
<TAXI_STAND_BY>
```

After pushback is complete, when the aircraft enters the `TAXI_REQ_INIT` state, send it into the newly created `TAXI_REQ_INIT_DEPARTURE` state. After executing `#WAIT(90)`, it transfers to `TAXI_REQ_LOOP` and requests taxi.

`{$USERFLAG06 == 0} #SUBCODE(@98,TAXI_REQ_LOOP,1,60)` prevents the crew from repeatedly executing the 90-second wait code if the player does not respond for a long time.

For other applications, see [Command](/en/examples/command.en.md).
