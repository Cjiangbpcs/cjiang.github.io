# Multiple Object Tracking

Multiple Object Tracking, MOT, aims to track motion trajectories of multiple objects in a series of video frames. This task includes two aspects: object detection and data association. Specifically, for each frame, the first step is to detect interested objects, which are then used to track by data association. 

Several approaches can be used to tackle MOT task, the following method is relatively mature for production: Backend tracking optimization algorithm based on Kalman Filter and Hungaraian (Kuhn-Munkres) algorithms with SORT, DEEP-SORT as examples. 

SORT, simple online and realtime tracking, uses linear velocity model and Kalman Filter to detect object locations. Hungarian algorithm then serves as a matching optimization algorithm by searching for the maximum matching of a bipartite graph. SORT uses IOU, Intersection Over Union, distance, as weights to integrate the Hungarian algorithm for data association. SORT also adopts linear assignment implementation directly from sklearn. A threshold of 0.3 for IOU is selected in the original paper to determine whether or not two objects have the same identity. SORT assumes that objects do not move too much between any two frames. Due to occlusion issues, SORT suffers from high Identity Switches. Its open-sourced version can be found here: https://github.com/abewley/sort.


DEEP-SORT was later developed to integrate SORT's Kalman Filter and data association with appearance information, which reduced 45 percent of SORT's Identity Switches. DEEP-SORT also adds Deep Association Metric, which is mainly used to effectively differentiate two objects. The architecture can be shown as follows. Its open-sourced version, DEEP-SORT plus YOLO3, can be found here: https://github.com/nwojke/deep_sort. Another open-sourced version, DEEP-SORT plus SSD512, can be found here: https://github.com/lyp-deeplearning/deep-sort.

Note that a voting scheme is proposed to be incorporated in DEEP-SORT to identify the best detections among face, object, and Kalman Filter. 

![my image](DEEP-SORT.jpg#center)
![my image](IOU_assignment.jpg#center)
![my image](matching_cascade.jpg#center)


# References:
Wojke, Nicolai and Bewley, Alex and Paulus, Dietrich "Simple Online and Realtime Tracking with a Deep Association Metric" In ICIP 2017

Bewley, Alex and Ge, Zongyuan and Ott, Lionel and Ramos, Fabio and Upcroft, Ben "Simple Online and Realtime Tracking" In ICIP 2016.

https://blog.csdn.net/zjc910997316/article/details/83721573
