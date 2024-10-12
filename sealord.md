# Grabbed from discord server

###deimos_expertmode

block loading {
until not except p1 loading {
sleep 1
}
}

block farming {
block crystal {
if inzone DragonSpire/DS_A1_Knowledge/DS_A1Z2_ConquestPlaza {
until hasxyz XYZ(-2717.58154296875, 4249.79931640625, -549.9983520507812) {
tp XYZ(-2717.58154296875, 4249.79931640625, -549.9983520507812)
}
until windowvisible ['WorldView', 'NPCRangeWin', 'imgBackground'] {
sleep 0.1
}
until not windowvisible ['WorldView', 'NPCRangeWin', 'imgBackground'] {
sendkey X, 0.1
}
}
}
call crystal
sleep 2
block combat {
until except p1 incombat {
except p1 tp XYZ(-1268.0, 4472.0, -550.0057983398438)
}
until p1 incombat {
p1 tp XYZ(-1268.0, 4472.0, -550.0057983398438)
}
while incombat {
waitforcombat completion
sleep 1
sendkey D, 0.5
sendkey A, 0.5
}
if not incombat {
entitytp Mana
sleep 0.5
entitytp Mana
sleep 3.5
}
}
call combat
}

block elixir {
block goto_hub {
if except p1 inzone DragonSpire/DS_A1_Knowledge/DS_A1Z2_ConquestPlaza {
until except p1 loading {
except p1 sendkey END, 0.1
}
call loading
sleep 1
}
}
call goto_hub
block goto_academy {
loop {
if except p1 inzone DragonSpire/DS_Hub_Cathedral {
until except p1 windowvisible ['WorldView', 'NPCRangeWin', 'imgBackground'] {
except p1 tp XYZ(893.526611328125, -912.1712036132812, -0.041259765625)
except p1 tp XYZ(1179.99072265625, -1177.7020263671875, -0.0655517578125)
sleep 2
}
until except p1 loading {
except p1 sendkey X, 0.1
}
call loading
sleep 1
} else {
exitloop
}
}
call loading
sleep 1
}
call goto_academy
block drake_work {
loop {
if except p1 inzone DragonSpire/DS_A3_Kings/DS_A3Hub_Academy {
until except p1 windowvisible ['WorldView', 'NPCRangeWin', 'imgBackground'] {
except p1 tp XYZ(-4666.75634765625, 10064.193359375, 1998.844970703125)
except p1 tp XYZ(-5235.45703125, 10115.9658203125, 1998.800048828125)
sleep 2
}
until except p1 loading {
except p1 sendkey X, 0.1
}
call loading
sleep 1
} else {
exitloop
}
}
call loading
sleep 1
until except p1 windowvisible ['WorldView', 'NPCRangeWin', 'imgBackground'] {
sleep 0.1
}
until except p1 loading {
except p1 sendkey X, 0.1
}
call loading
sleep 1
}
call drake_work
block mali_sigil {
loop {
if except p1 inzone DragonSpire/DS_A3_Kings/DS_A3Z3_Volcano/DS_LandingZone {
until except p1 windowvisible ['WorldView', 'NPCRangeWin', 'imgBackground'] {
except p1 tp XYZ(-21.02425765991211, 5608.392578125, 3.090667724609375)
except p1 tp XYZ(-17.227445602416992, 6111.54052734375, 100.00006103515625)
sleep 2
}
until not except p1 windowvisible ['WorldView', 'NPCRangeWin', 'imgBackground'] {
except p1 sendkey X, 0.1
}
sleep 18
call loading
} else {
exitloop
}
}
call loading
sleep 1
}
call mali_sigil
block grab {
until except p1 windowvisible ['WorldView', 'windowHUD', 'wndElixirContainer', 'sprtElixir1'] {
until except p1 hasxyz XYZ(46.819358825683594, 406.16522216796875, -274.8912048339844) {
except p1 tp XYZ(46.819358825683594, 406.16522216796875, -274.8912048339844)
}
until except p1 windowvisible ['WorldView', 'NPCRangeWin', 'imgBackground'] {
sleep 0.1
}
while except p1 windowvisible ['WorldView', 'NPCRangeWin', 'imgBackground'] {
except p1 sendkey X, 0.1
}
until except p1 windowvisible ['WorldView', 'NPCServicesWin', 'ControlSprite', 'optionsLayout', 'NPCServicesOptionWindow', 'OptionButton'] {
sleep 0.1
}
while except p1 windowvisible ['WorldView', 'NPCServicesWin', 'ControlSprite', 'optionsLayout', 'NPCServicesOptionWindow', 'OptionButton'] {
except p1 clickwindow ['WorldView', 'NPCServicesWin', 'ControlSprite', 'optionsLayout', 'NPCServicesOptionWindow', 'OptionButton']
}
}
}
if except p1 inzone DragonSpire/DS_A3_Kings/DS_A3Z3_Volcano/DS_Volcano1_2 {
call grab
}
times 5 {
except p1 clickwindow ['WorldView', 'NPCServicesWin', 'wndDialogMain', 'Exit']
}
}

block return {
until not except p1 windowdisabled ['WorldView', 'windowHUD', 'compassAndTeleporterButtons', 'RecallButton'] {
sleep 1
}
while not except p1 windowdisabled ['WorldView', 'windowHUD', 'compassAndTeleporterButtons', 'RecallButton'] {
clickwindow ['WorldView', 'windowHUD', 'compassAndTeleporterButtons', 'RecallButton']
}
except p1 waitforzonechange completion
sleep 1
}

#Bot
while inzone DragonSpire/DS_A1_Knowledge/DS_A1Z2_ConquestPlaza {
if except p1 windowvisible ['WorldView', 'windowHUD', 'wndElixirContainer', 'sprtElixir1'] {
call farming
} else {
print Elixir Inactive
until not except p1 windowdisabled ['WorldView', 'windowHUD', 'compassAndTeleporterButtons', 'MarkButton'] {
sleep 1
}
if not except p1 windowdisabled ['WorldView', 'windowHUD', 'compassAndTeleporterButtons', 'MarkButton'] {
except p1 clickwindow ['WorldView', 'windowHUD', 'compassAndTeleporterButtons', 'MarkButton']
}
call elixir
call return
}
}
