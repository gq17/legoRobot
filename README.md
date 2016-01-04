# legoRobot
This repository is for the project of Operating System course.

We are going to programming on a Lego robot.

2015.12.13 12:00
---------------------------
Now we can find the ball, and grab it;
But we may not return to the original set-forth point.

2015.12.14 15:00
----------------------------
Finish the first two tasks;
Need to build the website: http://lockdown-eurecom.weebly.com/

2016.1.4
----------------------------
for the first test

We first need to know about the sensors. The color sensor can only detect color within 3 centimeters, and the ultrasonic
sensor works within 23 centimeters. The reading is in chaos outside this distance.

Currently we have three tasks in parallel, movement task, sensor task and the communication task;
Movement task is the main task, receiving signals from the other two tasks.

algorithm

Navigate

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

To prepare for the second test, we decide to change the architechure
