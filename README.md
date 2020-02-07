## Udacity self-driving Car Capstone Project : System Integration

## Project Overview

   In this project, there are three subsystems:

   1. Perception - Camera and sensors are contained in this subsystem. The Traffic Light Detection Node needs to be implemented. Two programs(tl_detector.py and tl_classifier.py) needs to be completed.

   2. Planning - The planning subsystem contains two nodes, Waypoint Loader and Waypoint Updater Node. The Waypoint Loader is provided by Udacity. When completed, the Waypoint Updater Node will provide the vehicle waypoints to follow in the simulator. The program, waypoint_updater.py, needs to be implemented.     

   3. Control - The control subsystem provides the PID control and Drive By Wire for the vehicle. The programs dbw_node.py, twist_controller.py, and pid.py needs to be implemented.  

   After the implementation of these subsystems the vehicle will be able to follow the waypoints and stop at red lights.

## Implementation Details
  The suggested order for project/program development is:

#### 1. Waypoint Updater (Partial)

  The video walkthrough for step 1 in the Capstone project is  to implement waypoint_updater.py to publish  waypoints. The end of implementation the node is subscribed to the following topics:

-   `/base_waypoints`
-   `/current_pose`

  and publishes the following topic:

-   `/final_waypoints` (publishes at 50Hz)

when executed in the simulator the vehicle attempts to the green dot waypoints but does not follow completely.

#### 2. Twist Controller

  The second part of the walkthrough is about implementing the dbw_node.py, PID.py, and twist_controller.py.
  The dbw_node.py program provides the overall control of the vehicle by publishing the topics:

  -   `/vehicle/steering_cmd` (publishes at 50Hz)
  -   `/vehicle/throttle_cmd` (publishes at 50Hz)
  -   `/vehicle/brake_cmd` (publishes at 50Hz)

  Within the dbw_node.py, twist_controller.py and PID.py is initialized. When the finished program is executed in the simulator, the vehicle follows the waypoints closely.

#### 3. Traffic Light Detection

  The third part of the walkthrough is detecting the state of the traffic light along the path and stopping at the stop line during a red light. The initial round of the implementation just uses the published state of the traffic light and based on that information to stop the vehicle. The next improvement will to implement an objection detection API to detect traffic light states (red, yellow, or green).

  The developer used rosbag and image viewer to collect traffic light images in the simulator. The images are labeled using labelimg provided by (https://github.com/tzutalin/labelImg). The pre-trained model can only detect the whole traffic light but no the states of the lights, therefore, the ssd_mobilenet_v1_coco_2018_01_28 needs to be re-trained on the local machine.

  However, the local machine has Tensorflow 2.0, which is newer version of the Tensorflow and when compiling the code retrain the model ran into many imcompatiabilities. Therefore, https://github.com/alex-lechner/Traffic-Light-Classification his trained model for my traffic light classifier.

#### 4. Waypoint Updater (Full)

  The Waypoint Updater (Full) is updated to Use /traffic_waypoint to change the waypoint target velocities before publishing to /final_waypoints. The vehicle should now stop at red traffic lights and move when they are green.
