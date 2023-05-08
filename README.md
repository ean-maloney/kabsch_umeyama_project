# Kabsch-Umeyama Algorithm for Image Alignment
### Ean J Maloney

## Abstract
The Kabsch-Umeyama Algorithm uses modified singular value decomposition to rotationally align n-dimensional point clouds. This project seeks to implement this alogrithm for aligning images of documents and provides examples of aplications of this technique.

## Introduction
Given two sets of points, A and B, in j dimensions and each with cardinality i, we can express A and B as matrices of the form 

[[x<sub>11</sub>, x<sub>12</sub>, ..., x<sub>1j</sub>], <br>
[x<sub>21</sub>, x<sub>22</sub>, ..., x<sub>2j</sub>], <br>
..., <br>
[x<sub>i1</sub>, x<sub>i2</sub>, ..., x<sub>ij</sub>]].

The Kabsch-Umeyama algorithm is a simple algorithm for constructing a rotation matrix R, such that the RMS distance between the respective points of A and B is minimized. Equivalently, this is the matrix R that minimizes the Frobenius norm of A - BR under the constraint that R must be a rotation matrix. In two dimensions, this is a matrix of the form

[[cos($\theta$), sin($\theta$)], <br>
[-sin($\theta$), cos($\theta$)]].[^1]

One practical application of this algorithm for image processing when the central object in an image has a standard shape and it is necessary to align these objects as closely as possible relative to one another. Specifically, we consider the scenario where we are given images of documents, where each document has a similar rectangular shape, but where they may be rotated relative to the borders of the image. For clarity of expression, we will use the term "aligned boundaries" to refer to cases where the document is "correctly" rotated relative to the image boundaries, "skew boundaries" to refer to cases other than these (see the following examples).

<img src="page_rotated_45.jpg" width="250">
*skew boundaries - image A*

<img src="page_straight.jpg" width="250">
*aligned boundaries - image B*

The intuitive way of converting this geometric situation into a vector problem is to represent the images by the coordinates of their corners in the xy-plane, which will be defined relative to the borders of the images as in the following image.[^2] 

<img src="fig1.JPG" width="250">
*images A and B translated into points with connecting edges*

We can then express each document object using the matrix form described above, where i = 4 (number of corners) and j = 2 (number of dimensions), and apply the algorithm to get the transformation matrix which rotates the document with skew boundaries into the one with aligned boundaries.

## Detailed Method
Prior to implementing the Kabsch-Umeyama Algorithm, we need to align the centroids of the two documents to the origin. This translation is obviously needed to get the best alignment, irrespective of later rotations. This is done for each object simply by subtracting the mean value over each dimension from the actual values. 

<img src="fig2.JPG" width="250">
*coordinates of A and B with aligned centroids*

Letting A and B be the matrix representations of the skew and aligned documents, respectively, the algorithm then proceeds according to the following steps.

Kabsch-Umeyama Algorithm
1. Compute the 2x2 matrix: H = A<sup>T</sup>B.
2. Fing the singular value decomposition of H, which gives U, S, V such that H = USV<sup>T</sup>.
3. Let $\hat{S}$ = I if det(V) * det(U) $\geq$ 0, else S' = diag(1, -1).
4. Return 2x2 rotation matrix: R = U $\hat{S}$ V<sup>T</sup>.[^3] 

Multiplying A by R rotates a to give the following:

<img src="fig3.JPG", width="250">
*the black rectangle is A before rotation, the red rectangle is AR, and the blue rectangle is B*


[^1]: Throughout we will use a convention of right multiplication by rotation matrices, which will give us the transpose of the more standard left handed convention. See: https://en.wikipedia.org/wiki/Rotation_matrix.
[^2]: For image processing, the standard is to invert the y-axis relative to the normal Cartesian coordinates, a convention which we have adopted here.
[^3]: Adapted from Umeyama, Shinji (1991), "Least-Squares Estimation of Transformation Parameters Between Two Point Patterns", IEEE Trans, Pattern Anal. Mach. Intell. 13 (4): 376–380, Bernal et al., "A Purely Algebraic Justification of the
Kabsch-Umeyama Algorithm", https://math.nist.gov/~JBernal/kujustf.pdf, and https://en.wikipedia.org/wiki/Kabsch_algorithm.
