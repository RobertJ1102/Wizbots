```js
# TP to sigil
# Default zone: DragonSpire/DS_A3_Kings/DS_A3Z3_Volcano/DS_LandingZone
mass tp XYZ(-11.618746757507324, 5880.02783203125, 100.00003051757812)
sleep 1
mass walkto XYZ(-15.984509468078613, 6295.8046875, 100.00006103515625)
sleep 2

# use sigil
mass sendkey X, 0.1
mass waitforzonechange completion
# zone is now: DragonSpire/DS_A3_Kings/DS_A3Z3_Volcano/DS_Volcano1_2

# Elixer for everyone but p1

# GRAB ELIXIR
print GRABBING ELIXIR
except p1 tp XYZ(46.81935501098633, 434.7252197265625, -274.8912048339844)
except p1 waitforpath ['WorldView', 'NPCRangeWin', 'imgBackground']
except p1 sendkey X, 0.1
sleep 0.1
except p1 sendkey X, 0.1
except p1 waitforpath ['WorldView', 'NPCServicesWin', 'ControlSprite', 'optionsLayout', 'NPCServicesOptionWindow', 'OptionButton']
except p1 clickwindow ['WorldView', 'NPCServicesWin', 'ControlSprite', 'optionsLayout', 'NPCServicesOptionWindow', 'OptionButton']
print ELIXIR ACQUIRED
sleep 5

# Zone change 1
mass tp XYZ(3821.3955078125, 10698.171875, -403.51507568359375)
sleep 1

# walk into zone 2
mass walkto XYZ(3775.5263671875, 11401.67578125, -277.0177307128906)
mass waitforzonechange completion
# zone is now: DragonSpire/DS_A3_Kings/DS_A3Z3_Volcano/DS_Volcano_Cave3
sleep 1

# Tp to zone 3 door
mass tp XYZ(-1485.54296875, -10534.1298828125, -2024.521484375)
sleep 1

# Walk into zone 3
mass walkto XYZ(-901.6196899414062, -10509.5830078125, -1934.3839111328125)
mass waitforzonechange completion
# zone: DragonSpire/DS_A3_Kings/DS_A3Z3_Volcano/DS_Volcano1_2
sleep 1

# Tp tp elevator
mass tp XYZ(-1362.7371826171875, 4742.02685546875, -5777.40673828125)
sleep 1

# walk onto elevator
mass walkto XYZ(-1329.827392578125, 5545.05712890625, -5777.4228515625)
sleep 2

# press elevator button
mass sendkey X, 0.1
mass sendkey X, 0.1

# wait for elevator
# now in zone: DragonSpire/DS_A3_Kings/DS_A3Z3_Volcano/DS_Volcano_Elevator_Up
sleep 24

# walk out of elevator
mass walkto XYZ(-1264.4229736328125, 6503.68408203125, 4734.39453125)
mass waitforzonechange completion

# this part can sometimes lag a shit ton, 4-20 seconds. we will need to check it
# we will need to use something to manage that. Maybe while in zone for the elevator one.
# after leaving elevator
# Zone: DragonSpire/DS_A3_Kings/DS_A3Z3_Volcano/DS_Volcano2

# tp Near crystal
# still zone: DragonSpire/DS_A3_Kings/DS_A3Z3_Volcano/DS_Volcano2

mass tp XYZ(-902.6307983398438, 1694.65478515625, 4734.23681640625)
sleep 1

# walk to crystal
mass walkto XYZ(-1087.7169189453125, 1157.3712158203125, 4733.9189453125)
sleep 1
mass sendkey X, 0.1
sleep 2

# tp to door
mass tp XYZ(-1350.284423828125, 10894.7216796875, 4734.22314453125)
sleep 1

# walk into door
mass walkto XYZ(-1339.4818115234375, 11675.1474609375, 4734.2080078125)
mass waitforzonechange completion
# new zone: DragonSpire/DS_A3_Kings/Interiors/DS_MalistaireLair
sleep 1

# tp to minion pre boss
mass tp XYZ(828.63134765625, 8958.0673828125, 410.4039001464844)
sleep 2

# walk into minion fight
mass walkto XYZ(1522.18310546875, 7888.48681640625, 410.4040222167969)
mass waitforcombat completion

# Cut scenes
sleep 10
mass tp XYZ(-402.6929931640625, 9342.6884765625, 410.4037170410156)
sleep 10
mass walkto XYZ(-1635.5560302734375, 8926.9658203125, 626.3646240234375)
sleep 20
mass walkto XYZ(-1958.846435546875, 8581.6435546875, 626.3646850585938)
sleep 11

# heal up if needed
mass usepotion 10 5
sleep 1

# walk into malistaire fight
mass walkto XYZ(-3110.9765625, 7370.09228515625, 626.3649291992188)
mass waitforcombat completion
sleep 15

# Walk  out of dungeon

# to current zone door:
mass tp XYZ(-156.0725860595703, -1761.805419921875, 0.029296875)
mass waitforzonechange completion

#tp near elevator
mass tp XYZ(-1347.205322265625, 6297.431640625, 4734.39453125)
sleep 1
mass walkto XYZ(-1333.9017333984375, 5616.208984375, 4734.3955078125)
sleep 1

# use elevator
mass sendkey X, 0.1
mass sendkey X, 0.1
sleep 2

#wait for elevator
sleep 24

#walk off elevator
mass walkto XYZ(-25.114501953125, -399.935546875, -14.570526123046875)
mass waitforzonechange completion
sleep 1

# to second zone
mass tp XYZ(-7590.79345703125, 13105.228515625, -4993.42724609375)
mass waitforzonechange completion
sleep 1

# to first zone
mass tp XYZ(356.1940002441406, -13.57496166229248, -13.29583740234375)
mass waitforzonechange completion
sleep 1

# tp to exit
mass tp XYZ(243.9343719482422, -1400.333740234375, -274.8580322265625)
sleep 2

# Exit
print Exit
mass tp XYZ(-101.14385986328125, 185.35235595703125, -41.03167724609375)
mass clickwindow ['MessageBoxModalWindow', 'messageBoxBG', 'messageBoxLayout', 'AdjustmentWindow', 'Layout', 'centerButton']
mass clickwindow ['MessageBoxModalWindow', 'messageBoxBG', 'messageBoxLayout', 'AdjustmentWindow', 'Layout', 'centerButton']
mass clickwindow ['MessageBoxModalWindow', 'messageBoxBG', 'messageBoxLayout', 'AdjustmentWindow', 'Layout', 'centerButton']
mass waitforzonechange completion
sleep 1
# zone is now the start: DragonSpire/DS_A3_Kings/DS_A3Z3_Volcano/DS_LandingZone
# end script
```

```js
# Combat

### p1
any<aura & out_damage>  | Storm Lord[epic] | Tempest[epic] | Tempest[epic]

### p2
Feint @ boss | Feint @ boss | any<aoe>[strong]
```
