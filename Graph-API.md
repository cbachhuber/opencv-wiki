What it is?
===========

* OpenCV 4.0 comes with an experimental Graph API module (see [opencv/modules/gapi](https://github.com/opencv/opencv/tree/master/modules/gapi)). This is a new API which allows to enable offload and optimizations for image processing / CV algorithms on pipeline level.

* The idea behind G-API is to declare image processing task in form of expressions and then submit it for execution – using a number of available backends. At the moment, there’s reference “CPU” (OpenCV-based), "GPU" (also OpenCV T-API-based), and experimental “Fluid’ backends available, with other backends coming up next.

* G-API is an uncommon OpenCV module since it acts as a framework: it provides means for declaring operations, building graphs of operations, and finally implementing the operations for a particular backend. G-API model enforces separation between interfaces and implementations, so once an algorithm is expressed in G-API terms, it can be scaled/ported/offloaded to a new platform easily.

* G-API CPU (OpenCV) backend implements G-API standard functions using OpenCV itself (core/imgproc modules) and acts as a quick prototyping/porting/testing backend. If you have an image processing algorithm composed of OpenCV-like functions already, you would be able to switch quickly to G-API by using this backend.

* G-API Fluid backend implements a cache-efficient execution model and allows to save memory dramatically – e.g. a 1.5GB image processing pipeline fits into 750KB memory footprint with G-API/Fluid. G-API comes with a number of operations implemented for Fluid backend, so one can switch OpenCV/Fluid operations within a graph easily and even mix both in the same graph.

* G-API GPU backend implements the majority of available functions and allows to run OpenCL kernels on available OpenCL-programmable devices. At the moment, GPU backend is based on OpenCV Transparent API; in future versions it will be extended to support integration of arbitrary OpenCL kernels (and likely be renamed to "OpenCL backend").

Materials
============

* A [tutorial](https://docs.opencv.org/4.0.0/df/d7e/tutorial_table_of_content_gapi.html) and some [documentation chapters](https://docs.opencv.org/4.0.0/d0/d1e/gapi.html) are already available!

* Check out [these slides](files/2018-12-24-GAPI_Overview.pdf) as a compact introduction to G-API.
