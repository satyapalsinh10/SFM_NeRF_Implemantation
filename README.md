# Structure from Motion (SfM) and Neural Radiance Fields (NeRF)


This repository contains the implementation of the Structure from Motion (SfM) and Neural Radiance Fields (NeRF) projects.

## Project Overview:

The implementation of SFM and NeRF is in two phases:

**Phase 1: Structure from Motion (SfM):** This phase involves reconstructing a 3D scene and obtaining poses of the monocular camera using classical SfM techniques. The main steps include feature matching, estimating the fundamental matrix, essential matrix, camera pose, triangulation, and bundle adjustment.

**Phase 2: Neural Radiance Fields (NeRF):** This phase focuses on implementing the NeRF algorithm, allowing us to synthesize novel views of 3D scenes using deep learning. NeRF represents a scene as a continuous volumetric function and can generate photorealistic views.


## Phase 1 - Classical Structure from Motion (SfM) Pipeline : 

The classical structure from motion (SfM) pipeline is implemented in phase1 using the below steps:

* ``` Feature_matching:``` Extract SIFT features and match across images
* ``` Fundamental_matrix:``` Estimate fundamental matrix with RANSAC outlier rejection
* ``` Essential_matrix:``` Compute essential matrix from fundamental matrix
* ``` Camera_pose:``` Extract relative camera pose from the essential matrix
* ``` Triangulation:``` Linear and nonlinear triangulation of 3D points
* ``` pnp:``` Perspective-n-Point camera pose estimation
* ``` Bundle_adjustment:``` Bundle adjustment to refine camera poses and 3D points
* ``` Visiblity_matrix:``` Construct visibility matrix between cameras and points
* ``` wrapper.py:``` Main script to run the entire SfM pipeline

### Input:
The data given to us is a set of 5 images of Unity Hall at WPI, using a Samsung S22 Ultra’s primary camera at f/1.8 aperture, ISO 50 and 1/500 sec shutter speed.

<img src="Phase1/Data/IntermediateOutputImages/Imgs.png"  align="center" alt="Undistorted" width="800"/>

The data folder contains 4 matching files named matching*.txt where * refers to numbers from 1 to 5. For eg., matching3.txt contains the matching between the third image and images that come after, i.e., I3↔I4,I3↔I5. This is the reason image 5 does not have a text file.

<br>

### Initial Feature matching
<img src="Phase1/Data/IntermediateOutputImages/feature_matching.png"  align="center" alt="Undistorted" width="500"/>

<br>

### Outlier Rejectiong - RANSAC (using Fundamental matrix)
<img src="Phase1/Data/IntermediateOutputImages/matching_Inliers.jpeg"  align="center" alt="Undistorted" width="700"/>

### Cheirality check
<img src="Phase1/Data/IntermediateOutputImages/Initial triangulation plot with disambiguity, showing all four possible camera poses.jpeg"  align="center" alt="Undistorted" width="500"/>

### Triangulation(1 & 2) using Correct Camera pose
<img src="Phase1/Data/IntermediateOutputImages/Projection_of_correct_camera_pose_for 2_cams.jpeg"  align="center" alt="Undistorted" width="500"/>

### After Perspective-n-Point and Bundle Adjustment
<img src="Phase1/Data/IntermediateOutputImages/bundel_adj.png"  align="center" alt="Undistorted" width="500"/>


### Usage Guidelines:

1. To Execute the SFM pipeline run the below code:
```
python3 Wrapper.py
```

#### Outputs:

1. All Intermediate Images Output are saved in Phase1-> Data-> IntermideateOutputs

#### Input and Output Data

1. You can change the savepath loacation and Data path in Arg-Parser


## Phase 2 - NeRF:
Implementing the original NERF method [from this paper](https://arxiv.org/abs/2003.08934).

### Input:
Download the lego data for NeRF from the original author’s link [here](https://drive.google.com/drive/folders/1lrDkQanWtTznf48FCaW5lX9ToRdNDF1a)

#### Sample input

<img src="Phase2/Results/input.png"  align="center" alt="Undistorted" width="500"/>

### Neural Network used
<img src="Phase2/Results/Network.png"  align="center" alt="Undistorted" width="300"/>

### Training
<img src="Phase2/Results/loss.png"  align="center" alt="Undistorted" width="400"/>

### Result on Test set
<img src="Phase2/Results/ezgif.com-gif-maker (4).gif"  align="center" alt="Undistorted" width="500"/>

### Usage Guidelines:

#### Training:
1. Change the directory to Phase 2.
2. To train the NeRF model on GPU:

```
python3 NeRF_train.py
```
3. Output of Loss plot will be saved in Results folder.

#### Testing
1. Change the directory to Phase 2.
2. To test the model:

```
python3 NeRF_test.py
```
3. Output video will be saved in the same directory.


## References:
1. https://rbe549.github.io/fall2022/proj/p3/
2. https://arxiv.org/abs/2003.08934



