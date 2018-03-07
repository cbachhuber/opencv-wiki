## Getting rid of C API in OpenCV

* Author: Vadim Pisarevsky
* Link: [The feature request](https://github.com/opencv/opencv/issues/11000)
* Status: **Draft**
* Platforms: All
* Complexity: a few man-weeks

## Introduction and Rationale

There is no new OpenCV 1.x versions for a long time already, but there is still the legacy C API. It's partly used in OpenCV itself (e.g. persistence, parts of calib3d etc.) and partly by very old user code. We generally want to get rid of all this functionality in the new versions of OpenCV.

C API is very old. It's not safe to use, it's verbose. We want to eliminate the use of this old API from OpenCV itself and encourage our users to do the same.

## Proposed solution

* Rewrite persistence using STL containers.
* Get rid of IplImage, CvSeq etc. data structures.
* Rewrite the remaining imgproc, calib3d, ... using OpenCV C++ API (cv::Mat, cv::Matx, std::vector etc.)
* Get rid of the old API in highgui, videoio, imgcodecs, ...

## Impact on existing code, compatibility

it will likely have slight impact on most OpenCV users who switched to C++ API long time ago. Still, some applications may stop to compile. For them there is still an option to use OpenCV 2.4.x and OpenCV 3.x 

## Possible alternatives

Clean up OpenCV itself so that it does not use C API anymore. But the old functionality can be retained.

## References

1. [The related question at OpenCV Answers](http://answers.opencv.org/question/17546/opencv-will-drop-c-api-support-soon/)