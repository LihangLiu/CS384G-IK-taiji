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

![alt text](https://raw.githubusercontent.com/LihangLiu/IK-taiji/master/media/fig_ccd.jpg "CCD")

The CCD decomposed the IK problem of all DOF into subrproblems by considering each DOF independently for a given time step.
As shown in the Fig above, for each given time step and for each DOF, we can apply geometry analysis to find the optimal rotation for this DOF if all other DOF stay constant. 

More concretely, denote the world position of i-th DOF, the end-effector and the target as x_i, x and t, respectively. Also, denote the transform matrix from the world coordinate to the i-th DOF coordinate as M, then:
      
      v_i = M*(x-x_i)
      v = M*(t-x_i)
      \theta = angle(v_i,v)
      d = cross(v_i,v)
where angle(,) returns the angle between two vectors and the cross(,) returns the cross product of two vectors.

From the \theta and d, we can get the needed quaternion to make up the discrepancy between current position and the optimal optimal:

      quat = (cos(\theta), d*sin(\theta))
      
     



