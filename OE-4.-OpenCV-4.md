## Planning OpenCV 4.0

* Author: Vadim Pisarevsky
* Link: TBD
* Status: **Draft**
* Platforms: **All**
* Complexity: many man-weeks

## Introduction and Rationale


Now, why release 
Given that OpenCV 3.0 came out 6 years later after OpenCV 2.0, one may wonder why release 4.0 in “just” 3 years after 3.0 (assuming that 4.0 will be released in 2018, June).

Here are some fundamental reasons (not sorted by importance):

Switch to C++ 11. OpenCV 3.0 is C++ 98 library, whereas many C++ developers switched to C++ 11 or even later standards. C++ 11 includes many new features, and at least some of them can be useful for OpenCV users and for us, OpenCV developers:
lambda functions – will simplify parallel_loop implementation. BTW, we added parallel_for flavor with lambda function argument (std::function) in OpenCV 3.3.
static_assert. Now we use ad-hoc implementation of it.
“auto” keyword and the special for-in loop will make code less verbose.
std::threads. Could implement task-level parallelism on top of it.
thread_local variables. Another little thing that could simplify OpenCV code.
initializer lists. We’ve already added such initializers for basic OpenCV data structures to OpenCV 3.3.
easier-to-use static class member initializers.
move semantics could probably be useful for some matrix expressions.
const_expr could probably let us to simplify some universal intrinsics and some other things.
C++ 11 mode is already being tested by our buildbot. That is, our users can build OpenCV as C++ 11 library and use all the new features in their apps. But we cannot use C++ 11 inside OpenCV. If we start using C++ 11, there is no way back – if we decide to make use of C++ 11 features but provide backward-compatible branches, it will make OpenCV code more obscure, not less obscure. And going with C++ 11 means breaking “binary compatibility promise”, so this move alone would require OpenCV 4.0. 
Disclaiming binary compatibility and moving to source-level compatibility. Several years ago we stated that OpenCV will stay binary-compatible between major releases. Technically, it was a necessary thing for OpenCV Manager for Android, but it also was seemingly useful thing for binary OpenCV packages for Linux. Those are the positive things about binary compatibility. However, binary compatibility puts a lot of restrictions, such as:
one cannot add a virtual method to a class. We use quite weird tricks with dynamic_cast<> as a workaround.
one cannot convert a method from virtual to non-virtual or vice versa.
sometimes one cannot add an overloaded method (virtual or even non virtual).
it’s impossible to add an optional parameter to a method (even non-virtual) or a function.
it’s impossible to change parameter type to more general one (e.g. cv::Mat to cv::InputArray).
we cannot shuffle functionality between modules.
At the same time, the reasons to preserve binary compatibility are not that relevant anymore:
OpenCV Manager for Android appears to be used by very simple applications. Any real application with real QA cannot depend on externally and independently updated software. Instead, developers prefer to link their apps against the known and tested (within the app) version of OpenCV statically.
Linux distributions also often prefer not to make major updates of OpenCV and just patch the security problems instead. And it’s not that OpenCV is included into the list of “essential” packages of some Linux distro. The static libs should also be preferred way to distribute OpenCV binaries in Linux.
It’s the same situation on Mac, Windows and iOS. On iOS there is no option at all to use dynamic OpenCV libraries.
So there is a serious intention to relax “binary compatibility” claim to “source compatibility”. But this requires a new major release. Within 3.x we preserve binary compatibility.
Halide as a part of OpenCV. We already experimented quite a bit with Halide and think that Halide can partially or completely replace many of the kernels that we optimize manually. In fact, it can fundamentally change the way we and our users write computationally-intensive CV code. But now Halide is a separately evolving tool that has dependency from LLVM, and thus is quite heavy. So, we cannot expect that many OpenCV users will make serious use of it. So, we cannot use it “by default” and hope that all the users will have it. So there is ambitious plan to embed a subset of Halide into OpenCV and treat OpenCV + Halide as the new-style OpenCV. And it may transform OpenCV in such a radical way that we would definitely need the new major release to start this process and the disclaimed binary compatibility at least during the process. Besides, Halide is C++ 11 library. See the dedicated section about the Halide below.
Big revision of functionality and modules content. Computer Vision evolves fast (especially since the raise of Deep Learning) and so many algorithms present in OpenCV 3.x (many of which date back to OpenCV 2.x and even OpenCV 1.x) can be considered as obsolete now and safely moved to opencv_contrib. At the same time, in opencv_contrib there is some interesting stuff (e.g. cool optical flow, tracking algorithms) that is worth going to the main repository. Such a radical revision cannot be done without a new major release.
Compact OpenCV. This item correlates with the previous ones, but it’s important enough for a separate discussion. People like compact solutions and for mobile/embedded/“edge-side” vision the library footprint may be an essential thing. OpenCV 3.x is big, e.g. self-contained Python module for Windows, cv2.pyd, takes as much as 100MB. Since OpenCV 1.0 the library grew in size, but only a small part of it is actually used by most of the users. Something like 80-20 or even 90-10 rule is likely valid here. OpenCV is so big because of the following:
for many CV and image processing tasks, such as demosaicing, HDR, background segmentation, optical flow, PnP registration, tracking, stereo, feature detectors etc. we often offer several different algorithms, but only few of them are “pareto-optimal”, i.e. are “very fast with good quality” or “very good quality, yet reasonably fast”. There is no good solution for this problem other than do a periodical cleaning and move “second-best” algorithms to opencv_contrib.
Extensive data type support in basic and not very basic functions. OpenCV uses templates, but it’s not a template library (which is very good property, apparently). So the template are instantiated at OpenCV compile time and it increases the library size. Since users usually need only a tiny fraction of all those branches, it would be nice to generate the code on-fly. It’s where OpenCL helps a lot in the case of GPU and it’s where Halide could definitely help.
IPP acceleration adds a lot. IPP folks promised to prepare a stripped version of IPPICV in the next update.
It would be nice if OpenCV 4.0 will be 2x or 10x smaller than OpenCV 3.x. And, of course, it cannot be done without bumping major version number.
Another big revision of DNN module. DNN module got quite a good shape by OpenCV 3.3, and given its importance for community, we decided to move it to the main repository. But there are still some things that we’d like to make there, including some API changes, like migration from cv::Mat to cv::InputArray in method parameters, much easier integration of user layers, including the layers implemented in Halide, GPU acceleration (through Halide or not) etc. It’s not a big reason to make a major release on its own, but if we make OpenCV 4.0, it’s good opportunity to extend DNN and maybe even do some redesign of the architecture.
New, even more distributed development model (?) This is quite fuzzy idea at the moment, but conceptually it’s the further extension of the idea of splitting opencv into opencv “main” and opencv_contrib. Something like the Python distribution model “download, build and use it at your own risk”. It’s not clear what changes it will require in OpenCV build scripts, but they also may require a major release.
Because we can. OpenCV 3.0 has been released at the time when OpenCV dev team was rather small and so we could not afford to make OpenCV 3.0 a radically better than 2.x library. Now the core team is the biggest one during past ~10 years, so, I believe, we should use the chance and spend the resources on some radical improvements in the library instead of putting another 100 algorithms into the library which we could unlikely support for many years when the team will inevitably become smaller.

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
