## Add unified loging/tracing abilities into OpenCV

* Author: Alexander Alekhin, Vadim Pisarevsky
* Link: [The feature request](https://github.com/opencv/opencv/issues/11003)
* Status: **Draft**
* Platforms: **All**
* Complexity: a few man-weeks to do the basic stuff, some more time to convert existing logging code to the new API

## Introduction and Rationale

OpenCV is already quite complex and in places a multi-layered library (e.g. the DNN module or video capturing API), so it could be useful to have logging capabilities. For example, logging may help to investigate and debug problems on inaccessible/remote platforms/hardware/cameras/etc. And it would be nice to use some convenient API across the whole library instead of chunks of conditionally-compiled code and ad-hoc printf's.

## Proposed solution

The solution may be based on or resemble Google's glog library. Whatever framework is used as a base (or written from scratch), it should have the following properties at least:

1. Practically zero overhead when the logging is turned off
1. Logging calls should have "component" and "verbosity" parameters, so that logging could be enabled just for the certain component and just at the certain level of verbosity (or less).
1. The control over logging should be done globally, but on per-thread basis.

## Impact on existing code, compatibility

Because it's new API and the internal changes in the library, it should not affect the existing user code.

## Possible alternatives

Leave it as-is.

## References

1. [OpenCV already includes some tracing capabilies](https://github.com/opencv/opencv/wiki/Profiling-OpenCV-Applications)
1. [Using glog](http://rpg.ifi.uzh.ch/docs/glog.html)