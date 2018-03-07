## Introduce a separate optflow module with up-to-date algorithms

* Author: Vadim Pisarevsky
* Link: [The feature request](https://github.com/opencv/opencv/issues/11013)
* Status: **Draft**
* Platforms: **All**
* Complexity: 1-2 man-weeks

## Introduction and Rationale

The module [video](https://github.com/opencv/opencv/tree/master/modules/video) from OpenCV 2.x and 3.x includes various functionality including sparse and dense optical flow algorithms. At the same time, there is experimental [optflow module in opencv_contrib](https://github.com/opencv/opencv_contrib/tree/master/modules/optflow) that includes some new optical flow algorithms. It makes sense to consolidate optical flow estimation algorithm into a dedicated module.

## Proposed solution

Create a dedicated `optflow` module in the main repository with the best available (within the library) collection of sparse and dense optical flow algorithms. For the sparse optical flow we have LK optical flow and maybe some experimental `semi-dense` optical flow somewhere that we can put it. As for the dense optical flow, we have more or less classical Farneback algorithm and we have much better DIS optical flow. We need to compare them all and select the best algorithms.

We will also need to shape all the optical flow algorithms as classes derived from the base sparse or dense optical flow `estimators`. Some attempts to do that can already be found in `video` module.

We also need to rename `optflow` module in opencv_contrib to something else (let's move away from `xmodule` naming scheme in opencv_contrib)

## Impact on existing code, compatibility

Even though we consolidate API and move to the uniform object-oriented API, we may keep the old API for backward compatibility (e.g. `cv::computeOptFlowFarneback` etc.).

## Possible alternatives

nothing really; we need to consolidate optical flow code.

## References

TBD