Opencv4
=======

Major Changes
-------------

OpenCV 4.0 is the evolution of OpenCV 3.0. We follow the same design principles and the same library layout as in OpenCV 3.0. So most of the code and most of the scripts should work fine, with a few notable exceptions:

 * Most of the C API has been excluded. In particular, instead of `cv::cvtColor(src, dst, CV_RGB2GRAY)` one should use `cv::cvtColor(src, dst, cv::COLOR_RGB2GRAY)`; instead of `cv::VideoCapture cap(0); cap.set(CV_CAP_PROP_WIDTH, 640);` one should use `cv::VideoCapture cap(0); cap.set(cv::CAP_PROP_WIDTH, 640);` etc. Also, the classical C data structures, such as `CvMat`, `IplImage`, `CvMemStorage` etc., as well as the corresponding functions, such as `cvCreateMat()`, `cvThreshold()` etc., are mostly excluded from API and will be completely excluded in further OpenCV 4.x updates. Please, replace them with the corresponding C++ structures and functions, like `cv::Mat`, `std::vector`, `cv::threshold()` etc.

Graph API
---------

The new engine for constructing efficient image processing has been introduced. See [[Graph API (G-API)|Graph-API]] for details.
