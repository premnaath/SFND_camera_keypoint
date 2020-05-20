# SFND 2D Feature Tracking
#### Premnaath Sukumar

<img src="images/keypoints.png" width="820" height="248" />

This a performance evaluation report for Project 2 of Sensor Fusion Nanodegree program. The aim of this document is to provide an overview of all the detectors and descriptors introduced during the course and to present a brief performance evaluation report.

_NOTE:_ The evaluation is presented with a brief analysis of specific use-case of detecting a braking preceeding vehicle. The accuracy of keypoint matching is not considered.

## Types of detectors used

Listed below are the detectors evaluated in the project.

* SHITOMASI
* Harris corner detector
* FAST
* BRISK
* ORB
* AKAZE
* SIFT

Key criterias for choosing a good detector are mainly number of features detected, execution time, repeatability and robustness in handling scaling, rotation and affine transform.

## Types of descriptors used

* BRISK
* BRIEF
* ORB
* FREAK
* AKAZE
* SIFT

Key criterias for choosing a good descriptor are mainly execution time and description area of keypoints for matching.

## Discussion

All the presented detector and descriptors possess their own set of advantages and disadvantages. The use of any or their combinations mainy depend on the presented use case. Presented below is a table showing the performance evaluation of a set of these detector and descriptor combinations.

**Performance evaluation**

| Detector | Descriptor | Num keypoints | Num matches | Detector exec (ms) | Descriptor exec (ms) |
| :---: |  :---: |  :---: |  :---: |  :---: |  :---: |
|SHITOMASI| BRISK|	104.63|	75.38|	10.43|	0.98|
|SHITOMASI|	BRIEF|	104.63|	93.88|	9.46|	0.43|
|SHITOMASI|	ORB|	104.63|	90.50|	8.25|	2.87|
|SHITOMASI|	FREAK|	104.63|	76.38|	11.88|	29.72|
|SHITOMASI|	SIFT|	104.63|	91.50|	12.34|	10.39|
|					|
|HARRIS|	BRISK|	23.63|	13.75|	15.16|	0.36|
|HARRIS|	BRIEF|	23.63|	17.13|	15.37|	0.26|
|HARRIS|	ORB|	23.63|	16.50|	16.93|	2.83|
|HARRIS|	FREAK|	23.63|	14.38|	19.37|	29.12|
|HARRIS|	SIFT|	23.63|	16.25|	15.64|	9.79|
|	|				
|FAST|	BRISK|	133.63|	89.38|	1.84|	1.27|
|FAST|	BRIEF|	133.63|	109.38|	1.40|	0.53|
|FAST|	ORB|	133.63|	107.63|	1.03|	2.91|
|FAST|	FREAK|	133.63|	87.75|	2.14|	29.76|
|FAST|	SIFT|	133.63|	103.13|	2.37|	13.35|
|	|				
|BRISK|	BRISK|	249.38|	155.75|	34.83|	2.37|
|BRISK|	BRIEF|	249.38|	170.75|	30.83|	0.77|
|BRISK|	ORB|	249.38|	149.88|	30.99|	9.74|
|BRISK|	FREAK|	249.38|	154.63|	33.26|	33.18|
|BRISK|	SIFT|	249.38|	165.38|	30.57|	20.43|
||
|ORB|	BRISK|	102.13|	70.00|	6.56|	0.96|
|ORB|	BRIEF|	102.13|	52.13|	6.46|	0.41|
|ORB|	ORB|	102.13|	72.00|	5.86|	11.05|
|ORB|	FREAK|	102.13|	37.13|	5.75|	29.66|
|ORB|	SIFT|	102.13|	71.88|	5.84|	22.08|
||
|AKAZE|	BRISK|	149.88|	121.00|	45.95|	1.30|
|AKAZE|	BRIEF|	149.88|	125.75|	48.07|	0.57|
|AKAZE|	ORB|	149.88|	117.38|	45.72|	7.10|
|AKAZE|	AKAZE|	149.88|	123.88|	46.33|	37.25|
|AKAZE|	SIFT|	149.88|	126.50|	47.15|	15.40|
||
|SIFT|	BRISK|	122.50|	56.50|	66.03|	1.13|
|SIFT|	BRIEF|	122.50|	66.75|	65.34|	0.50|
|SIFT|	FREAK|	122.50|	58.00|	65.31|	30.48|
|SIFT|	SIFT|	122.50|	80.63|	67.81|	55.41|
||

**Selection**
A selection of three detector descriptor combination and a brief justification for the given use-case is presented below.

| Detector | Descriptor | Num keypoints | Num matches | Detector exec (ms) | Descriptor exec (ms) |
| :---: |  :---: |  :---: |  :---: |  :---: |  :---: |
|**FAST**|	**BRIEF**|	133.63|	109.38|	1.40|	0.53|
|**ORB**|	**SIFT**|	102.13|	71.88|	5.84|	22.08|
|**BRISK**|	**BRIEF**|	249.38|	170.75|	30.83|	0.77|

All the detectors have a capability to detect keypoints with good repeatability in the order of hundreds which brings more keypoints to describe our targets, which can be used for better description and matching.

**FAST & BRIEF:**
FAST detector method is an improvement on Harris edge detector. It possess a good capability to detect keypoint with edge features. The keypoint areas are relatively larger than the ones from Harris edge detector itself, hence convering more area deatures which is handy when it comes to matching. This method is optimized for performance and hence the complete detection is in the order of a few milliseconds.

BRIEF descriptor method describes the keypoint area with binary strings with a use of a XOR operator making it computationally very less intensive. However our only disadvantage is the detector's incapability to handle rotation. But given our use case where there is very less yaw, pitch and roll this combination can be seen a the best combination in detection and describing keypoints.

**ORB && SIFT:**
ORB detector is an enhancement of FAST detector. It uses a pyramid like structure to produce multiscale features. Thus it possess the same advantages of FAST detector and brings another dimension of information to the keypoints. The execution time in comparison with the other set of detectors is quite less, however it is marginally more time consuming than the FAST detector. The keypoint areas covers concentric circles with more area.

SIFT descriptor method possess all the advantages with the use of HOG features to represent the keypoint neighbourhood, hence the descriptor is rotational invariant. This makes the descriptor features more robust and can help in better matching. However this comes with an increase in computational time.

**BRISK && BRIEF:**
The BRISK detector is again a type of corner detection. BRISK features are invariant to scale , roatations and affine transformations. The keypoints comes with a varying neighbourhood areas. The number of detected keypoints is simply a lot, which easily makes this one of the best keypoint detectors. However this comes with an increased computation time.

BRIEF method is already described and possess the same advantages here.
