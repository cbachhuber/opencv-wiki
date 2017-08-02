Deep Learning is the most popular and the fastest growing area in Computer Vision nowadays. Since OpenCV 3.1 there is DNN module in the library that implements forward pass (inferencing) with deep networks, pre-trained using some popular deep learning frameworks, such as Caffe. In OpenCV 3.3 the module has been promoted from http://github.com/opencv/opencv_contrib repository to the main repository and has been accelerated significantly.

The module has no any extra dependencies, except for libprotobuf, and libprotobuf is now included into OpenCV. 

The supported frameworks:

 * Caffe 1
 * TensorFlow
 * Torch/PyTorch

The supported layers:

 * AbsVal
 * AveragePooling
 * BatchNormalization
 * Concatenation
 * Convolution (including dilated convolution)
 * Crop
 * Deconvolution, a.k.a. transposed convolution or full convolution
 * DetectionOutput (SSD-specific layer)
 * Dropout
 * Eltwise (+, *, max)
 * Flatten
 * FullyConnected
 * LRN
 * LSTM
 * MaxPooling
 * MaxUnpooling
 * MVN
 * NormalizeBBox (SSD-specific layer)
 * Padding
 * Permute
 * Power
 * PReLU (including ChannelPReLU with channel-specific slopes)
 * PriorBox (SSD-specific layer)
 * ReLU
 * RNN
 * Scale
 * Shift
 * Sigmoid
 * Slice
 * Softmax
 * Split
 * TanH

The module includes some SSE, AVX, AVX2 and NEON acceleration for the performance-critical layers. There is also constantly-improved Halide backend. OpenCL (libdnn-based) backend is being developed and should be integrated after OpenCV 3.3 release. Here you may find the up-to-date benchmark results for the module: https://github.com/opencv/opencv/wiki/DNN-Efficiency

The following networks have been tested and known to work:

 * AlexNet
 * GoogLeNet v1 (also referred to as Inception-5h)
 * ResNet-34/50/...
 * SqueezeNet v1.1
 * VGG-based FCN (semantical segmentation network)
 * ENet (lightweight semantical segmentation network)
 * VGG-based SSD (object detection network)
 * MobileNet-based SSD (light-weight object detection network)

The provided API (for C++ and Python) is very easy to use, just load the network and run it. Multiple inputs/outputs are supported. Here are the examples: https://github.com/opencv/opencv/tree/master/samples/dnn.

There is Habrahabr article describing the module: https://habrahabr.ru/company/intel/blog/333612/ (in Russian).