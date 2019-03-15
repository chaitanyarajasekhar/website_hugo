+++
title = "sundevil-f1/10car"
subtitle = ""

date = 2019-02-25T00:00:00
lastmod = 2019-03-07T00:00:00
draft = false

# Authors. Comma separated list, e.g. `["Bob Smith", "David Jones"]`.
authors = ["admin"]

tags = ["RC-Car"]
summary = "Introducing 1/10th scale RC-car platform for multi-agent robotics research"

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["deep-learning"]` references
#   `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
# projects = ["internal-project"]

# Featured image
# To use, add an image named `featured.jpg/png` to your project's folder.
[image]
  # Caption (optional)
  caption = ""

  # Focal point (optional)
  # Options: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight
  focal_point = ""

  # Show image only in page previews?
  preview_only = false

+++

[lidar]: ./images/rplidar.jpg
[zed_camera]: ./images/zed_camera.jpg
[imu]: ./images/razor_imu.jpg
[vesc]: ./images/vesc.jpg
[tx2]: ./images/tx2.jpg


We at [Interactive Robotics Lab](https://interactive-robotics.engineering.asu.edu/) at ASU are working on RC-car based robotics platform for multi-agent research. We call it f1/10car which stands for Fast - 1/10th (scale) - Cooperative - Autonomous - Robot. This project is funded by [Intel](https://intel.com). It is based on Traxxas [Slash 4x4 platinum](https://traxxas.com/products/models/electric/6804Rslash4x4platinum) RC-car, and inspired by the [mit-racecar](https://github.com/mit-racecar) design.

In this post, I will be briefly describing the electronics hardware and software we are using in the car. For our application, we need an embedded GPU-processor which can handle computer vision and reinforcement learning networks, so we choose the Nvidia's Jetson platform's TX2 development kit which is economical when compared to their new Xavier board and can handle GPU computing.

![alt text][tx2]

For perception, we are using a [ZED](https://www.stereolabs.com/zed/) depth camera from stereo labs, which is a little older than the recent Intel's realsense [435i](https://realsense.intel.com/depth-camera/#D435i) depth camera. In terms of specifications, realsense is much smaller and has a better depth sensing in indoors due to its active IR stereo, but it has very less compatibility with cuda and getting it to work with the TX2 is a little difficult. For convenience, we moved forward with the zed camera. Since we are only using one forward camera, for localization and a 360-degree view we needed a single beam lidar. Slamtec Rplidar A3 is perfect in size and has ros compatibility within our budget. We also have a Velodyne VLP-16 lidar in the lab which I think is power hungry, heavy, and overkill for this project.

![alt text][zed_camera]

![alt text][lidar]

For state and pose estimation, we are using [razor 9DOF imu](https://www.sparkfun.com/products/14001).

![alt text][imu]

Lastly, Slash 4x4 already comes with an Electronic Speed Controller (ESC) which has some limitations like the lowest speed it can work with 5 miles/hr which is not suitable for our application. This made us to replace it with VESC which is opensource and has ros support. VESC in the picture below is based on 4.12 hardware firmware.

![alt text][vesc]


In the later posts, I will be talking more about the design with some tutorials.
