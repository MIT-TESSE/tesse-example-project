# TESSE
Task Execution with Semantic Segmentation Environment

This repository contains code and assets relevent to the Task Execution with Semantic Segmentation Environment in Unity3D.

## Getting Started

To setup this project in Unity on a new machine, you must do the following:
* Install Unity 2019.1+ (this project was tested using 2019.1.0f2)
* Clone the repository to the desired location
* Open the project in the Unity Editor by starting Unity, selecting 'Add' and navigating to the folder of the cloned repository
* After the project is open, load the *tesse_multiscene* scene located in *Assets/TESSE/Scenes*
* Press play in the editor, or build the executable

## Simulation Builds

Builds of the simulation environments will be provided with additional environments soon.

## Agent Control

The agent can be controlled via the [TESSE_interface]() remotely or locally via python. The agent can also be controlled via the keyboard using the following commands.

### Movement

* 'w' key - applies a force equal to *speed* to the agent's Z axis, resulting in the agent moving forward
* 's' key - applies a force equal to *-speed* to the agent's Z axis, resulting in the agent moving backward
* 'e' key - applies a force equal to *speed* to the agent's X axis, resulting in the agent moving right
* 'q' key - applies a force equal to *-speed* to the agent's X axis, resulting in the agent moving left
* 'd' key - applies a torque equal to *turn_speed* about the agent's Y axis, resulting in the agent turning right
* 'a' key - applies a torque equal to *-turn_speed* about the agent's Y axis, resulting in the agent turning left
* 'x' key - causes the agent to fully stop

### Agent Interface

* 'r' key - causes the agent to respawn
* 'left shift' + 't' keys pressed simultaneously - Toggle keyboard movement, this will enable or disable the keyboard movement. Useful if running experiments via the python interface and do not want to risk introducing spurious inputs.
*  'escape' key - exit the application
* 'left shift' + 'left control' + 'g' keys  pressed simultaneously - Toggle spawn point capture mode. When in spawn point capture mode the system will record the agent's location once a second to the spawn points csv file located in "*application_path*/Resources/*scene_name*_spawn_points.csv". This file is loaded whenever the application loads this scene and gives the agent valid spawn point locations. If this file does not exist when the scene is loaded, the system generates 20,000 spawn points randomly from the scene volume. This is not accurate and the user is expected to find valid spawn points by pressing 'r' repeatedly, or by manually entering them into the *scene_name*_spawn_points.csv file before loading the scene. Once valid spawn points are found, or if the user wishes to generate additional spawn points, they may enter spawn point capture mode and collect spawn locations by moving the agent through the scene and exiting spawn point capture mode when done collecting spawn points.

In addition to spawn point capture, there is also a mapping from objects to semantic labels located in "*application_path*/StreamingAssets/*scene_name*_segmentation_mapping.csv". This csv file contains the mapping from object labels to the RGB colors used to represent them in the semantic segmentation truth output obtained by querying the segmentation camera via the [TESSE_interface]().

## Command Line Arguments

This is a summary of all available command line arguments to the TESSE multiscene v0.2 build. 

### Communication Ports

* "--listen_port *int*" - sets the ports that the interface listens on, all listen ports operate on the UDP protocol; specifically it sets the port values to the following
  - position listen port = *int* (default=9000)
  - metadata listen port = *int* + 1 (default=9001)
  - image listen port = *int* + 2 (default=9002)
  - position update port = *int* + 3 (default=9003) *note: this is not yet implemented*
  
* "--send_port *int*" - sets the sned ports that the interface sends data back to a client on, all send ports operate on the TCP protocol; specifically it sets the port values to the following
  - position send port = *int* (default=9000)
  - metadata send port = *int* + 1 (default=9001)
  - image send port    = *int* + 2 (default=9002)
  - metadata udp streaming broadcast port = *int* + 4 (default=9004)
  
### Player Resolution

* "--set_resolution *width_int* *height_int*" - sets the screen resolution of the game to *width_int* x *height_int* (default is *width_int*=1024 and *height_int*=768)
* "--fullscreen" - if this argument is given, then the game will be fullscreen (default is windowed)

### Agent Control

* "--speed *float*" - sets the force given to the agent when pressing the 'w', 's', 'q' and 'e' keys to *float* (default=10)
* "--turn_speed *float*" - sets the torque given to the agent when pressing the 'a' and 'd' keys to *float* (default=0.5)

### Fixed Frame Rate Capture Mode
* "--capture_rate *fps_int* *execution_time_float*" - sets the game to fixed frame rate capture mode, while in this mode the game will execute an action at *fps_int* frames per second of game time, regardless of the speed the game can run on the system (ie. the computer runs the game at 15 FPS, but if *fps_int*=30 the game will run one second of game time in two seconds of wall time), all movement inputs will be executed for *execution_time_float* game seconds (ie. a move forward command will be applied continuously for *execution_time_float* game seconds and then the game will pause and wait for a new command). NOTE: All new commands will be ignored while a previously entered command is being executed. NOTE: If fixed frame rate mode is initiated via the python interface and the command line argument was not used, all keyboard actions will take place for 1 game second (ie. *execution_time_float* will be 1.0)

## Copyright
DISTRIBUTION STATEMENT A. Approved for public release. Distribution is unlimited.

This material is based upon work supported by the Under Secretary of Defense for Research 
and Engineering under Air Force Contract No. FA8702-15-D-0001. Any opinions, findings, 
conclusions or recommendations expressed in this material are those of the author(s) and 
do not necessarily reflect the views of the Under Secretary of Defense for Research and 
Engineering.

© 2019 Massachusetts Institute of Technology.

MIT Proprietary, Subject to FAR52.227-11 Patent Rights - Ownership by the contractor (May 2014)

The software/firmware is provided to you on an As-Is basis

Delivered to the U.S. Government with Unlimited Rights, as defined in DFARS Part 252.227-7013 
or 7014 (Feb 2014). Notwithstanding any copyright notice, U.S. Government rights in this work
are defined by DFARS 252.227-7013 or DFARS 252.227-7014 as detailed above. Use of this work 
other than as specifically authorized by the U.S. Government may violate any copyrights that 
exist in this work.
