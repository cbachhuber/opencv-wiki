# What is it?

This is the collection of OpenCV Evolution proposals. OpenCV is quite mature library, but still there are many small and big things that the core team and the community would like to change or would like to add. For small and not so small things one can submit [bug reports or feature requests](https://github.com/opencv/opencv/issues), one can submit a [pull request](https://github.com/opencv/opencv/wiki/How_to_contribute) with the ready solution. But what to do with big things that may take several man-weeks or even several man-months to implement and that can significantly affect the library and our users? How to document such big ideas, bring it up to some public discussion? For this purpose we've established the _OpenCV Evolution_ mechanism, similar to [Python PEP](https://www.python.org/dev/peps/) or [Swift Evolution](https://github.com/apple/swift-evolution).

Each evolution proposal should be shaped as a page in our wiki following the certain [template](OpenCV-Evolution-Template). Initially one can submit such evolution proposal as a [feature request](https://github.com/opencv/opencv/issues) and if the core team/committee decides that it deserves to be an evolution proposal, we add the corresponding tag "evolution", and copy the content to our wiki with the link to  the corresponding feature request, which is retained as the place for discussion.

The pool of evolution proposals can then be used to plan GSoC projects, as the list of possible projects for volunteers who would like to contribute to OpenCV etc.

# The list of evolution proposals

* [OE-0 - The Template](OE-0.-Template)
* [OE-1 - OpenCV 1.x C API Maintainance](OE-1.-Old-C-API)
* [OE-2 - OpenCV 2.x Maintainance](OE-2.-OpenCV-2)
* [OE-3 - OpenCV 3.x Maintainance](OE-3.-OpenCV-3)
* [OE-4 - OpenCV 4.0](OE-4.-OpenCV-4)
* OE-5 to OE-9 are reserved for OpenCV 5.0 to 9.0
* [OE-10 - FP16 Support](OE-10.-FP16)
* [OE-11 - Add Logging](OE-11.-Logging)
* [OE-12 - Bring Lapack back](OE-12.-Lapack)
* ~~[OE-13 - ONNX Importer in DNN](OE-13.-DNN-ONNX-Importer)~~
* ~~[OE-14 - FP16 Path in DNN](OE-14.-DNN-FP16)~~
* [OE-15 - Bit-Exactness](OE-15.-Bit-Exactness)
* [OE-16 - Mini-Halide in OpenCV](OE-16.-Mini-Halide)
* [OE-17 - New Filter Engine](OE-17.-New-Filter-Engine)
* [OE-18 - Optflow Module](OE-18.-Module-Optflow)
* [OE-19 - Stereo Module](OE-19.-Module-Stereo)
* [OE-20 - Calibration Module](OE-20.-Module-Calibration)
* [OE-21 - Tracking Module](OE-21.-Module-Tracking)
* [OE-22 - Point Cloud Module](OE-22.-Module-Point-Cloud)
* [OE-23 - Graph API Module](OE-23.-Module-GAPI)
* [OE-24 - Revised HighGUI Module](OE-24.-Module-HighGUI)
* [OE-25 - H/W Accelerated Video I/O](OE-25.-Fast-VideoIO)
* [OE-26 - Revise Samples](OE-26.-Samples)
* [OE-27 - Wide Universal Intrinsics](OE-27.-Wide-Universal-Intrinsics)