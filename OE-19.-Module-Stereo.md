## Introduce a separate stereo correspondence module with up-to-date algorithms

* Author: Vadim Pisarevsky
* Link: [The feature request](https://github.com/opencv/opencv/issues/11014)
* Status: **Draft**
* Platforms: **All**
* Complexity: 1-2 man-weeks (or more, if OpenCL optimization is included)

## Introduction and Rationale

The module [calib3d](https://github.com/opencv/opencv/tree/master/modules/calib3d) from OpenCV 2.x and 3.x includes various functionality including stereo correspondence algorithms. At the same time, there is experimental [stereo module in opencv_contrib](https://github.com/opencv/opencv_contrib/tree/master/modules/stereo) that includes some new stereo correspondence algorithms or interesting modifications of existing algorithms. It makes sense to put this code into a dedicated module.

## Proposed solution

Create a dedicated `stereo` module in the main repository with the best available (within the library) collection of stereo correspondence algorithms. Basically, these are `StereoBM` and `StereoSGBM` algorithms. StereoSGBM should at minimum include the 4-directional parallel version, may be 5-directional sequential versions, both pixel or feature-based. StereoBM should probably be just feature-based, because pixel-based is not very good.

The functionality may also include some API for stereo rectification, depth map to point cloud mapping etc. Potentially it may include multi-view depth estimation algorithms as well (something like DTAM).

**Question:** do we need to keep some (renamed) module in `opencv_contrib` for experimental stereo correspondence algorithms? Probably yes. Need some better than `xstereo` name.

## Impact on existing code, compatibility

Overall, the external API will change slightly, if any (there will be `StereoMatcher` base class and the derivatives), but users will have to put some other include directives in their code (or keep using `#include "opencv2/opencv.hpp"`)

## Possible alternatives

nothing really; we need to consolidate stereo correspodence code.

## References

TBD