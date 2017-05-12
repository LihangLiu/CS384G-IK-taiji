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
      
### Object Tracking in videos
In order to track the hands in the video, here we use the Camshift (Continuously Adaptive Meanshift) algorithm for tracking. 

The idea of Meanshift is simple, for a given window of the initial image, we can get a histogram of this region, which is the encoding of the object within the window. When the next frame comes, the algorithm will shift the window with the same size to minimize the distance of two corresponding histograms until convergence.

The problem of Meanshift is that it assumes that the window size stays the same. What Camshift will do is that it will first apply Meanshift to the convergence, and then update size of the window. Then the Meanshift is applied again so on so forth until the distance error is within the given threshold.

## Experiments

### Inverse Kinematics

![alt text](https://raw.githubusercontent.com/LihangLiu/IK-taiji/master/media/taiji-ik-picker.png "animator")

We based IK implementation on the course project animator as shown above. The red ball is the target and the animated character can use IK to approach the red ball. There are several features added to the animator:
1. The user can pick the red ball and move around.
2. The animated character moves all its DOFs to follow the ball by CCD algorithm.

See the [video](https://raw.githubusercontent.com/LihangLiu/IK-taiji/master/media/taiji-ik-picker.mov) for details.

### Hand Tracking in videos

![alt text](https://raw.githubusercontent.com/LihangLiu/IK-taiji/master/media/taiji-handtracking.png "hand tracking")

The implementation of the [Camshift](http://docs.opencv.org/3.1.0/db/df8/tutorial_py_meanshift.html) algoithm is provided by the [opencv](http://docs.opencv.org/3.1.0/index.html) community. We use their tool to track the left and right hands of the man in the video.

See the [video](https://raw.githubusercontent.com/LihangLiu/IK-taiji/master/media/taiji-handtracking.mov) for details.

### From videos to the animator

![alt text](https://raw.githubusercontent.com/LihangLiu/IK-taiji/master/media/taiji-ik-compare.png "")

By applying the Camshift algorithm to an online video, we can get the trajectories for the left and the right hands of the man. Then, we can enable the end-effectors of the animated character to follow the trajectories by applying the CCD algorithm.

See [the original video](https://raw.githubusercontent.com/LihangLiu/IK-taiji/master/media/taiji-original.mp4) and [the animated video](https://raw.githubusercontent.com/LihangLiu/IK-taiji/master/media/taiji-ik-handtracking.mp4) for details.

















