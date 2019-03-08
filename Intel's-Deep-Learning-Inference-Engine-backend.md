[Intel's Deep Learning Inference Engine](https://software.intel.com/inference-engine-devguide) (DL IE) is a part of [Intel&reg; OpenVINO&trade; toolkit](https://software.intel.com/openvino-toolkit). You can use it as a computational backend for OpenCV deep learning module.

### Download
* Download and install [Intel&reg; OpenVINO&trade; toolkit](https://software.seek.intel.com/openvino-toolkit). 

  **Important note**: if you want to transfer the installed Inference Engine binaries to another machine w/o running OpenVINO installer there, you need [the redistributable files of Intel C++ compiler](https://software.intel.com/en-us/articles/intel-compilers-redistributable-libraries-by-version) (use the latest update, 64-bit version), otherwise the Inference Engine or some of its essential plugins will refuse to load and run, which may result in an app crash.

### OpenCV from OpenVINO
OpenVINO 2018 R2 and later comes with OpenCV built with DL IE support, so you can skip this step if you use fresh enough version.

### Build OpenCV from source

#### Ubuntu

Setup environment variables to detect Inference Engine:
```
source /opt/intel/computer_vision_sdk/bin/setupvars.sh
```

Build OpenCV with extra flags:
```
cmake \
  -DWITH_INF_ENGINE=ON \
  -DENABLE_CXX11=ON \
  ...
```

#### Microsoft Windows

Setup environment variables to detect Inference Engine:
```
C:\Intel\computer_vision_sdk_2018.3.343\bin\setupvars.bat
```

Build OpenCV with extra flags:
```
cmake ^
  -DWITH_INF_ENGINE=ON ^
  -DENABLE_CXX11=ON ^
  ...
```

#### Raspbian Stretch

Use Docker to cross-compile OpenCV for Raspberry Pi. Check that `uname -m` detects `armv7l` CPU architecture (starts from Raspberry Pi 2 model B).

1. Create a folder named `debian_9_armhf` with a file `Dockerfile` with the following content:

  ```docker
  FROM debian:stretch

  USER root

  RUN dpkg --add-architecture armhf && \
      apt-get update && \
      apt-get install -y --no-install-recommends \
      crossbuild-essential-armhf \
      cmake \
      pkg-config \
      wget \
      xz-utils \
      libgtk2.0-dev:armhf \
      libpython-dev:armhf \
      libpython3-dev:armhf \
      python-numpy \
      python3-numpy \
      libgstreamer1.0-dev:armhf \
      libgstreamer-plugins-base1.0-dev:armhf

  # Install Inference Engine
  RUN wget --no-check-certificate https://download.01.org/openvinotoolkit/2018_R5/packages/l_openvino_toolkit_ie_p_2018.5.445.tgz && \
      tar -xf l_openvino_toolkit_ie_p_2018.5.445.tgz

  RUN useradd ocv
  USER ocv
  ```

2. Build a Docker image

  ```bash
  docker image build debian_9_armhf
  ```

  Example output:
  ```
  Successfully built 13404dac3614
  ```

3. Tag a build and run Docker container mounting source code folder from host.

  ```bash
  docker tag 13404dac3614 debian_9_armhf:latest
  docker run -i -t -v /absolute/path/to/opencv:/opencv debian_9_armhf /bin/bash
  ```

4. Build

  ```bash
  cd opencv && mkdir opencv_build && mkdir opencv_install && cd opencv_build
  cmake -DCMAKE_BUILD_TYPE=Release \
        -DCMAKE_INSTALL_PREFIX="../opencv_install" \
        -DOPENCV_CONFIG_INSTALL_PATH="cmake" \
        -DCMAKE_TOOLCHAIN_FILE="../platforms/linux/arm-gnueabi.toolchain.cmake" \
        -DWITH_IPP=OFF \
        -DBUILD_TESTS=OFF \
        -DBUILD_PERF_TESTS=OFF \
        -DOPENCV_ENABLE_PKG_CONFIG=ON \
        -DPKG_CONFIG_EXECUTABLE="/usr/bin/arm-linux-gnueabihf-pkg-config" \
        -DPYTHON2_INCLUDE_PATH="/usr/include/python2.7" \
        -DPYTHON2_NUMPY_INCLUDE_DIRS="/usr/local/lib/python2.7/dist-packages/numpy/core/include" \
        -DPYTHON3_INCLUDE_PATH="/usr/include/python3.5" \
        -DPYTHON3_NUMPY_INCLUDE_DIRS="/usr/local/lib/python3.5/dist-packages/numpy/core/include" \
        -DPYTHON3_CVPY_SUFFIX=".cpython-35m-arm-linux-gnueabihf.so" \
        -DENABLE_NEON=ON \
        -DCPU_BASELINE="NEON" \
        -DWITH_INF_ENGINE=ON \
        -DINF_ENGINE_LIB_DIRS="/inference_engine_vpu_arm/deployment_tools/inference_engine/lib/raspbian_9/armv7l" \
        -DINF_ENGINE_INCLUDE_DIRS="/inference_engine_vpu_arm/deployment_tools/inference_engine/include" \
        -DCMAKE_FIND_ROOT_PATH="/inference_engine_vpu_arm/" \
        -DENABLE_CXX11=ON ..
  make -j4 && make install
  ```

5. Copy `opencv_install` to the board. Follow https://software.intel.com/articles/OpenVINO-Install-RaspberryPI to install OpenVINO distribution for Raspberry Pi. Then type the following commands to specify new location of OpenCV:

  ```bash
  export PYTHONPATH=/path/to/opencv_install/lib/python2.7/dist-packages/cv2/python-2.7/:$PYTHONPATH
  export PYTHONPATH=/path/to/opencv_install/lib/python3.5/dist-packages/cv2/python-3.5/:$PYTHONPATH
  export LD_LIBRARY_PATH=/path/to/opencv_install/lib/:$LD_LIBRARY_PATH
  ```

### Usage

* Enable Intel's Inference Engine backend right after `cv::dnn::readNet` invocation:
  ```cpp
  net.setPreferableBackend(DNN_BACKEND_INFERENCE_ENGINE);
         // the other possible options are
         // DNN_BACKEND_OPENCV (the default C++ implementation)
         // DNN_BACKEND_HALIDE (Halide-based implementation)
  ```
  note that the inference engine backend is used by default since OpenCV 3.4.2 (OpenVINO 2018.R2) when OpenCV is built with the Inference engine support, so the call above is not necessary. Also, the Inference engine backend is the only available option (also enabled by default) when the loaded model is represented in OpenVINO&trade; Model Optimizer format.

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

  Set `OMP_WAIT_POLICY` to `PASSIVE` to prevent efficiency gaps due networks partitioning if there are layers unsupported by Inference Engine backend or you have several networks with preferable backend `DNN_TARGET_CPU`.
