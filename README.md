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

<img src="https://render.githubusercontent.com/render/math?math=x_{distorted} = x( 1 + k_1 r^2 + k_2 r^4 + k_3 r^6)">
<img src="https://render.githubusercontent.com/render/math?math=y_{distorted} = y( 1 + k_1 r^2 + k_2 r^4 + k_3 r^6)">

Similarly, tangential distortion occurs because the image-taking lense is not aligned perfectly parallel to the imaging plane. So, some areas in the image may look nearer than expected. The amount of tangential distortion can be represented as below:

<img src="https://render.githubusercontent.com/render/math?math=x_{distorted} = x + [ 2p_1xy + p_2(r^2+2x^2)]">
<img src="https://render.githubusercontent.com/render/math?math=y_{distorted} = y + [ p_1(r^2+ 2y^2)+ 2p_2xy]">

In short, we need to find five parameters, known as distortion coefficients given by:

<img src="https://render.githubusercontent.com/render/math?math=dist = (k_1 \hspace{10pt} k_2 \hspace{10pt} p_1 \hspace{10pt} p_2 \hspace{10pt} k_3)">
