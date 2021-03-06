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
