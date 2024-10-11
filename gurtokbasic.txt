#Gurtok farming with modified exiting

#tp to sigil
print Going to sigil
sleep 2
p1 walkto XYZ(-36.59947204589844, 6191.037109375, 100.00009155273438)
sleep 2
mass sendkey X, 0.1
mass sendkey X, 0.1
mass sendkey X, 0.1
sleep 3
mass waitforzonechange completion
mass usepotion 5 5
#tp to gurtok
sleep 2
# zonechange 1
p1 tp XYZ(3872.218017578125, 11489.134765625, -403.51519775390625)
mass waitforzonechange completion
sleep 1
# zonechange 2
p1 tp XYZ(-775.92822265625, -10539.5693359375, -2404.1728515625)
mass waitforzonechange completion
sleep 1

#elevator
p1 tp XYZ(-1374.6505126953125, 5575.81689453125, -5777.42236328125)
sleep 2
mass sendkey X, 0.1
mass sendkey X, 0.1
mass sendkey X, 0.1

#wait for elevator
sleep 24

#use potion if low
mass usepotion 10 5

sleep 4
# Walk to next room
p1 walkto XYZ(-2.821014404296875, 483.7445068359375, -14.570587158203125)
mass waitforzonechange completion
sleep 1
p1 entitytp Helephant-Fire-Boss-R9
p1 waitforcombat completion
sleep 2

# go to spawn
p1 clickwindow  ['WorldView', 'windowHUD', 'compassAndTeleporterButtons', 'GoHomeButton']
mass waitforzonechange completion
sleep 2

#recall
print pressing recal
p1 clickwindow  ['WorldView', 'windowHUD', 'compassAndTeleporterButtons', 'ResumeInstanceButton']
mass waitforzonechange completion
sleep 2

# tp to exit
p1 tp XYZ(243.9343719482422, -1400.333740234375, -274.8580322265625)
sleep 2

# Exit
print Exit
mass tp XYZ(-101.14385986328125, 185.35235595703125, -41.03167724609375)
mass clickwindow ['MessageBoxModalWindow', 'messageBoxBG', 'messageBoxLayout', 'AdjustmentWindow', 'Layout', 'centerButton']
mass clickwindow ['MessageBoxModalWindow', 'messageBoxBG', 'messageBoxLayout', 'AdjustmentWindow', 'Layout', 'centerButton']
mass clickwindow ['MessageBoxModalWindow', 'messageBoxBG', 'messageBoxLayout', 'AdjustmentWindow', 'Layout', 'centerButton']
mass waitforzonechange completion
# end script


# Combat:
# Bunyips rage[Epic] | Tempest[Epic] | Frenzy | Tempest[Epic]