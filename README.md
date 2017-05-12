# From Video to Animator
Lihang Liu
University of Texas at Austin

## Abstract. 
In this project, we try to combine hand tracking with [Inverse Kinematics](https://en.wikipedia.org/wiki/Inverse_kinematics).
Firstly, the inverse kinematics will be implemented to enable the animated
character to move according to the changing end-effectors. Secondly, we can extract
the hands trajectory of a human in a video using [Camshift algorithm](https://fr.wikipedia.org/wiki/Camshift). 
Finally, we can enable the end-effectors of the animator to follow the movement of the hands of the human.

## Methodology

### Inverse Kinematics
There are several algorithms to solve the IK problem, like the Jacobian algorithm and Cyclic Coordinate Descent (CCD). 
Here we use CCD as our solver for the IK problem.

![alt text](https://github.com/adam-p/markdown-here/raw/master/src/common/images/icon48.png "Logo Title Text 1")



