#### Configurations list

**OS:** Linux 4.8.0-34-generic x86_64  
**OpenCV:** 3.2.0-dev (22th Jun 2017)
**Compiler:** gcc 5.4.0  
**CPU:** Intel&reg; Core&trade; i7-6700K CPU @ 4.00GHz x 8  
**GPU:** Intel&reg; HD Graphics 530 (Skylake GT2)
**MKL:** 2017


|   Framework| State                                                                                   |
|-----------:|-----------------------------------------------------------------------------------------|
|     OpenCV | https://github.com/opencv/opencv/commit/d27009c775307e18d28da430862665ef1934d400        |
|        DNN | https://github.com/opencv/opencv_contrib/commit/e551d15c2b58edce36fe5a5c23072cbe6ce74a93|
|    clCaffe | https://github.com/BVLC/caffe/commit/483c58f5f46b5959dc0a978882843713daae18f6           |
| TensorFlow | https://github.com/tensorflow/tensorflow/commit/1ec6ed51182adf8f1b03a3188c16cd8a45ca6c85|
|      Torch | https://github.com/torch/distro/tree/748f5e3c5c804eebf5715c0b47b1519d60ef4409           |
|     Halide | https://github.com/halide/Halide/commit/abef1d9bf6cb3f866393fa4c5f48726f728285ee        |
| LLVM/Clang | 4.0.0                                                                                   |

Best time of single image forward pass (in milliseconds):

#### CPU

|           Model |    Input (CHW) | DNN, default| DNN, Halide | Intel-Caffe, MKL | TensorFlow | Torch, MKL |
|----------------:|---------------:|------------:|------------:|-----------------:|-----------:|-----------:|
|       GoogLeNet | 3x227x227, F32 |   **20.01** |          33 |                  |            |            |
|         AlexNet | 3x227x227, F32 |   **14.68** |        22.4 |             17.5 |            |            |
|       ResNet-50 | 3x224x224, F32 |       56.82 |          74 |         **55.8** |            |            |
| SqueezeNet v1.1 | 3x224x224, F32 |    **5.82** |         6.4 |             7.38 |            |            |
|    Inception-5h | 3x224x224, F32 |       21.05 |          32 |                  |   **17.9** |            |
|            ENet | 3x512x256, F32 |       65.69 |      **41** |                  |            |        240 |

#### GPU (OpenCL 2.0): 

|           Model |    Input (CHW) | DNN, Halide |     clDNN | clCaffe, MKL |
|----------------:|---------------:|------------:|----------:|-------------:|
|       GoogLeNet | 3x227x227, F32 |       93.56 |    **28** |          181 |
|         AlexNet | 3x227x227, F32 |          49 | **14.65** |           27 |
|       ResNet-50 | 3x224x224, F32 |         189 |           |      **132** |
| SqueezeNet v1.1 | 3x224x224, F32 |        18.3 |   **8.0** |         18.2 |
|    Inception-5h | 3x224x224, F32 |        89.5 |           |              |
|            ENet | 3x512x256, F32 |       39.67 |           |              |

#### References
* OpenCV's deep learning module, https://github.com/opencv/opencv_contrib/tree/master/modules/dnn.
* Intel-Caffe, https://github.com/intel/caffe.
* clCaffe, https://github.com/BVLC/caffe/tree/opencl.
* clDNN, https://github.com/01org/clDNN.
* TensorFlow, https://www.tensorflow.org/.
* Torch, http://torch.ch/.
* Halide, http://halide-lang.org/.
