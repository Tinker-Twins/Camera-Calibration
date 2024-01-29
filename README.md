# Camera Calibration

### Objectives:
* Calibrate a camera to get its distortion coefficients, intrinsic parameters and extrinsic parameters.

### Theory:
Camera calibration computes the following parameters:
* Distortion Coefficients
* Camera Intrinsic Parameters
    * Focal length
    * Optical centers
* Camera Extrinsic Parameters
    * Rotation vector
    * Translation vector

Following is a brief description of the process[^1].

#### Distortion Coefficients
<p align="justify">
Some cameras introduce significant distortion to images. Two major kinds of distortion are radial distortion and tangential distortion.

Radial distortion causes straight lines to appear curved. Radial distortion becomes larger the farther points are from the center of the image. The amount of radial distortion can be represented as follows:
</p>

<p align="center">
$x_{distorted} = x( 1 + k_1 r^2 + k_2 r^4 + k_3 r^6)$
</p>
<p align="center">
$y_{distorted} = y( 1 + k_1 r^2 + k_2 r^4 + k_3 r^6)$
</p>

<p align="justify">
Similarly, tangential distortion occurs because the image-taking lense is not aligned perfectly parallel to the imaging plane. So, some areas in the image may look nearer than expected. The amount of tangential distortion can be represented as below:
</p>

<p align="center">
$x_{distorted} = x + [ 2p_1xy + p_2(r^2+2x^2)]$
</p>
<p align="center">
$y_{distorted} = y + [ p_1(r^2+ 2y^2)+ 2p_2xy]$
</p>

<p align="justify">
In short, we need to find five parameters, known as distortion coefficients given by:
</p>

<p align="center">
$dist = (k_1 \hspace{10pt} k_2 \hspace{10pt} p_1 \hspace{10pt} p_2 \hspace{10pt} k_3)$
</p>

#### Camera Intrinsic Parameters

<p align="justify">
   Intrinsic parameters are specific to a camera. They include information like focal length $(f_x,f_y)$ and optical center $(c_x,c_y)$. The focal length and optical center can be used to create a camera matrix, which can be used to remove distortion due to the lens of a specific camera. The camera matrix is unique to a specific camera, so once calculated, it can be reused on other images captured by the same camera. It is expressed as a $3 \times 3$ matrix:
</p>

<p align="center">
   $$mtx=\left[\begin{matrix} f_x & 0 & c_x \\ 0 & f_y & c_y \\ 0 & 0 & 1 \end{matrix}\right]$$
</p>

#### Camera Extrinsic Parameters

<p align="justify">
Extrinsic parameters correspond to rotation and translation vectors, $r_{vecs}$ and $t_{vecs}$ respectively, which transform 3D coordinates of a point in world frame to camera coordinate system.
</p>

### Implementation:

<p align="justify">
To find these parameters, we must provide some sample images of a well defined pattern (e.g. a chess board). We find some specific points of which we already know the relative positions (e.g. square corners in the chess board). We know the coordinates of these points in real world space and we know the coordinates in the image, so we can solve for the distortion coefficients. For better results, we need at least 10 test patterns.

The important input data needed for calibration of the camera is the set of 3D real world points, i.e. object points or `objpoints` and the corresponding 2D coordinates of these points in the image, i.e. image points or `imgpoints`. 

2D image points can be easily found from the image; these image points are locations where two black squares touch each other in chess boards.

However, it is not straightforward to compute the 3D real world points since the images are taken from a static camera and chess boards are placed at different locations and orientations. So we need to know (X,Y,Z) values. But for simplicity, we can say chess board was kept stationary at XY plane, (so Z=0 always) and camera was moved accordingly. This consideration helps us to find only X,Y values. Now for X,Y values, we can simply pass the points as (0,0), (1,0), (2,0), ... which denotes the location of points. In this case, the results we get will be in the scale of size of chess board square. But if we know the square size, (say 30 mm), we can pass the values as (0,0), (30,0), (60,0), ... Thus, we get the results in mm.

Once we get the `objpoints` and `imgpoints`, we can use them to calibrate the camera.
</p>

![](https://github.com/Tinker-Twins/Camera-Calibration/blob/main/Camera%20Calibration.png)

**Note:** To calibrate your own camera, you will need to print a suitable [calibration grid](https://github.com/Tinker-Twins/Camera-Calibration/tree/main/Calibration%20Grid) and use your own camera to take multiple pictures of the grid from various angles (similar to the sample [calibration images](https://github.com/Tinker-Twins/Camera-Calibration/tree/main/Calibration%20Images) in this repository). For better results, the distance between the camera and calibration grid should be approximately equal to the working distance that you intend to maintain in your application. Additionally, the resolution and focus of the camera should be maintained constant while taking pictures.

### References:
[^1]: OpenCV, \"Camera Calibration,\" [Online]. Available: https://docs.opencv.org/master/dc/dbb/tutorial_py_calibration.html
