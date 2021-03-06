# Camera Calibration
<b>Authors:</b> Tanmay Samak and Chinmay Samak

### Objectives:
* Calibrate the camera to get its intrinsic parameters.

### Theory:
Camera calibration computes the following parameters:
* Distortion coefficients
* Camera Intrinsic Parameters
    * Focal length
    * Optical centers
* Camera Extrinsic Parameters
    * Rotation vector
    * Translation vector

Following is a brief description of the process [1].

#### Distortion Coefficients

Some cameras introduce significant distortion to images. Two major kinds of distortion are radial distortion and tangential distortion.

Radial distortion causes straight lines to appear curved. Radial distortion becomes larger the farther points are from the center of the image. The amount of radial distortion can be represented as follows:

<img src="https://render.githubusercontent.com/render/math?math=x_%7Bdistorted%7D%20%3D%20x(%201%20%2B%20k_1%20r%5E2%20%2B%20k_2%20r%5E4%20%2B%20k_3%20r%5E6)">
<img src="https://render.githubusercontent.com/render/math?math=y_%7Bdistorted%7D%20%3D%20y(%201%20%2B%20k_1%20r%5E2%20%2B%20k_2%20r%5E4%20%2B%20k_3%20r%5E6)">

Similarly, tangential distortion occurs because the image-taking lense is not aligned perfectly parallel to the imaging plane. So, some areas in the image may look nearer than expected. The amount of tangential distortion can be represented as below:

<img src="https://render.githubusercontent.com/render/math?math=x_%7Bdistorted%7D%20%3D%20x%20%2B%20%5B%202p_1xy%20%2B%20p_2(r%5E2%2B2x%5E2)%5D">
<img src="https://render.githubusercontent.com/render/math?math=y_%7Bdistorted%7D%20%3D%20y%20%2B%20%5B%20p_1(r%5E2%2B%202y%5E2)%2B%202p_2xy%5D">

In short, we need to find five parameters, known as distortion coefficients given by:

<img src="https://render.githubusercontent.com/render/math?math=dist%20%3D%20(k_1%20%5Chspace%7B10pt%7D%20k_2%20%5Chspace%7B10pt%7D%20p_1%20%5Chspace%7B10pt%7D%20p_2%20%5Chspace%7B10pt%7D%20k_3)">

#### Camera Intrinsic Parameters

Intrinsic parameters are specific to a camera. They include information like focal length <img src="https://render.githubusercontent.com/render/math?math=(f_x%2Cf_y)"> and optical centers <img src="https://render.githubusercontent.com/render/math?math=(c_x%2Cc_y)">. The focal length and optical centers can be used to create a camera matrix, which can be used to remove distortion due to the lenses of a specific camera. The camera matrix is unique to a specific camera, so once calculated, it can be reused on other images taken by the same camera. It is expressed as a <img src="https://render.githubusercontent.com/render/math?math=3%20%5Ctimes%203"> matrix:

<img src="https://render.githubusercontent.com/render/math?math=mtx%20%3D%20%5Cleft%20%5B%20%5Cbegin%7Bmatrix%7D%20f_x%20%26%200%20%26%20c_x%20%5C%5C%200%20%26%20f_y%20%26%20c_y%20%5C%5C%200%20%26%200%20%26%201%20%5Cend%7Bmatrix%7D%20%5Cright%20%5D">

#### Camera Extrinsic Parameters

Extrinsic parameters correspond to rotation and translation vectors, <img src="https://render.githubusercontent.com/render/math?math=r_%7Bvecs%7D"> and <img src="https://render.githubusercontent.com/render/math?math=t_%7Bvecs%7D"> respectively, which transform coordinates of a 3D point to a coordinate system.
