```js
###deimos_expertmode

# Block Portion
# Go to malistaire sigil and run bot

block tp_to_sigil_and_use {
    while inzone DragonSpire/DS_A3_Kings/DS_A3Z3_Volcano/DS_LandingZone {
        # TP to sigil and use it
        print Going to sigil
        sleep 2
        p1 walkto XYZ(-36.59947204589844, 6191.037109375, 100.00009155273438)
        sleep 2
        if windowvisible ['WorldView', 'NPCRangeWin', 'imgBackground'] {
            print Interacting with sigil...
            sendkey X, 0.1
            sendkey X, 0.1
            sendkey X, 0.1
            sleep 13
	    } else {
            print Sigil Failsafe Activated
            p1 tp XYZ(-36.59947204589844, 6191.037109375, 100.00009155273438)
            sleep 1
            sendkey X, 0.1
            sendkey X, 0.1
            sendkey X, 0.1
            sleep 13
        }
    }
}

block use_potion_before_fight {
    # Use potion before the fight if needed
    mass usepotion 5 5
}

block zone_changes_to_gurtok {
    # Zone changes to reach Gurtok
    sleep 2
    # Zone change 1
    print Zone change 1
    p1 tp XYZ(3872.218017578125, 11489.134765625, -403.51519775390625)
    mass waitforzonechange completion
    sleep 1
    # Zone change 2
    print Zone change 2
    p1 tp XYZ(-775.92822265625, -10539.5693359375, -2404.1728515625)
    mass waitforzonechange completion
    sleep 1
}

block use_elevator {
    # Teleport to elevator
    if inzone DragonSpire/DS_A3_Kings/DS_A3Z3_Volcano/DS_Volcano1 {
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
        while not inzone DragonSpire/DS_A3_Kings/DS_A3Z3_Volcano/DS_Volcano1 {
            print Fixing...
            if inzone DragonSpire/DS_A3_Kings/DS_A3Z3_Volcano/DS_Volcano1_2 {
                call zone_changes_to_gurtok
            }
            if inzone DragonSpire/DS_A3_Kings/DS_A3Z3_Volcano/DS_Volcano_Cave3 {
                p1 tp XYZ(-775.92822265625, -10539.5693359375, -2404.1728515625)
                mass waitforzonechange completion
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

block fight_gurtok {
    # Use potion if low
    mass usepotion 10 5
    sleep 2
    # Walk to Exit elevator
    print Exiting elevator...
    p1 walkto XYZ(-2.821014404296875, 483.7445068359375, -14.570587158203125)
    mass waitforzonechange completion
    sleep 1
    # Teleport to Gurtok boss
    p1 entitytp Helephant-Fire-Boss-R9
    p1 waitforcombat completion
    sleep 2
}

block exit_dungeon {
    # Exit the dungeon
    # Go to spawn
    print Teleporting to spawn
    p1 clickwindow ['WorldView', 'windowHUD', 'compassAndTeleporterButtons', 'GoHomeButton']
    sleep 4
    while not inzone DragonSpire/DS_Hub_Cathedral {
        print still not at spawn
        sleep 4
        p1 clickwindow ['WorldView', 'windowHUD', 'compassAndTeleporterButtons', 'GoHomeButton']
    }
    sleep 2
    while inzone DragonSpire/DS_Hub_Cathedral {
        # Recall
        print pressing recall
        p1 clickwindow ['WorldView', 'windowHUD', 'compassAndTeleporterButtons', 'ResumeInstanceButton']
        #mass waitforzonechange completion
        sleep 4
    }
    sleep 1

    # TP to exit of dungeon
    p1 tp XYZ(243.9343719482422, -1400.333740234375, -274.8580322265625)
    sleep 2

    # Exit
    print Exiting...
    mass tp XYZ(-101.14385986328125, 185.35235595703125, -41.03167724609375)
    mass clickwindow ['MessageBoxModalWindow', 'messageBoxBG', 'messageBoxLayout', 'AdjustmentWindow', 'Layout', 'centerButton']
    mass clickwindow ['MessageBoxModalWindow', 'messageBoxBG', 'messageBoxLayout', 'AdjustmentWindow', 'Layout', 'centerButton']
    mass clickwindow ['MessageBoxModalWindow', 'messageBoxBG', 'messageBoxLayout', 'AdjustmentWindow', 'Layout', 'centerButton']
    mass waitforzonechange completion
}

# Bot Portion
call tp_to_sigil_and_use
call use_potion_before_fight
call zone_changes_to_gurtok
call use_elevator
call fight_gurtok
call exit_dungeon

# Combat: Bunyips rage[Epic] | Tempest[Epic] | Frenzy | Tempest[Epic]
```
