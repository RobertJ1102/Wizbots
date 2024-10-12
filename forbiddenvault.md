# less obvious version using limited tps, farms all mobs. Can skip to last if desired but all drop loot.

```js
###deimos_expertmode

block heal {
    if inzone Mirage/MR_Z01_AlkaliBarrows {
        print Healing...
        entitytp Health
        sleep 0.2
        entitytp Mana
    }
    waitforfree
}

block sigil {
    while inzone Mirage/MR_Z01_AlkaliBarrows {

        if healthbelow 70% {
            call heal
        }

        if manabelow 70% {
            call heal
        }
        waitforfree
        tp XYZ(-21801.396484375, -2532.4580078125, -2696.59912109375)
        if windowvisible ['WorldView', 'NPCRangeWin', 'imgBackground'] {
            print Interacting with sigil...
            sendkey X, 0.1
            sendkey X, 0.1
            sendkey X, 0.1
            sleep 13
	    } else {
            sleep 2
        }
    }
}

block combat {
    while not inzone Mirage/Interiors/MR_Z01_ForbiddenVault {
        sleep 3
    }
    print Starting Combat
    if manabelow 10% {
        usepotion
    }
    sleep 2
    entitytp MR_Durvish_Warrior_A_02
    tp XYZ(2833.88916015625, -4231.84326171875, 675.2103271484375)
    waitforcombat completion
    sleep 2
    tp XYZ(984.9298706054688, -4148.744140625, 675.210693359375)
    sleep 0.1
    tp XYZ(-2406.256103515625, -2629.235595703125, 381.1365051269531)
    entitytp MR_Djinn_Common_A_04
    waitforcombat completion
    sleep 2
    tp XYZ(-183.9381866455078, 380.51104736328125, -148.9249267578125)
    sleep 0.2
    tp XYZ(153.82203674316406, 299.3526306152344, -148.9249725341797)
    sleep 0.2
    tp XYZ(563.3228149414062, 604.6121215820312, -148.92520141601562)
    waitforcombat completion
}

block exit {
    print Exiting...
    sleep 1
    tp XYZ(2649.272705078125, -6421.83203125, 770.66259765625)
    while not inzone Mirage/MR_Z01_AlkaliBarrows {
        sleep 1
    }
}

call sigil
call combat
call exit

# Combat (STORM): Bunyips Rage[Epic] | Tempest[Epic] | Tempest[Epic]


```
