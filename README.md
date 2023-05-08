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
[-sin($\theta$), cos($\theta$)]]. [^1]

One practical application of this algorithm for image processing when the central object in an image has a standard shape and it is necessary to align these objects as closely as possible relative to one another. Specifically, we consider the scenario where we are given images of documents, where each document has a similar rectangular shape, but where they may be rotated relative to the borders of the image.
For clarity of expression, we will use the term "aligned boundaries" to refer to cases where the document is "correctly" rotated relative to the image boundaries, "skew boundaries" to refer to cases other than these (see the following examples).

<p><img src="page_straight.jpg" width="250"><figcaption>aligned boundaries</figcaption></p>

<p><img src="page_rotated_45.jpg" width="250"><figcaption>skew boundaries</figcaption></p>

The intuitive way of converting this geometric situation into a vector problem is to represent the images by the coordinates of their corners in the xy-plane, which will be defined relative to the borders of the images as in the following image. [^2] 

<p><img src="fig1.jpg" width="250"><figcaption>aligned boundaries</figcaption></p>

We can then express the 

[^1] Throughout we will use a convention of right multiplication by rotation matrices, which will give us the transpose of the more standard left handed convention. See https://en.wikipedia.org/wiki/Rotation_matrix.
[^2] For image processing, the standard is to invert the y-axis relative to the normal Cartesian coordinates, a convention which we have adopted here.
