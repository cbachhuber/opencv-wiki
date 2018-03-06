OpenCV 3.x is the release series maintained for almost 3 years already (as of 2018 Spring). It's been an evolutionary and noticeable improvement over 2.4.x and brought the following major features:

* Revised OpenCL acceleration, a.k.a. T-API, with semi-automatic fallback to CPU.
* Subset of IPP (IPPICV) is included into the library by default (though, it can be explicitly excluded). It accelerates some basic core & imgproc OpenCV functionality noticeably.
* Introduced opencv_contrib repository with experimental functionality. At the moment, the repository includes over 30 modules.
* Introduced OpenCV HAL, low-level synchronous (i.e. CPU-oriented) API that can be used to accelerate various OpenCV functions on different platforms. Currently, there is ARM acceleration backend by NVidia. Part of IPPICV acceleration is also done via HAL API.
* A major cleanup of the library has been done where we mostly replaced internal C-like code that used OpenCV 1.x API with the new versions using C++ API. The external API has also been cleaned, and we now extensively use the “open interface + hidden implementation” pattern.
* ML module has been completely rewritten using the new-style C++ API.
* A lot of new functionality has been added, mostly as user contributions and results of GSoC 2015, 2016 and 2017.
* Doxygen replaced RST (ReStructuredText) as the documentation generation tool. For big textual chunks of documentation, such as the tutorials, we now use markdown. 

At the same time, many fundamental aspects of the library have been retained:

* The library is built up as a collection of modules with well-defined directory structure (include, src, test, perf, samples etc. subdirectories)
* CMake is used as configuration and build system.
* Retained the same set of basic types: `cv::Mat`, `std::vector<>`, `cv::Matx<>`, `cv::Vec<>`, `cv::Ptr<>`. `cv::Mat`-like `cv::UMat` type has been added to implement T-API.
* The basic modules `core`, `imgproc`, `highgui`, i.e. the mostly used ones, are pretty much compatible with OpenCV 2.x (even though `highgui` has been split into `highgui`, `imgcodecs` and `videoio`).
* Python bindings were extended to support Python 3.
