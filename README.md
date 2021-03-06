# height_camera_estimation
Estimate the height of the camera using only depth information. 

This package has been tested using:

*  Kinect1
*  Asus Xtion Pro Live 
*  ROS Indigo
*  Ubuntu 14.04

The first step is to choose 10 points from the ground or from any plane in the scene, then those points are transfomed into points cloud (x,y,z) using the intrinsic parameters of the camera (The parameters used in this package are for the Kinect1). 

Once we get our 3d points, we will use the RANSAC method (pcl::SAC_RANSAC) for plane segmentation.

Finally the height of the camera correponds to the orthogonal distance between that plane and the point (0,0,0) which is the position of the camera.


Quick Start:
===============

To use this package, clone the repository to your disc and build it:

    $ cd catkin_ws/src 
    $ git clone https://github.com/JaouadROS/heightcameraestimation
    $ cd ..
    $ catkin_make
    $ source devel/setup.bash

Open a new shell and start the Openni driver or freenect driver:

Kinect:

     $ roslaunch freenect_launch freenect.launch

Asus:

     $ roslaunch openni2_launch openni2.launch

Open a new shell and run subKinect node:

    $ rosrun height_camera_estimation camera_height 
```sh
        [ INFO] [1465204785.331114944]: Estimate the height of the camera
```

Select 10 points in the image. 

The distance between the plane, estimated from the 10 points, and the origin is computed :+1: 

    Model coefficients: 0.0210965 -0.980173 0.197017 -0.759828
    Model inliers: 10
    0    0.291351 -0.482725 1.385
    1    0.43 -0.420932 1.681
    2    0.156388 -0.383243 1.936
    3    -0.238882 -0.31497 2.327
    4    -0.467761 -0.407569 1.853
    5    -0.582672 -0.484711 1.532
    6    -0.443362 -0.510077 1.358
    7    -0.15139 -0.505036 1.363
    8    -0.0557711 -0.440154 1.657
    9    0.0214014 -0.492484 1.413
    
    The height of the camera is: -0.759828 (m)

Model coefficients are the estimated plane parameters (a.x + b.y + c.z + d = 0 form)

Model inliers correspond to the points of the plane model found. In our case it shows 10 which means that all the points that has been selected are in the plane segmentated.
