## Implement ONNX importer in OpenCV DNN module

* Author: Vadim Pisarevsky
* Link: [The feature request](https://github.com/opencv/opencv/issues/11008)
* Status: **Draft**
* Platforms: **All**
* Complexity: 1-2 man-months

## Introduction and Rationale

[ONNX](https://onnx.ai) is Open Neural Network Exchange Format, co-developed by Facebook, Amazon and Microsoft and supported by many more big and small companies.

It's now supported by Caffe 2, PyTorch, MxNet, and it's big chance that it will become de-facto standard to represent the deep models. So it would be useful to have support for such format in OpenCV.

## Proposed solution

ONNX support code is open-source project under MIT license hosted at github [\[1\]](https://github.com/onnx/onnx). It's also quite well documented with several popular models converted to this format. It would be quite strait-forward task to create the parser for it in OpenCV similar to Caffe, TensorFlow, Torch and Darknet parsers.

## Impact on existing code, compatibility

It's extra functionality in DNN, so it will not affect any existing code.

## Possible alternatives

Possible alternative would be to have some python script that would parse ONNX models and convert them to TensorFlow. Eventually, we may want to limit the number of formats supported by OpenCV DNN and may be even exclude some (e.g. Torch, Darknet), but ONNX looks like some well-supported thing that should stay around for a long time.

## References

1. [ONNX source code](https://github.com/onnx/onnx)
