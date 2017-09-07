#### Configuration:

 **OS:** Linux 4.8.0-34-generic x86_64  
 **Compiler:** gcc 5.4.0  
 **CPU:** Intel&reg; Core&trade; i7-6700K CPU @ 4.00GHz x 8  
 **GPU:** Intel&reg; HD Graphics 530 (Skylake GT2)

|            | State                                                                                   |
|-----------:|-----------------------------------------------------------------------------------------|
|     OpenCV | https://github.com/opencv/opencv/commit/b46f5b1b386663ea2df9ec70f65d1668cbf154d1        |
|Intel-Caffe | https://github.com/intel/caffe/commit/3bbc9f11d9dffbb96f8944ebb6303ecba48b4188          |
|    clCaffe | https://github.com/BVLC/caffe/commit/483c58f5f46b5959dc0a978882843713daae18f6           |
| TensorFlow | https://github.com/tensorflow/tensorflow/commit/1ec6ed51182adf8f1b03a3188c16cd8a45ca6c85|
|      Torch | https://github.com/torch/distro/tree/748f5e3c5c804eebf5715c0b47b1519d60ef4409           |
|     Halide | https://github.com/halide/Halide/commit/abef1d9bf6cb3f866393fa4c5f48726f728285ee        |
| LLVM/Clang | 4.0.0                                                                                   |
|        MKL | Build date 2017.04.13                                                                   |

Best time of single image forward pass (in milliseconds):

#### CPU
All calculations are done in float32.

Actual measurements in progress: https://github.com/opencv/opencv/pull/9313
> | Model | DNN, C++ | DNN, Halide | Intel-Caffe, MKLDNN | TensorFlow | Torch w. MKL |
> |----------------:|----------:|--------:|---------:|---------:|---------:|
> |       GoogLeNet |     19.50 |      33 |  **9.31**|          |          |
> |         AlexNet |     14.68 |    22.4 | **11.95**|          |          |
> |       ResNet-50 |     42.56 |      74 | **22.54**|          |          |
> | SqueezeNet v1.1 |      4.96 |     6.4 | **3.01** |          |          |
> |    Inception-5h |     19.58 |      32 |          | **17.9** |          |
> |  ENet @ 512x256 |     45.79 |  **41** |          |          |      240 |

#### GPU (OpenCL 2.0): 
All computations in float-32.

Actual measurements in progress: https://github.com/opencv/opencv/pull/9313
> |           Model | DNN, Halide|     clDNN | clCaffe |
> |----------------:|------------:|----------:|-------------:|
> |       GoogLeNet |  93.56 |      28.0 |    **18.59** |
> |         AlexNet |     49 | **14.65** |        15.22 |
> |       ResNet-50 |    189 |           |    **57.77** |
> | SqueezeNet v1.1 |   15.8 |       8.0 |     **5.58** |
> |    Inception-5h |   89.5 |           |              |
> |  ENet @ 512x256 |  39.67 |           |              |

#### References
* OpenCV's deep learning module, https://github.com/opencv/opencv_contrib/tree/master/modules/dnn.
* Intel-Caffe, https://github.com/intel/caffe.
* clCaffe, https://github.com/BVLC/caffe/tree/opencl.
* clDNN, https://github.com/01org/clDNN.
* TensorFlow, https://www.tensorflow.org/.
* Torch, http://torch.ch/.
* Halide, http://halide-lang.org/.
