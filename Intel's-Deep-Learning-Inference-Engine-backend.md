[Intel's Deep Learning Inference Engine](https://software.intel.com/inference-engine-devguide) is a part of 
[Intel&reg; OpenVINO&trade; toolkit](https://software.intel.com/openvino-toolkit). You can use it as a computational backend for OpenCV deep learning module.

* Download and install [Intel&reg; OpenVINO&trade; toolkit](https://software.seek.intel.com/openvino-toolkit).

* Build `cpu_extension` library contains extra layers implementations.

  * Ubuntu
  ```
  $ cd /opt/intel/computer_vision_sdk/deployment_tools/inference_engine/samples
  $ mkdir build && cd build
  $ cmake .. -DCMAKE_BUILD_TYPE=Release && make -j4
  ```

  * Microsoft Windows
  ```
  > cd C:\Intel\computer_vision_sdk_2018.1.249\deployment_tools\inference_engine\samples
  > mkdir build && cd build
  > "C:\Program Files\CMake\bin\cmake.exe" -DCMAKE_BUILD_TYPE=RELEASE -G "Visual Studio 14 Win64" ..
  > "C:\Program Files\CMake\bin\cmake.exe" --build . --config Release -- /m:4
  ```

* Build OpenCV specifying paths to installed libraries and plugins.

  * Ubuntu
  ```
  cmake \
    -DWITH_INF_ENGINE=ON \
    -DINTEL_CVSDK_DIR="/opt/intel/computer_vision_sdk/deployment_tools/" \
    -DIE_PLUGINS_PATH="/opt/intel/computer_vision_sdk/deployment_tools/inference_engine/lib/ubuntu_16.04/intel64/;/opt/intel/computer_vision_sdk/deployment_tools/inference_engine/samples/build/intel64/Release/lib/" \
    -DENABLE_CXX11=ON \
    ...
  ```

  * Microsoft Windows
  ```
  cmake ^
    -DWITH_INF_ENGINE=ON ^
    -DINTEL_CVSDK_DIR="C:\\Intel\\computer_vision_sdk_2018.1.249\\deployment_tools\\inference_engine" ^
    -DIE_PLUGINS_PATH="C:\\Intel\\computer_vision_sdk_2018.1.249\\deployment_tools\\inference_engine\\lib\\intel64\\Release;C:\\Intel\\computer_vision_sdk_2018.1.249\\deployment_tools\\inference_engine\\bin\\intel64\\Release" ^
    -DENABLE_CXX11=ON ^
    ...
  ```

* Enable Intel's Inference Engine backend right after `cv::dnn::readNet` invocation:
  ```cpp
  net.setPreferableBackend(DNN_BACKEND_INFERENCE_ENGINE);
  ```

* You may also import [pre-trained models](https://software.intel.com/openvino-toolkit/documentation/pretrained-models) passing paths to `.bin` and `.xml` files to `cv::dnn::readNet` function.