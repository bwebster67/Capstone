
Currently I am faced with a challenge of scope. I aim for this project to achieve the following goals:

1. Have a robot that moves around a room.
2. Have said robot capture data for 3DGS.
3. Create a high-quality 3DGS reconstruction of the room.

Previously it was a stretch goal to add a secondary camera on a ~3-4ft mast atop the robot. After doing more research, it seems like this may be more of a requirement, as capturing images exclusively from floor-height will not result in a high-quality reconstruction.

This insight presents challenges with navigation. I originally intended to use a Roomba-esque navigation method, where the robot would naively navigate around the room, changing direction at collisions. This, however, is complicated by the presence of a mast, as the robot would bump the mast when attempting to drive under a table. It is nontrivial to detect a bump on the mast, and if I am going to put in time and effort to find a hardware solution to allow the robot to navigate naively, I might as well spend that time finding a software solution to allow the robot to navigate more intelligently. 

This leads to the change in focus. Instead of focusing my time on implementing 3DGS from scratch, I think the best path forward is to use an out-of-the-box 3DGS pipeline, and focus more on the data-capture and navigation aspects of the project.

I propose the following solutions:

Manually drive the robot around the room for a first-pass. Capture positional information as the robot moves, and manually or automatically place keypoints to mark out the "safezone" for the robot on a grid/floorplan. Then, have the robot do one of the following:
- (a) Follow the manually driven path exactly.
- (b) Drive from keypoint to keypoint.

Alternatively, while manually being driven around the room the robot could capture images. These images can be used to create point cloud using COLMAP that can be used to identify obstacles. Then, the robot could autonomously navigate the safezone. This would allow for more autonomous and impressive navigation, but would likely be more challenging to implement, and it would take an inconvenient amount of time to generate the COLMAP point cloud necessary to consntruct the safezone.