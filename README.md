# Pedestrian intension detection based on movement

## Problem statement
Design and develop an algorithm fpr pedestrian intension detection based on motion tracking.
           Autonomous vehicles are expected to reduce drivers’ workload and  reduce the number of traffic accidents caused by human error.
One of the most significant challenges that autonomous vehicles still confront is a lack of comprehensive understanding of human behavior.

Behaviour prediction plays a pivotal role in autonomous driving  applications as it supports efficient decision making and enables risk  assessment.
The function of an autonomous vehicle to predict the future states of the  nearby pedestrians based on the current and past observations of the  surrounding environment, helps enhance their awareness of the imminent  hazards.

## System Design

Our research aims to provide autonomous vehicles with the ability to predict the intended actions of pedestrians in real time using only a video stream from a monocular RGB camera. In order to achieve this, a unified framework that can recognise and track pedestrians in traffic situations utilising a moving observer RGB camera. Furthermore, by using a real-time spatio-temporal model,  method predicts the pedestrian's intended course of action based on the sequence of observed bounding boxes.

The complete system is designed into three main steps:
* Pedestrian Detection using YOLOv3 algorithm
* Pedestrian Tracking using Deep SORT algorithm
* Pedestrian Classification using Spatio-temporal densnet.

## Implementaion Details

### Algorithm

### Speecifications
1. Pedestrian Detection using YOLOv3 algorithm
The camera captures a wide variety of obects on the road. In a few instances, we also see animals crossing the road. Considering that the only motion we are interested in in this research is that of humans, hence here humans on the road are referred to as pedestrians. These days, the main concern is how to address the problems that autonomous vehicles have with causing accidents. Accidents involving pedestrians are the most significant of these problems. Therefore, it is crucial for us to identify pedestrians on the road and classify them as follows: Those who pose a threat to the vehicle those who don't.

In the YOLOv3 algorithm for object detection:
* It is an advanced object detection algorithm having 53 convolutional layers
* This algorithm takes an image of 416X426 resolution as an input.
* This produces an output of tensor of size nx6 where n is the number of objects detected.
* Compared to other algorithms YOLOv3 is fast and accurate in terms of mean average precision and intersection over union values.


2. Pedestrian Tracking using Deep SORT algorithm
To classify the pedestrians as the above quoted classes we need to know their motion. The pedestrian tracking system accomplishes this by monitoring their mobility, or by comparing the pedestrians' locations in various frames of the video.

In the Deep SORT algorithm 
* This takes the tensor coming out from the YOLO algorithm as an input.
* Produces the tensor which contains the information of the tracking Ids.
* It is the advancement of the SORT algorithm.
* Which properly deals with the occlusion the re appearance which is not dealt with SORT
* It relies on the Kalman filter that tracks an object based on the available and previous predictions to determine the current state of the object.


3. Pedestrian Classification using Spatio-temporal densnet
There will be many pedestrians crossing a busy street; some will be on a pathway, some will be trying to cross, some will be closer to the vehicle, and some will be farther away. Here, we need categorize all of these pedestrians into two categories.

For the classification of the pedestrian into the threat posing and non-threat posing categories, the Spatio-temporal densnet is used, in this algorithm
* There are about 106 CNN layers.
* It is composed of three dense blocks separated by the transition layers.
* Each dense block is composed of four 1x1x1 and 3x3x3 convolutions.
* For training the dense net block takes an input sequence of 16 frames before the action of crossing.
* When the number of frames has not reached the minimum required for dense-net classification it uses a sliding window technique that multiplies the frames, and hence the system takes an input sequence of the frame and provides an output classification for all pedestrian’s action in every frame.



