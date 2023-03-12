# Final_Project_EEP520

This is the final project I completed for Software Engineering for Embedded Systems utilizing [ENVIRO](https://github.com/klavinslab/enviro/) and [ELMA](https://github.com/klavinslab/elma). Robot attributes and behavior, such as mass and velocity, may be manipulated in the multi-robot simulation environment known as Enviro. Also, to mimic a real-world situation, static items such as walls and blocks might be placed to the area.

## Overview

The project's objective is to build a robot simulation based on the leader-follower paradigm. The leader robot chooses the route that it will travel, as well as the following robots that swarm behind it. To prevent collisions with other robots, every robot is equipped with a range sensor. A train-like structure is produced by the periodic spawning of each follower robot at intervals of five seconds, with the freshly created robots following the robot that spawned before them. When force and torque are applied simultaneously, the leader robot moves in an unpredictable manner. Because they are following the parent robot, this causes the followers to likewise pursue a crazy path. When there is a significant distance between two robots, force and torque are used to propel the kid robot in the direction of its parent. A negative force is used to slow down the young robot if it approaches too closely. Each robot is notified of its parent robot's coordinates through events.

There are three primary blocks in the code:

**Coordinator:**
This is what produces new follower robots. As a coordinator shouldn't be seen in the simulation, it is specified in the project setup as an invisible process. The maximum number of robots that may be formed in the current code is 15, and each follower agent is created regularly every 5 seconds. In coordinator.h, this number can be modified. Yet as the number of robots grows, the likelihood of robot collisions increases. The robots would eventually be able to follow their parent, though.

**Leader:**
For all follower robots, the leader robot is responsible. The robots that are following it are its primary responsibility. The leader robot must slow down when it encounters barriers on the path and must also broadcast an event that notifies the first follower robot behind it of its current coordinates.

**Follower:**
The follower robot keeps an eye out for the parent robot's coordinates and also sends its own coordinates through an event to the child robot that was created using the coordinator.

![alt text](https://github.com/bhavanrajan7/Final_project/blob/main/gif/Final_project.gif)

## Key Challenges

**Physics behind the robots:**
Finding the robots' linear and angular velocities, forces, torque, friction, and mass was one of the most difficult tasks. To guarantee that the robots truly followed a looping course, it took several tries to find the optimal parameters.

**Handling Collisions:**
I also had to deal with handling collisions when additional robots are spawned, which was a significant aspect. As a result, each robot had to slow down and keep a safe distance when another robot was going to crash into them.

**Version Selection:**
I had to experiment with several versions of Enviro before settling on v1.61. When I utilized earlier versions, I frequently ran across segmentation errors. Moreover, some features like references and invisible processes were not supported in earlier versions.

## Installation

### Requirements & Steps to Run

[Docker](https://docs.docker.com/get-docker/) and [Git](https://git-scm.com/) have to be installed on the local machine before following the steps mentioned below.

1. Open the command prompt
2. git clone https://github.com/bhavanrajan7/Final_project.git
3. cd Final_project/project/
4. docker run -p80:80 -p8765:8765 -v $PWD:/source -it klavins/enviro:v1.61 bash
5. Now you must have entered the docker container
6. esm start
7. Open a web browser and enter http://localhost in the search bar
8. enviro
9. You should be able to see the simulation in the localhost

## Acknowledgments

The project used packages provided by [ENVIRO](https://github.com/klavinslab/enviro/) and [ELMA](https://github.com/klavinslab/elma).

The docker image used was provided by [Klavins](https://github.com/klavinslab).
