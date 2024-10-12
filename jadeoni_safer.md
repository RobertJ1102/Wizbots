###deimos_expertmode
block goto_elixir {
until except p1 hasxyz XYZ(-486.0492248535156, 1294.857421875, 0.0) {
except p1 tp XYZ(261.74334716796875, 1419.468994140625, 0.0)
sleep 1
except p1 tp XYZ(-486.0492248535156, 1294.857421875, 0.0)
}
sleep 1
}

block grab_elixir {
while except p1 windowvisible ['WorldView', 'NPCRangeWin', 'imgBackground'] {
sendkey X, 0.1
}
until not except p1 windowvisible ['WorldView', 'NPCServicesWin', 'ControlSprite', 'optionsLayout', 'NPCServicesOptionWindow', 'OptionButton'] {
sleep 2
except p1 clickwindow ['WorldView', 'NPCServicesWin', 'ControlSprite', 'optionsLayout', 'NPCServicesOptionWindow', 'OptionButton']
}
}

#Bot Portion

# acquire elixir if inactive

    until except p1 windowvisible ['WorldView', 'windowHUD', 'wndElixirContainer', 'sprtElixir1'] {
    	sleep 1
    	call goto_elixir
    	call grab_elixir
    }

# farming proccess

    until not except p1 windowvisible ['WorldView', 'windowHUD', 'wndElixirContainer', 'sprtElixir1'] {
    	sleep 1

# location near obelisk

    until hasxyz XYZ(-1834.5396728515625, 307.535400390625, 100.0) {
    	tp XYZ(-1239.3154296875, 421.05780029296875, 0.0)
    	sleep 2
    	tp XYZ(-1834.5396728515625, 307.535400390625, 100.0)
    }

sleep 2

# interact with obelisk

    until not windowvisible ['WorldView', 'NPCRangeWin', 'imgBackground'] {
    	sendkey X, 0.1
    	sendkey X, 0.1
    	sleep 1
    	sendkey X, 0.1
    }

# range

    until hasxyz XYZ(-4839.11669921875, -881.8522338867188, 767.7666015625) {
    	tp XYZ(-4839.11669921875, -881.8522338867188, 767.7666015625)
    }

# combat

    until except p1 incombat {
    	except p1 entitytp Oni-Jade-MSBoss-L76
    }
    while except p1 incombat {
    	p1 entitytp Oni-Jade-MSBoss-L76
    	p1 entitytp Oni-Jade-MSBoss-L76
    	p1 entitytp Oni-Jade-MSBoss-L76
    	waitforcombat completion
    	sleep 1
    	sendkey D, 0.5
    	sendkey A, 0.5
    	entitytp Mana
    	sleep 0.5
    	entitytp Mana
    	sleep 0.5
    	entitytp Health
    	sleep 0.5
    	entitytp Health
    	sleep 0.5
    }

}
