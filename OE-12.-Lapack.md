## Insert a subset of BLAS and Lapack back to OpenCV

* Author: Vlad Sovrasov, Vadim Pisarevsky
* Link: [The feature request](https://github.com/opencv/opencv/issues/11007)
* Status: **Draft**
* Platforms: **All**
* Complexity: a few man-weeks

## Introduction and Rationale

Implementation of some linear algebra operations, mostly notably SVD and Eigen decomposition, are much slower in OpenCV than in Lapack in the case of large matrices (whereas on 3x3 to ~6x6 matrices OpenCV is faster). It makes things like camera calibration and other SVD-based algorithms quite slow. Now it's possible to build OpenCV with external Lapack and then it will be used, but:

* it's not done by default
* some Lapack implementations, such as MKL, provide decent performance but take a lot of space. People may want some compromise solution with smaller footprint.

## Proposed solution

In OpenCV 2.2 we had a small subset of Lapack (i.e. CLapack from netlib) distributed with and built into OpenCV. It should be possible to restore this code (probably, update it to the latest version of CLapack).

## Impact on existing code, compatibility

* It's mostly internal change, so that user code should not be affected
* OpenCV core module will become 1-2Mb heavier, maybe more.
* Certain corner test cases may fail, because different SVD implementation may provide slightly different results, especially on the ill-conditioned matrices.
* Lapack is a big chunk of code, we need to watch potential legal issues when putting this code into OpenCV.

## Possible alternatives

1. We can explain more clearly how to build OpenCV with external BLAS/Lapack and promote it.
1. We can consider Eigen instead of Lapack, but on large matrices Lapack's SVD and Eigen decomposition is much faster than Eigen.

## References

1. [complain about the slow SVD](https://github.com/opencv/opencv/issues/10084)
1. [Lapack subset in OpenCV 2.2](https://github.com/opencv/opencv/tree/2.2/3rdparty/lapack)
1. [netlib Lapack](http://www.netlib.org/clapack/)
1. [Eigen homepage](http://eigen.tuxfamily.org/index.php?title=Main_Page)