# legoRobot
This repository is for the project of Operating System course.

Website: http://lockdown-eurecom.weebly.com/
Github:  https://github.com/gq17/legoRobot

related websites:
course link: http://soc.eurecom.fr/OS/projects_fall2015.html
Communication protocol: https://gitlab.eurecom.fr/ludovic.apvrille/os_robot_project_fall2015
lego tutorial: http://doc.ubuntu-fr.org/lego_mindstorms_nxt_sur_ubuntu

--------------------------------------------------------------------
The color sensor can only detect color within 3 centimeters:
The ultrasonic sensor works within 23 centimeters. The reading is in chaos outside this distance.

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
step6: Hold the ball and go back.

-------------------------------------------------------------
Final version--totally modulized
