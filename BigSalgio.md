```js
###deimos_expertmode

block bg_sigil {
    while inzone Celestia/CL_Hub {
        print Starting BG Sigil
        walkto XYZ(687.2861938476562, 11123.978515625, -899.699951171875)
        sleep 2

        # health Check
        while not p1 healthabove 90% {
            print p1 hp is below 90%
            loop {
                sleep 1
                if p1 healthabove 90% {
                    break
                }
            }
        }

        if p1 manabelow 6% {
            p1 entitytp Mana
            sleep 0.1
            p1 tp XYZ(687.2861938476562, 11123.978515625, -899.699951171875)
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
    while p2 inzone Celestia/CL_Hub {
        print Going to elixir
        sleep 1
        except p1 walkto XYZ(169.07508850097656, 11548.8544921875, -899.699951171875)
        except p1 tp XYZ(29.151844024658203, 12400.830078125, -1026.8914794921875)
        except p1 tp XYZ(29.151844024658203, 12400.830078125, -1026.8914794921875)
        except p1 tp XYZ(-7.791812896728516, 13870.3427734375, -1099.699951171875)
        except p1 tp XYZ(52.71698760986328, 15274.7724609375, -1049.6998291015625)
        sleep 3
        if windowvisible ['WorldView', 'NPCRangeWin', 'imgBackground'] {
            print Interacting with elixir...
            sendkey X, 0.1
            sendkey X, 0.1
            sendkey X, 0.1
            sleep 13
        } else {
            print Elixir Failsafe Activated (goto_elixir)
            if p2 inzone Celestia/CL_Hub {
                except p1 tp XYZ(52.71698760986328, 15274.7724609375, -1049.6998291015625)
            }
            sleep 1
            sendkey X, 0.1
            sendkey X, 0.1
            sendkey X, 0.1
            sleep 13
        }
    }
}

block goto_elixir_backup {
    print Elixir Failsafe2 Activated
    if p2 inzone Celestia/CL_Hub {
        except p1 tp XYZ(52.71698760986328, 15274.7724609375, -1049.6998291015625)
    }
    sleep 1
    sendkey X, 0.1
    sendkey X, 0.1
    sendkey X, 0.1
    sleep 13
}

block elixir {
    # at this point the user should be in Celestia/CL_Z12_Test_of_the_Spheres/StarRoom
    loop {
        print Loading...
        if not loading {
            sleep 1
            break
        }
    }
    sleep 2
    except p1 tp XYZ(-173.06936645507812, -3922.546630859375, 0.0)
    sleep 2
    if p2 inzone Celestia/CL_Z12_Test_of_the_Spheres/StarRoom {
        if except p1 windowvisible ['WorldView', 'windowHUD', 'wndElixirContainer', 'sprtElixir1'] {
            print Elixir already acquired, skipping
        } else {
            # Elixir for everyone but p1
            # GRAB ELIXIR
            print GRABBING ELIXIR
            until except p1 windowvisible ['WorldView', 'windowHUD', 'wndElixirContainer', 'sprtElixir1'] {
                until except p1 hasxyz XYZ(-424.8884582519531, -3270.589111328125, -9.1552734375e-05) {
                    except p1 tp XYZ(-424.8884582519531, -3270.589111328125, -9.1552734375e-05)
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
    } else {
        print Not in the correct zone, should be in Celestia/CL_Z12_Test_of_the_Spheres/StarRoom
        print Fixing...
        # fix it
    }
    sleep 1
}

block exit_TOTS {
    while not p2 inzone Celestia/CL_Hub {
        if not loading {
            sleep 1
            except p1 tp XYZ(140.42445373535156, -5175.6884765625, 0.0)
            sleep 1
            except p1 clickwindow ['MessageBoxModalWindow', 'messageBoxBG', 'messageBoxLayout', 'AdjustmentWindow', 'Layout', 'centerButton']
            except p1 clickwindow ['MessageBoxModalWindow', 'messageBoxBG', 'messageBoxLayout', 'AdjustmentWindow', 'Layout', 'centerButton']
            except p1 clickwindow ['MessageBoxModalWindow', 'messageBoxBG', 'messageBoxLayout', 'AdjustmentWindow', 'Layout', 'centerButton']
        }
        sleep 1
        print Waiting for p2 to exit star room
    }
}

block gotobg_sigil {
    if inzone Celestia/CL_Hub {
        print Going to bg sigil
        sleep 0.3
        except p1 tp XYZ(-7.791812896728516, 13870.3427734375, -1099.699951171875)
        sleep 0.3
        except p1 tp XYZ(29.151844024658203, 12400.830078125, -1026.8914794921875)
        sleep 0.3
        except p1 tp XYZ(29.151844024658203, 12400.830078125, -1026.8914794921875)
        sleep 0.2
        except p1 tp XYZ(169.07508850097656, 11548.8544921875, -899.699951171875)
    } else {
        print Not in the correct zone, should be in Celestia/CL_Hub
        if p2 inzone Celestia/CL_Z12_Test_of_the_Spheres/StarRoom {
            call exit_TOTS
        }
        if p2 inzone Celestia/CL_Z11_Temple_Of_The_Sun {
            if p1 inzone Celestia/CL_Z11_Temple_Of_The_Sun {
                # Exit Dungeon
                print In wrong place...
                tp XYZ(-26.30625343322754, -8857.177734375, 795.8013916015625)
                mass clickwindow ['MessageBoxModalWindow', 'messageBoxBG', 'messageBoxLayout', 'AdjustmentWindow', 'Layout', 'centerButton']
                mass clickwindow ['MessageBoxModalWindow', 'messageBoxBG', 'messageBoxLayout', 'AdjustmentWindow', 'Layout', 'centerButton']
                mass clickwindow ['MessageBoxModalWindow', 'messageBoxBG', 'messageBoxLayout', 'AdjustmentWindow', 'Layout', 'centerButton']
                while not inzone Celestia/CL_Hub {
                    print Waiting for zone change
                    sleep 4
                }
            } else {
                print Exiting dungeon
                except p1 tp XYZ(-26.30625343322754, -8857.177734375, 795.8013916015625)
                except p1 clickwindow ['MessageBoxModalWindow', 'messageBoxBG', 'messageBoxLayout', 'AdjustmentWindow', 'Layout', 'centerButton']
                except p1 clickwindow ['MessageBoxModalWindow', 'messageBoxBG', 'messageBoxLayout', 'AdjustmentWindow', 'Layout', 'centerButton']
                except p1 clickwindow ['MessageBoxModalWindow', 'messageBoxBG', 'messageBoxLayout', 'AdjustmentWindow', 'Layout', 'centerButton']
                while not except p1 inzone Celestia/CL_Hub {
                    print Waiting for zone change
                    sleep 4
                }
            }
        }
    }
}


block big_salgio_combat {

    sleep 2
    #use potion if needed
    if p1 manabelow 10% {
        print Using potion
        p1 usepotion
        sleep 2
    }

    sleep 1

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
        sleep 1
        print Teleporting to boss area
        tp XYZ(-44.261634826660156, 23190.470703125, -1994.5316162109375)
        sleep 1
        # Boss Location, teleport p1 and then the rest
        print Teleporting to boss location to start combat
        p1 tp XYZ(-26.361656188964844, 24880.357421875, -1944.36376953125)
        p1 waitforcombat
        except p1 tp XYZ(-26.361656188964844, 24880.357421875, -1944.36376953125)
        print All clients are in combat
        waitforcombat completion
        print BigSalgio defeated
        sleep 1

        # Exit Dungeon
        print Exiting dungeon
        while not inzone Celestia/CL_Hub {
            # Handle p1 teleport and interaction
            if not p1 loading {
                print "Teleporting p1 to hub"
                p1 tp XYZ(-26.30625343322754, -8857.177734375, 795.8013916015625)
                sleep 1
                clickwindow ['MessageBoxModalWindow', 'messageBoxBG', 'messageBoxLayout', 'AdjustmentWindow', 'Layout', 'centerButton']
                clickwindow ['MessageBoxModalWindow', 'messageBoxBG', 'messageBoxLayout', 'AdjustmentWindow', 'Layout', 'centerButton']
                clickwindow ['MessageBoxModalWindow', 'messageBoxBG', 'messageBoxLayout', 'AdjustmentWindow', 'Layout', 'centerButton']
            }

            # Handle p2 teleport and interaction
            if not p2 loading {
                print "Teleporting p2 to hub"
                p2 tp XYZ(-26.30625343322754, -8857.177734375, 795.8013916015625)
                sleep 1
                clickwindow ['MessageBoxModalWindow', 'messageBoxBG', 'messageBoxLayout', 'AdjustmentWindow', 'Layout', 'centerButton']
                clickwindow ['MessageBoxModalWindow', 'messageBoxBG', 'messageBoxLayout', 'AdjustmentWindow', 'Layout', 'centerButton']
                clickwindow ['MessageBoxModalWindow', 'messageBoxBG', 'messageBoxLayout', 'AdjustmentWindow', 'Layout', 'centerButton']
            }

            # Check if both are in the same zone
            if samezone {
                print "Both clients are in the same zone"
            }

            sleep 1
            print "Waiting for zone change..."
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
        call elixir
        call exit_TOTS
        call gotobg_sigil
        call bg_sigil
    }
}

call big_salgio_combat
```
