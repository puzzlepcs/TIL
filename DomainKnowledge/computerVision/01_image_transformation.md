# Image transformations
applications
  * matching
  * stiching
    * affine, homography
    * accurate parameters

## 1. 2D Transformations
* mapping from source to target
* Translation, Rotation, scale, similarity, affine, homography

### 1.1 Translation
moves every source by the same distance by given direction
called motion vector
optical flow
dof = 1

### 1.2 Scale
scalining factor s, s
dof = 1

### 1.3 Rotation
dof = 1

### 1.4 Similarity
Rigid transformation(translation and Rotation)
if no scale change -> Euclidean(dof = 3)
dof = 4

### 1.5 2D affine
dof = 6

additive does not work for affine transformations -> use homogeneous coordinate

### DOF degree of freedom
number of parameters


## 2 Homogeneous coordinate
### 2.1 2d Transformaitons using Homogeneous Coordinates
* DOF of transformations does not change~

### 2.2 Why homogoneous?
* Converting back from a homonedous coord.
  * homogeneous coord. maps to single Euclidean coord.

### 2.3 Points at infinity(vanishing point)
 유클리디언 평면에서 두 평행한 선은 만나지 않음
 homogeneous coord. 에서는 meet at infinity when z = 0 (setting last element to zero)
이러한 점을 소실점(vanishing point)이라고 할 수 있음.

## 3 Image Warping
* Easy to transfer a point with a fiven transformation
### 3.1 Forward warping
Easy to calculate target points. just simply move the source pixel to target pixel
따라서 가장 큰 단점으로는 Cracks&holes가 발생한다. (예를 들어 scale transformation with s = 2)

### 3.2 Inverse Warping
avoid cracks and holes (역함수를 이용하여 계산) 간단하게 말하면 dst 의 좌표를 기준으로 src의 좌표를 계산하는 것
단점으로는 Interpolation is necessary.. 정수 값이 아닌 경우 Interpolation 과정이 필수적임!
* Linear Interpolation이 많이 사용됨.

### 3.3 Recent Warping Techniques
* Seam carving
* Learning-based approach
