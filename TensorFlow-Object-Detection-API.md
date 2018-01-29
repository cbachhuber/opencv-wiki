**WIP**

This wiki describes how to work with object detection models trained using [TensorFlow Object Detection API](https://github.com/tensorflow/models/tree/master/research/object_detection).

## Run network in TensorFlow
Deep learning networks in TensorFlow are represented as graphs where an every node is a transformation of it's inputs. They could be common layers like `Convolution` or `MaxPooling` and implemented in C++ or a custom ones