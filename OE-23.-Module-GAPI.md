## Introduce a separate module implementing expression-based image processing

* Author: Vadim Pisarevsky
* Link: [The feature request](https://github.com/opencv/opencv/issues/11018)
* Status: **WIP** (currently not exposed to the public)
* Platforms: **All**
* Complexity: several man-months

## Introduction and Rationale

See the [Mini Halide](OE-16.-Mini-Halide) proposal for the basic introduction and rationale. While the Halide mini-compiler is cooking, it may be useful to have some intermediate solution for efficient image processing pipelines that would do tiling, parallelization and potentially offloading to GPU automatically. This is what G-API designed for.

## Proposed solution

TBD

## Impact on existing code, compatibility

This is new functionality, it should not affect existing code. It may affect how people write the new code though.

We should also think how to provide smooth transition to Halide-in-OpenCV when it's finally ready.

## Possible alternatives

the existing API and Halide.

## References

1. [Image Algebra - one of inspiration sources for G-API](https://www.researchgate.net/publication/220690331_Handbook_of_Computer_Vision_Algorithms_in_Image_Algebra)