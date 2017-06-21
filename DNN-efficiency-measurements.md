Best time of single image forward pass (in millisecond):

#### CPU: Intel&reg; Core&trade; i7-6700K CPU @ 4.00GHz x 8

|           Model |    Input (CHW) | DNN, default| DNN, Halide | Intel-Caffe, MKL | TensorFlow | Torch, MKL |
|----------------:|---------------:|------------:|------------:|-----------------:|-----------:|-----------:|
|       GoogLeNet | 3x227x227, F32 |   **24.21** |          33 |                  |            |            |
|         AlexNet | 3x227x227, F32 |   **15.51** |        22.4 |             17.5 |            |            |
|       ResNet-50 | 3x224x224, F32 |       57.11 |          74 |         **55.8** |            |            |
| SqueezeNet v1.1 | 3x224x224, F32 |        8.01 |     **6.4** |             7.38 |            |            |
|    Inception-5h | 3x224x224, F32 |       24.64 |          32 |                  |   **17.9** |            |
|            ENet | 3x512x256, F32 |          96 |      **41** |                  |            |        240 |

#### GPU (OpenCL 2.0): Intel&reg; HD Graphics 530 (Skylake GT2)

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
