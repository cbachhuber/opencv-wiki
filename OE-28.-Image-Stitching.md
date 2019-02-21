## Stitching Module
* Author: Jiri Horner
* Link: https://github.com/opencv/opencv/issues/11039
* Status: Open
* Platforms: All
* Complexity: Several man-weeks

## Introduction and Rationale

Stitching module has been around for quite some time and hasn't been refreshed to match changes in rest of the OpenCV.

Stitcher interface is widely used from Python, but lots of features can't be controlled from Python. User experience should be improved.

There is no interoperability with features2d module, all feature finders need to be wrapped manually for stitching module.

Dependencies on legacy CUDA stuff in stitching module let to some compilation problems recently.

Dependencies on xfeatures2d makes it impossible for distributions to provide patent-free stitching module while offering patented algorithms to use with for users that need them.

## Proposed solution
* remove detail::FeaturesFinder and detail::FeaturesMatcher wrapper classes. 
* Use cv::Feature2D and cv::DescriptorMatcher from features2d module. 
   * This will allow to use all features and descriptors with stitching modules. 
* Move all estimation code from detail::FeaturesMatcher to detail::Estimator. 
   * This also solves problems with dependencies on xfeatures2d.
* allow user to explicitly set detail::Estimator
* consolidate creation methods for stitcher. 
   * Keep only Stitcher::create, 
   * wrap this method for Python. 
   * Drop try_use_gpu flag, rely on T-API or user explicitly setting CUDA classes to use.
* allow users to set FeaturesFinder, DescriptorMatcher, BundleAdjuster etc. from Python
* drop legacy usage of legacy Levenberg–Marquardt API from bundle adjusters. Replace with new LevMarq API.
* remove direct usage of CUDA from stitching module (OpenCL alternatives are already available). Move to CUDA modules where it makes sense.

## Impact on existing code, compatibility
Changes in Stitcher interface might require some changes in user code. We could introduce some wrapper classes and aliases to ease transition towards using new API with classes from features2d.

## Possible alternatives
Keep as is.

## References
1. https://github.com/opencv/opencv/issues?utf8=%E2%9C%93&q=is%3Aissue+label%3A%22category%3A+gpu+%28cuda%29%22+stitching