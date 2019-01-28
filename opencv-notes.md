[//]: # (#opencv notes)
## sobel scharr laplacian
1. grayscale input
2. don't produce binary image

## canny
1. grayscale input
2. produce binary image

## drawContours
1. contours must be **cv::Point2i** or its alias **cv::Point**

## convertTo cvtColor
1. they may change depth, but not value, i.e. no implicit scaling or offset happens

## filter2D
1. the way to get a kernel : 
```cpp
cv::Mat laplacian_kernel = (cv::Mat_<float>(3, 3) << 1, 1, 1, 1, -8, 1, 1, 1, 1);
```

## watershed
1. the src image better have shape edges by applying laplacian
[reference](https://docs.opencv.org/master/d2/dbd/tutorial_distance_transform.html)

## approxPolyDP
1. the approximated points are lined up counter-clock wise.

## fillPoly
1. given vertices, filled the area determined by the them.

## transform warp getXXtransform
1. transform: 	given a transformation, input sparse points and output sparse points
2. warp:		given a transformation, input an image and output an image
    ==Note that if a transformation consists of translation and linear transformation, translation happens first==
3. getXX:		input 2 sets of corrosponding points, output a transformation

## SURF SIFT ... descriptor matching
1. it is important to throw away ambiguous matchs, that is, when the closest match and the second closest match is very close. Otherwise, matches will respond even if there is no targets at scene.
