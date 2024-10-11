```js
###deimos_expertmode

block bg_sigil {
    while inzone Celestia/CL_Hub {
        print Starting BG Sigil
        walkto XYZ(687.2861938476562, 11123.978515625, -899.699951171875)
        sleep 2

        # health Check
        while not healthabove 90% {
            print hp is below 90%
            sleep 10
            sendkey W, 0.1
            sendkey S, 0.1
        }

        if windowvisible ['WorldView', 'NPCRangeWin', 'imgBackground'] {
            print Pressing X...
            sendkey X, 0.1
            sendkey X, 0.1
            sendkey X, 0.1
            sleep 13
        } else {
            if inzone Celestia/CL_Hub {
                print Sigil Failsafe Activated
                tp XYZ(687.2861938476562, 11123.978515625, -899.699951171875)
                sleep 1
                sendkey X, 0.1
                sendkey X, 0.1
                sendkey X, 0.1
                sleep 13
            }
        }
    }
}

block goto_elixir {
    while inzone Celestia/CL_Hub {
        print Going to elixir
        # walk
        sleep 2
        if windowvisible ['WorldView', 'NPCRangeWin', 'imgBackground'] {
            print Interacting with elixir...
            sendkey X, 0.1
            sendkey X, 0.1
            sendkey X, 0.1
            sleep 13
        } else {
            print Elixir Failsafe Activated
            # walk
            sleep 1
            sendkey X, 0.1
            sendkey X, 0.1
            sendkey X, 0.1
            sleep 13
        }
    }
}

block elixir_sigil {
}

block gotobg_sigil {

}


block big_salgio_combat {

    sleep 2
    #use potion if needed
    p1 usepotion 10 5

    sleep 2

    if not samezone {
        print clients are not in the same zone
        while p1 inzone Celestia/CL_Z11_Temple_Of_The_Sun {
            # p1 leaves
            print p1 Exiting dungeon
            p1 tp XYZ(-26.30625343322754, -8857.177734375, 795.8013916015625)
            p1 clickwindow ['MessageBoxModalWindow', 'messageBoxBG', 'messageBoxLayout', 'AdjustmentWindow', 'Layout', 'centerButton']
            p1 clickwindow ['MessageBoxModalWindow', 'messageBoxBG', 'messageBoxLayout', 'AdjustmentWindow', 'Layout', 'centerButton']
            p1 clickwindow ['MessageBoxModalWindow', 'messageBoxBG', 'messageBoxLayout', 'AdjustmentWindow', 'Layout', 'centerButton']
            sleep 4
        }

        while p2 inzone Celestia/CL_Z11_Temple_Of_The_Sun {
            # p2 leaves
            print p2 Exiting dungeon
            p2 tp XYZ(-26.30625343322754, -8857.177734375, 795.8013916015625)
            p2 clickwindow ['MessageBoxModalWindow', 'messageBoxBG', 'messageBoxLayout', 'AdjustmentWindow', 'Layout', 'centerButton']
            p2 clickwindow ['MessageBoxModalWindow', 'messageBoxBG', 'messageBoxLayout', 'AdjustmentWindow', 'Layout', 'centerButton']
            p2 clickwindow ['MessageBoxModalWindow', 'messageBoxBG', 'messageBoxLayout', 'AdjustmentWindow', 'Layout', 'centerButton']
            sleep 4
        }
    }

    while inzone Celestia/CL_Hub {
        print Re-entering dungeon
        call bg_sigil
        sleep 4
    }

    while inzone Celestia/CL_Z11_Temple_Of_The_Sun {
        print Starting Big Salgio Combat
        # Boss Area
        sleep 2
        print Teleporting to boss area
        tp XYZ(-44.261634826660156, 23190.470703125, -1994.5316162109375)
        sleep 2
        # Boss Location, teleport p1 and then the rest
        print Teleporting to boss location to start combat
        p1 tp XYZ(-26.361656188964844, 24880.357421875, -1944.36376953125)
        p1 waitforcombat
        except p1 tp XYZ(-26.361656188964844, 24880.357421875, -1944.36376953125)
        print All clients are in combat
        waitforcombat completion
        print BigSalgio defeated
        sleep 2

        # Exit Dungeon
        print Exiting dungeon
        tp XYZ(-26.30625343322754, -8857.177734375, 795.8013916015625)
        mass clickwindow ['MessageBoxModalWindow', 'messageBoxBG', 'messageBoxLayout', 'AdjustmentWindow', 'Layout', 'centerButton']
        mass clickwindow ['MessageBoxModalWindow', 'messageBoxBG', 'messageBoxLayout', 'AdjustmentWindow', 'Layout', 'centerButton']
        mass clickwindow ['MessageBoxModalWindow', 'messageBoxBG', 'messageBoxLayout', 'AdjustmentWindow', 'Layout', 'centerButton']
        while not inzone Celestia/CL_Hub {
            print Waiting for zone change
            sleep 4
        }
    }
}

# Bot Content:
# Start in Celestia spawn on sigil
while inzone Celestia/CL_Hub {
    if except p1 windowvisible ['WorldView', 'windowHUD', 'wndElixirContainer', 'sprtElixir1'] {
        call bg_sigil
    } else {
        call goto_elixir
        call elixir_sigil
        call gotobg_sigil
        call bg_sigil
    }
}

call big_salgio_combat
```
