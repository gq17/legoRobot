# legoRobot
This repository is for the project of Operating System course.

Website: http://lockdown-eurecom.weebly.com/
Github:  https://github.com/gq17/legoRobot

course link: http://soc.eurecom.fr/OS/projects_fall2015.html

Communication protocol: https://gitlab.eurecom.fr/ludovic.apvrille/os_robot_project_fall2015

lego tutorial: http://doc.ubuntu-fr.org/lego_mindstorms_nxt_sur_ubuntu

--------------------------------------------------------------------
The robot characteristics

The ultrasonic sensor works within 23 centimeters. The reading would be in chaos outside this distance. So we use it detect the target. When we detect the ball, we will forward to get it.

The color semsor return the value based on the color, and the target needs to be near. This sensor is used only when we grab the ball.

The touch sensor return true or false, and you need to be careful about the direction.

The magnetic sensor will return the direction value, we donot use it in our project.

More information could be found in the tutorial.

--------------------------------------------------------------------------
Algorithms

Navigate Algothrim

The robot will continue forwarding until it meets obstacles. If the touch sensor or the ultrasonic sensor 
finds barrier, it will return and turn into another direction.

For location-predefined case

The robot knows the position of the ball, so it will go straight and turn 90 degrees, forward to get the ball.
then it will do the same actions in the other direction for the same time, and it will return.

For the arbitrary-location case

step0: Set the sensors,
step1: Turn more than 360 degrees to search the ball; if yes, to step3, if not, to step2;
step2: forward a distance while searching; if yes, to step3, if not, to step1;
step3: Adjust the angle, and approach the ball while measuring the distance, to step4;
step4: Approach the ball, grab the ball, check the color. if red, to step6 if not red, to step5;
step5: Return some distance, and turn a angle, forwarding a bit, then to step1;
step6: Hold the ball and go back. We assume the robot is in the other half field, so it will take longer, for example 10 seconds, to get back.

For the final match

Our last algorithm fails more than succeed, so we change it. This time, we keep record of our location(x, y) and the direction(0-360 degrees). Besides, we need to communicate with other robots.

First, the robot will go through all the field to search everywhere, so even if we miss some balls, we can still get others. The trajectory is like a snake in "S" shape.

We update our location and direction each step and send our moves to other robots.

Our ultrasonic sensor can detect around 23 cm, so each time wo forward 45 cm, then search 360 degrees for the ball. We check each 30 degrees, so we won't miss it. The searching continues until we detect the ball.

When we detect the ball, we know it's within 23 cm, so we forward 25 cm, grab it, and check. If it's not a ball(by color), the robot will go backwards 25 cm, and continues; if it's the ball, then we start to go back.

When grabing the ball, we calculate the distance and angle between the current location and the starting point. First we will go vertically then horizonally, to avoid running into the robots following me.

We will send our moves when we forward or turn, but we donnot sent message when we searching. Because it takes lots of time. When we find the ball, we will finish the 360 degrees, so the move is complete.

After we send our move, we will keep waiting for the acknowledgement from the next robot. We will resend the message if no responding for a certain period of time. If still no responding after resending 3 messages, we will ignore it and continue.

If we are the follower, we first receive the distance and angle from other robot, then transform them into our parameters. First we turn into that angle, then forward the corresponding distance. The following process will also send message to the next robot, and wait for the acknowledement.

The forwarding and turning process are not as accruate as we think. We notice this and make some complement. 

We make every move a module. Like forwarding 45 cm, turn 30 degrees, turn 90 degrees, then call them inside the main function, so the error is controlled. We also make compensation between them, so at last we could go back, not exactly the same place but very near, within 20 cm.


