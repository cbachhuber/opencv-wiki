[Intel's Deep Learning Inference Engine](https://software.intel.com/inference-engine-devguide) (DL IE) is a part of [Intel&reg; OpenVINO&trade; toolkit](https://software.intel.com/openvino-toolkit). You can use it as a computational backend for OpenCV deep learning module.

### Download
* Download and install [Intel&reg; OpenVINO&trade; toolkit](https://software.seek.intel.com/openvino-toolkit). 

  **Important note**: if you want to transfer the installed Inference Engine binaries to another machine w/o running OpenVINO installer there, you need [the redistributable files of Intel C++ compiler](https://software.intel.com/en-us/articles/intel-compilers-redistributable-libraries-by-version) (use the latest update, 64-bit version), otherwise the Inference Engine or some of its essential plugins will refuse to load and run, which may result in an app crash.

### Build
* OpenCV from OpenVINO

  OpenVINO 2018 R2 and later comes with OpenCV built with DL IE support, so you can skip this step if you use fresh enough version.

* OpenCV from source
  * Ubuntu
  ```
  cmake \
    -DWITH_INF_ENGINE=ON \
    -DINTEL_CVSDK_DIR="/opt/intel/computer_vision_sdk/deployment_tools/" \
    -DIE_PLUGINS_PATH="/opt/intel/computer_vision_sdk/deployment_tools/inference_engine/lib/ubuntu_16.04/intel64/" \
    -DENABLE_CXX11=ON \
    ...
  ```

  * Microsoft Windows
  ```
  cmake ^
    -DWITH_INF_ENGINE=ON ^
    -DINTEL_CVSDK_DIR="C:\\Intel\\computer_vision_sdk_2018.1.249\\deployment_tools\\inference_engine" ^
    -DIE_PLUGINS_PATH="C:\\Intel\\computer_vision_sdk_2018.1.249\\deployment_tools\\inference_engine\\lib\\intel64\\Release" ^
    -DENABLE_CXX11=ON ^
    ...
  ```

### Usage

* Enable Intel's Inference Engine backend right after `cv::dnn::readNet` invocation:
  ```cpp
  net.setPreferableBackend(DNN_BACKEND_INFERENCE_ENGINE);
         // the other possible options are
         // DNN_BACKEND_OPENCV (the default C++ implementation)
         // DNN_BACKEND_HALIDE (Halide-based implementation)
  ```
  note that the inference engine backend is used by default since OpenCV 3.4.2 when OpenCV is built with the Inference engine support, so the method call above is not necessary. Also, the Inference engine backend is the only available option (also enabled by default) when the loaded model is represented in OpenVINO&trade; Model Optimizer format.

* Then, optionally you can also set the device to use for the inference (by default it will use CPU):
  ```cpp
  net.setPreferableTarget(DNN_TARGET_OPENCL);
         // the possible options are
         // DNN_TARGET_CPU,
         // DNN_TARGET_OPENCL, 
         // DNN_TARGET_OPENCL_FP16
         //   (fall back to OPENCL if the hardware does not support FP16),
         // DNN_TARGET_MYRIAD
  ```

* You may also import [pre-trained models](https://software.intel.com/openvino-toolkit/documentation/pretrained-models) passing paths to `.bin` and `.xml` files to `cv::dnn::readNet` function.

### Troubleshooting

  If you run your network on CPU specify path to OpenMP by
  ```
  LD_PRELOAD=/opt/intel/computer_vision_sdk/deployment_tools/inference_engine/external/mkltiny_lnx/lib/libiomp5.so
  ```
  Set `OMP_WAIT_POLICY` to `PASSIVE` to prevent efficiency gaps due networks partitioning if there are layers unsupported by Inference Engine backend or you have several networks with this preferable backend.

* OpenVINO 2018 R2
  ```
  error: (-215:Assertion failed) prior_width > 0 in function 'DecodeBBox'
  ```
  Modify the following line at `ext_priorbox_clustered.cpp` and `ext_priorbox.cpp` in `/path/to/deployment_tools/inference_engine/samples/extension/` folder:

  ```cpp
  addConfig({{ConfLayout::ANY, true}, {ConfLayout::ANY, true}}, {{ConfLayout::PLN, true}});
  ```
  to
  ```cpp
  addConfig({{ConfLayout::ANY, true}, {ConfLayout::ANY, true}}, {{ConfLayout::PLN, false}});
  ```


  Rebuild `cpu_extension` library which contains extra layers implementations.

    * Ubuntu
    ```
    $ cd /opt/intel/computer_vision_sdk/deployment_tools/inference_engine/samples
    $ mkdir build && cd build
    $ cmake .. -DCMAKE_BUILD_TYPE=Release && make -j4
    $ export 
  LD_LIBRARY_PATH=/opt/intel/computer_vision_sdk/deployment_tools/inference_engine/samples/build/intel64/Release/lib/:$LD_LIBRARY_PATH
    ```

    * Microsoft Windows
    ```
    > cd C:\Intel\computer_vision_sdk_2018.2.300\deployment_tools\inference_engine\samples
    > mkdir build && cd build
    > "C:\Program Files\CMake\bin\cmake.exe" -DCMAKE_BUILD_TYPE=RELEASE -G "Visual Studio 14 Win64" ..
    > "C:\Program Files\CMake\bin\cmake.exe" --build . --config Release -- /m:4
    > set PATH=C:\Intel\computer_vision_sdk_2018.2.300\deployment_tools\inference_engine\bin\intel64\Release;%PATH%
    ```
    
    Replace existing `cpu_extension` libraries such `libcpu_extension_avx2.so` or `libcpu_extension_sse4.so` to a different folder to exclude them from search.