Deep Learning is the most popular and the fastest growing area in Computer Vision nowadays. Since OpenCV 3.1 there is DNN module in the library that implements forward pass (inferencing) with deep networks, pre-trained using some popular deep learning frameworks, such as Caffe. In OpenCV 3.3 the module has been promoted from opencv_contrib repository to the main repository (https://github.com/opencv/opencv/tree/master/modules/dnn) and has been accelerated significantly.

The module has no any extra dependencies, except for libprotobuf, and libprotobuf is now included into OpenCV. 

The supported frameworks:

 * [Caffe](http://caffe.berkeleyvision.org/)
 * [TensorFlow](https://www.tensorflow.org/)
 * [Torch](http://torch.ch/)
 * [Darknet](https://pjreddie.com/darknet/)
 * Models in [ONNX](https://onnx.ai/) format

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

The module includes some SSE, AVX, AVX2 and NEON acceleration of the performance-critical layers. There is also constantly-improved Halide backend. OpenCL (libdnn-based) backend is being developed and should be integrated after OpenCV 3.3 release. Here you may find the up-to-date benchmarking results: [[DNN Efficiency|DNN-Efficiency]]

The provided API (for C++ and Python) is very easy to use, just load the network and run it. Multiple inputs/outputs are supported. Here are the examples: https://github.com/opencv/opencv/tree/master/samples/dnn.

There is Habrahabr article describing the module: https://habrahabr.ru/company/intel/blog/333612/ (in Russian).

The following networks have been tested and known to work:

---
#### Image classification
---
##### Caffe
 * [AlexNet](http://dl.caffe.berkeleyvision.org/)
 * [GoogLeNet](http://dl.caffe.berkeleyvision.org/)
 * [VGG](http://www.robots.ox.ac.uk/~vgg/research/very_deep/)
 * [ResNet](https://github.com/KaimingHe/deep-residual-networks)
 * [SqueezeNet](https://github.com/DeepScale/SqueezeNet)
 * [DenseNet](https://github.com/shicai/DenseNet-Caffe)
 * [ShuffleNet](https://github.com/farmingyard/ShuffleNet)
##### TensorFlow
 * [Inception](https://github.com/petewarden/tf_ios_makefile_example)
 * [MobileNet](https://github.com/tensorflow/models/tree/master/research/slim/nets)
##### Darknet: https://pjreddie.com/darknet/imagenet/
##### ONNX: https://github.com/onnx/models
 * AlexNet
 * GoogleNet
 * CaffeNet
 * RCNN_ILSVRC13
 * ZFNet512
 * VGG16, VGG16_bn
 * ResNet-18v1, ResNet-50v1
 * CNN Mnist
 * MobileNetv2
 * LResNet100E-IR
 * Emotion FERPlus
 * Squeezenet
 * DenseNet121
 * Inception v1, v2
 * Shufflenet

---
#### Object detection
---
##### Caffe
 * [SSD VGG](https://github.com/weiliu89/caffe/tree/ssd)
 * [MobileNet-SSD](https://github.com/chuanqi305/MobileNet-SSD)
 * [Faster-RCNN](https://github.com/rbgirshick/py-faster-rcnn)
 * [R-FCN](https://github.com/YuwenXiong/py-R-FCN)
 * [OpenCV face detector](https://github.com/opencv/opencv/tree/master/samples/dnn/face_detector)
##### TensorFlow
 * [SSD, Faster-RCNN and Mask-RCNN from TensorFlow Object Detection API](https://github.com/tensorflow/models/tree/master/research/object_detection)
 * [EAST: An Efficient and Accurate Scene Text Detector](https://github.com/argman/EAST), paper: https://arxiv.org/abs/1704.03155v2
##### Darknet
 * [YOLOv2, tiny YOLO, YOLOv3](https://pjreddie.com/darknet/yolo/)
##### ONNX: https://github.com/onnx/models
 * TinyYolov2

---
#### Semantic segmentation
 * [FCN](https://github.com/shelhamer/fcn.berkeleyvision.org) (Caffe)
 * [ENet](https://github.com/e-lab/ENet-training) (Torch)
 * ResNet101_DUC_HDC (ONNX: https://github.com/onnx/models)

---
#### Pose estimation
 * [OpenPose body and hands pose estimation](https://github.com/CMU-Perceptual-Computing-Lab/openpose) (Caffe)

---
#### Image processing
 * [Colorization](https://github.com/richzhang/colorization) (Caffe)
 * [Fast-Neural-Style](https://github.com/jcjohnson/fast-neural-style) (Torch)

---
#### Person identification
 * [OpenFace](https://github.com/cmusatyalab/openface) (Torch)