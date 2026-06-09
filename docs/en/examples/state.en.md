![](https://i.waifu.pics/KjyZfjn.jpg)

# Examples of Command Code Sections

```ini
-----------------------------------
{($SHIP_MODE == 1) && ($SHIP_PUSHBACK == 0)}
Condition
-----------------------------------
#WAIT(90)
Wait for 90 seconds
-----------------------------------
#IAS(240)
Speed 240 kt. Airspeed or ground speed can both be used. If the value in parentheses is 0, the speed restriction is removed.
-----------------------------------
#HANDOFF(APP)
Hand off to approach
-----------------------------------
#SUBCODE(@98,TAXI_REQ_LOOP,1,60)
Jump back to the TAXI_REQ_LOOP parameter after 60 seconds
-----------------------------------
#ROUTECHANGETABLE(GP_AP34R_HVISUAL)
Change the route. This must be used together with route.ini.
-----------------------------------
#STATE(TAXI_REQ_INIT_DEPARTURE)
Allows the aircraft to jump to another control parameter, or state
-----------------------------------
#EXECUTE(GOAROUND)
Execute go-around
```

```text
<TAXI_RUNWAY>
<TAXI_STAND_BY>
Pop-up options: taxi clearance and taxi standby.
```
