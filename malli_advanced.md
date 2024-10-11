```js
###deimos_expertmode

# Block Portion

block tp_to_sigil {
    # TP to sigil
    # Default zone: DragonSpire/DS_A3_Kings/DS_A3Z3_Volcano/DS_LandingZone
    mass tp XYZ(-11.618746757507324, 5880.02783203125, 100.00003051757812)
    sleep 1
    mass walkto XYZ(-15.984509468078613, 6295.8046875, 100.00006103515625)
    sleep 2
}

block use_sigil {
    # Use sigil
    mass sendkey X, 0.1
    mass waitforzonechange completion
    # Now in zone: DragonSpire/DS_A3_Kings/DS_A3Z3_Volcano/DS_Volcano1_2
}

block grab_elixir {
    # Check if non-p1 clients already have the elixir
    if except p1 windowvisible ['WorldView', 'windowHUD', 'wndElixirContainer', 'sprtElixir1'] {
        print Elixir already acquired, skipping
    } else {
        # Elixir for everyone but p1
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
    }
}

block zone_change_1 {
    # Zone change 1
    mass tp XYZ(3821.3955078125, 10698.171875, -403.51507568359375)
    sleep 1
}

block walk_into_zone_2 {
    # Walk into zone 2
    mass walkto XYZ(3775.5263671875, 11401.67578125, -277.0177307128906)
    mass waitforzonechange completion
    # Now in zone: DragonSpire/DS_A3_Kings/DS_A3Z3_Volcano/DS_Volcano_Cave3
    sleep 1
}

block tp_to_zone_3_door {
    # TP to zone 3 door
    mass tp XYZ(-1485.54296875, -10534.1298828125, -2024.521484375)
    sleep 1
}

block walk_into_zone_3 {
    # Walk into zone 3
    mass walkto XYZ(-901.6196899414062, -10509.5830078125, -1934.3839111328125)
    mass waitforzonechange completion
    # Now in zone: DragonSpire/DS_A3_Kings/DS_A3Z3_Volcano/DS_Volcano1_2
    sleep 1
}

block tp_to_elevator {
    # TP to elevator
    mass tp XYZ(-1362.7371826171875, 4742.02685546875, -5777.40673828125)
    sleep 1
}

block use_elevator {
    # Walk onto elevator and activate
    mass walkto XYZ(-1329.827392578125, 5545.05712890625, -5777.4228515625)
    sleep 2
    mass sendkey X, 0.1
    mass sendkey X, 0.1
    # Wait for elevator to reach the top (approx 24 seconds)
    sleep 24
}

block walk_out_of_elevator {
    # Walk out of elevator
    mass walkto XYZ(-1264.4229736328125, 6503.68408203125, 4734.39453125)
    sleep 2
    # Ensure we are in the correct zone after exiting the elevator
    while not inzone DragonSpire/DS_A3_Kings/DS_A3Z3_Volcano/DS_Volcano2 {
        sleep 1
    }
}

block tp_to_crystal {
    # TP near crystal
    mass tp XYZ(-902.6307983398438, 1694.65478515625, 4734.23681640625)
    sleep 1
}

block activate_crystal {
    # Walk to and activate crystal
    mass walkto XYZ(-1087.7169189453125, 1157.3712158203125, 4733.9189453125)
    sleep 1
    mass sendkey X, 0.1
    sleep 2
}

block tp_to_door {
    # TP to door
    mass tp XYZ(-1350.284423828125, 10894.7216796875, 4734.22314453125)
    sleep 1
}

block walk_into_door {
    # Walk into door
    mass walkto XYZ(-1339.4818115234375, 11675.1474609375, 4734.2080078125)
    mass waitforzonechange completion
    # Now in zone: DragonSpire/DS_A3_Kings/Interiors/DS_MalistaireLair
    sleep 1
}

block tp_to_minion_pre_boss {
    # TP to minion before boss
    mass tp XYZ(828.63134765625, 8958.0673828125, 410.4039001464844)
    sleep 2
}

block engage_minion_fight {
    # Engage minion fight
    mass walkto XYZ(1522.18310546875, 7888.48681640625, 410.4040222167969)
    mass waitforcombat completion
}

block handle_cutscenes {
    # Handle cutscenes
    sleep 10
    mass tp XYZ(-402.6929931640625, 9342.6884765625, 410.4037170410156)
    sleep 10
    mass walkto XYZ(-1635.5560302734375, 8926.9658203125, 626.3646240234375)
    sleep 20
    mass walkto XYZ(-1958.846435546875, 8581.6435546875, 626.3646850585938)
    sleep 11
}

block heal_up_if_needed {
    # Heal if needed
    mass usepotion 10 5
    sleep 1
}

block walk_into_malistaire_fight {
    # Walk into Malistaire fight
    mass walkto XYZ(-3110.9765625, 7370.09228515625, 626.3649291992188)
    mass waitforcombat completion
    sleep 15
}

block exit_dungeon {
    # Exit dungeon
    p1 clickwindow ['WorldView', 'windowHUD', 'compassAndTeleporterButtons', 'GoHomeButton']
    mass waitforzonechange completion
    # Now in zone: DragonSpire/DS_Hub_Cathedral
    sleep 2
}

block recall_back_to_dungeon {
    # Recall back to dungeon
    print pressing recall
    p1 clickwindow ['WorldView', 'windowHUD', 'compassAndTeleporterButtons', 'ResumeInstanceButton']
    mass waitforzonechange completion
    # Now in zone: DragonSpire/DS_A3_Kings/DS_A3Z3_Volcano/DS_Volcano1_2
    sleep 2
}

block tp_to_exit {
    # TP to exit
    p1 tp XYZ(243.9343719482422, -1400.333740234375, -274.8580322265625)
    sleep 2
}

block exit {
    # Exit
    print Exit
    mass tp XYZ(-101.14385986328125, 185.35235595703125, -41.03167724609375)
    mass clickwindow ['MessageBoxModalWindow', 'messageBoxBG', 'messageBoxLayout', 'AdjustmentWindow', 'Layout', 'centerButton']
    mass waitforzonechange completion
    sleep 1
    # Now at start: DragonSpire/DS_A3_Kings/DS_A3Z3_Volcano/DS_LandingZone
}

# Bot Portion

call tp_to_sigil
call use_sigil
call grab_elixir
call zone_change_1
call walk_into_zone_2
call tp_to_zone_3_door
call walk_into_zone_3
call tp_to_elevator
call use_elevator
call walk_out_of_elevator
call tp_to_crystal
call activate_crystal
call tp_to_door
call walk_into_door
call tp_to_minion_pre_boss
call engage_minion_fight
call handle_cutscenes
call heal_up_if_needed
call walk_into_malistaire_fight
call exit_dungeon
call recall_back_to_dungeon
call tp_to_exit
call exit

```
