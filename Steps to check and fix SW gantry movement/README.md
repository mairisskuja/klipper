# Steps to check / fix Switchwire gantry movement

— In Klipper printer.cfg add:

    [force_move]
    enable_force_move: True

— Save and restart.

— Put the tool head in the middle of the gantry both on X and Z.

— In Klipper command prompt execute the following:

    SET_KINEMATIC_POSITION X=125 Z=100
    G91

— Then

    G0 X5

Note in which way it moved.

— Then

    G0 Z5

Note in which way it moved.

Compare the result with the graph in SW motor configuration guide and configure or swap motor connections properly: https://raw.githubusercontent.com/VoronDesign/Voron-Documentation/main/build/startup/images/SW-motor-configuration-guide.png

— Optional: Comment or remove [force_move] section in printer.cfg
