```js
# Built for 2 clients, p2 will be scaled
# Disable double click friend teleport and update p1 friend name in code
# This will farm a ton of spellements and lvl 50 gear
###deimos_expertmode

# Block Portion

block tp_to_sigil_and_use {
    while inzone DragonSpire/DS_A3_Kings/DS_A3Z3_Volcano/DS_LandingZone {
        # TP to sigil and use it
        print Going to sigil
        sleep 2
        walkto XYZ(-36.59947204589844, 6191.037109375, 100.00009155273438)
        sleep 2
        if windowvisible ['WorldView', 'NPCRangeWin', 'imgBackground'] {
            print Interacting with sigil...
            sendkey X, 0.1
            sendkey X, 0.1
            sendkey X, 0.1
            sleep 13
	    } else {
            print Sigil Failsafe Activated
            tp XYZ(-36.59947204589844, 6191.037109375, 100.00009155273438)
            sleep 1
            sendkey X, 0.1
            sendkey X, 0.1
            sendkey X, 0.1
            sleep 13
        }
    }
}

block grab_elixir {
    # Check if non-p1 clients already have the elixir
    if except p1 windowvisible ['WorldView', 'windowHUD', 'wndElixirContainer', 'sprtElixir1'] {
        print Elixir already acquired, skipping
    } else {
        # Elixir for everyone but p1
        # GRAB ELIXIR
        print GRABBING ELIXIR
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
        times 5 {
            except p1 clickwindow ['WorldView', 'NPCServicesWin', 'wndDialogMain', 'Exit']
        }
    }
}

block zone_changes_to_gurtok {
    # Zone changes to reach Gurtok
    sleep 2
    # Zone change 1
    print Zone change 1
    p1 tp XYZ(3872.218017578125, 11489.134765625, -403.51519775390625)
    p1 waitforzonechange completion
    sleep 1
    # Zone change 2
    print Zone change 2
    p1 tp XYZ(-775.92822265625, -10539.5693359375, -2404.1728515625)
    p1 waitforzonechange completion
    sleep 1
}

block use_elevator {
    # Teleport to elevator
    if p1 inzone DragonSpire/DS_A3_Kings/DS_A3Z3_Volcano/DS_Volcano1 {
        print Teleporting to elevator...
        p1 tp XYZ(-1374.6505126953125, 5575.81689453125, -5777.42236328125)
        sleep 2
        # Activate elevator
        print Activating elevator...
        mass sendkey X, 0.1
        mass sendkey X, 0.1
        mass sendkey X, 0.1
        # Wait for elevator to reach the top
        sleep 24
    } else {
        print ERROR: Not in the correct zone to use the elevator.  Attempting to fix....
        while not p1 inzone DragonSpire/DS_A3_Kings/DS_A3Z3_Volcano/DS_Volcano1 {
            print Fixing...
            if p1 inzone DragonSpire/DS_A3_Kings/DS_A3Z3_Volcano/DS_Volcano1_2 {
                call zone_changes_to_gurtok
            }
            if p1 inzone DragonSpire/DS_A3_Kings/DS_A3Z3_Volcano/DS_Volcano_Cave3 {
                p1 tp XYZ(-775.92822265625, -10539.5693359375, -2404.1728515625)
                p1 waitforzonechange completion
            }
        }
        sleep 1
        p1 tp XYZ(-1374.6505126953125, 5575.81689453125, -5777.42236328125)
        sleep 2
        # Activate elevator
        mass sendkey X, 0.1
        mass sendkey X, 0.1
        mass sendkey X, 0.1
        # Wait for elevator to reach the top
        sleep 24
    }
}

block exitElevator {
    while not p1 inzone DragonSpire/DS_A3_Kings/DS_A3Z3_Volcano/DS_Volcano2 {
    # Walk to Exit elevator
    print Exiting elevator...
    p1 walkto XYZ(-2.821014404296875, 483.7445068359375, -14.570587158203125)
    sleep 5
    }
}

block healthMana {
    if p1 inzone DragonSpire/DS_A3_Kings/DS_A3Z3_Volcano/DS_Volcano2 {
        # teleport all clients to p1
        except p1 friendtp Kevin StormHunter
        while not p2 inzone DragonSpire/DS_A3_Kings/DS_A3Z3_Volcano/DS_Volcano2 {
            sleep 1
        }
        print Healing all clients...
        sleep 1
        entitytp Health
        sleep 0.3
        entitytp Mana
        sleep 0.3
        entitytp Health
        sleep 0.3
        entitytp Mana
        sleep 0.3
        entitytp Health
        sleep 0.3
        entitytp Mana
        sleep 0.3
        entitytp Health
        sleep 0.3
        entitytp Mana
    } else {
        print Not in the correct zone to heal.
    }
}

block crystal {
    if p1 inzone DragonSpire/DS_A3_Kings/DS_A3Z3_Volcano/DS_Volcano2 {
        print Starting Crystal
        times 2 {
            # TP near crystal
            sleep 0.3
            p1 tp XYZ(-902.6307983398438, 1694.65478515625, 4734.23681640625)
            sleep 1
            # Walk to and activate crystal
            p1 walkto XYZ(-1087.7169189453125, 1157.3712158203125, 4733.9189453125)
            sleep 3
            sendkey X, 0.1
            sendkey X, 0.1
            sendkey X, 0.1
            sleep 1
        }
    } else {
        print Not in the correct zone to start the crystal.
    }
}

block tp_to_locked_door {
    print locked door
    if p1 inzone DragonSpire/DS_A3_Kings/DS_A3Z3_Volcano/DS_Volcano2 {
        # TP to door
        p1 tp XYZ(-1350.284423828125, 10894.7216796875, 4734.22314453125)
        sleep 1
    } else {
        print Not in the correct zone to teleport to the door.
    }
}

block walk_into_locked_door {
    # Walk into door
    print walk into locked door
    p1 tp XYZ(-1339.4818115234375, 11675.1474609375, 4734.2080078125)
    p1 waitforzonechange completion
    # Now in zone: DragonSpire/DS_A3_Kings/Interiors/DS_MalistaireLair
    sleep 1
}

block tp_to_minion_pre_boss {
    # TP to minion before boss
    p1 tp XYZ(828.63134765625, 8958.0673828125, 410.4039001464844)
    sleep 2
}

block engage_minion_fight {
    # Engage minion fight
    print Engaging minion fight, teleporting all clients
    while not p2 inzone DragonSpire/DS_A3_Kings/Interiors/DS_MalistaireLair {
        # tp to p1
        except p1 friendtp Kevin StormHunter
        sleep 7
        print Waiting for p2 to finish teleporting to p1
    }
    tp XYZ(1522.18310546875, 7888.48681640625, 410.4040222167969)
    waitforcombat completion
}

block handle_cutscenes {
    # Handle cutscenes
    sleep 2
    print 1st cutscene
    mass tp XYZ(-402.6929931640625, 9342.6884765625, 410.4037170410156)
    sleep 4
    print 2nd cutscene
    mass walkto XYZ(-1635.5560302734375, 8926.9658203125, 626.3646240234375)
    entitytp Malistaire-Boss-R10
    sleep 20
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
    # Exit the dungeon
    print Teleporting to spawn
    p1 clickwindow ['WorldView', 'windowHUD', 'compassAndTeleporterButtons', 'GoHomeButton']
    sleep 4
    while not p1 inzone DragonSpire/DS_Hub_Cathedral {
        print still not at spawn
        sleep 4
        p1 clickwindow ['WorldView', 'windowHUD', 'compassAndTeleporterButtons', 'GoHomeButton']
    }
    sleep 2
    while p1 inzone DragonSpire/DS_Hub_Cathedral {
        # Recall
        print pressing recall
        p1 clickwindow ['WorldView', 'windowHUD', 'compassAndTeleporterButtons', 'ResumeInstanceButton']
        sleep 4
    }
    sleep 1

    # TP to exit of dungeon
    print Teleporting to exit of dungeon
    p1 tp XYZ(243.9343719482422, -1400.333740234375, -274.8580322265625)
    sleep 2

    # Exit
    print Exiting...
    p1 tp XYZ(-101.14385986328125, 185.35235595703125, -41.03167724609375)
    p1 clickwindow ['MessageBoxModalWindow', 'messageBoxBG', 'messageBoxLayout', 'AdjustmentWindow', 'Layout', 'centerButton']
    p1 clickwindow ['MessageBoxModalWindow', 'messageBoxBG', 'messageBoxLayout', 'AdjustmentWindow', 'Layout', 'centerButton']
    p1 clickwindow ['MessageBoxModalWindow', 'messageBoxBG', 'messageBoxLayout', 'AdjustmentWindow', 'Layout', 'centerButton']
    while not p1 inzone DragonSpire/DS_A3_Kings/DS_A3Z3_Volcano/DS_LandingZone {
        sleep 1
        print Waiting for p1 to finish teleporting to dragon roost
    }
    sleep 3
    # tp to p1
    except p1 friendtp Kevin StormHunter
    sleep 6
    while not p2 inzone DragonSpire/DS_A3_Kings/DS_A3Z3_Volcano/DS_LandingZone {
        # tp to p1
        except p1 friendtp Kevin StormHunter
        sleep 6
        print Waiting for p2 to finish teleporting to p1
    }
}

# Bot Portion

call tp_to_sigil_and_use
call grab_elixir
call zone_changes_to_gurtok
call use_elevator
call exitElevator
call healthMana
call crystal
call tp_to_locked_door
call walk_into_locked_door
call tp_to_minion_pre_boss
call engage_minion_fight
call handle_cutscenes
call heal_up_if_needed
call walk_into_malistaire_fight
call exit_dungeon


```
