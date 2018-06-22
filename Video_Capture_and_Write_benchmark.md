## Introduction

In this experiment, performance (video stream encoding and decoding) and ease of use of the OpenCV library for CPU and iGPU were studied. For this purpose, the libraries libva (VA-API) and FFmpeg were used. FFMpeg was used for processing on CPU, because OpenCV wrapper for this library does not support hardware acceleration yet.

**FFmpeg** is a free software project, the product of which is a vast software suite of libraries and programs for handling video, audio, and other multimedia files and streams.

**VAAPI (Video Acceleration API)** is an API specification, which provides access to graphics hardware acceleration capabilities for video processing.

More information about [FFmpeg](https://www.ffmpeg.org/) and [VA-API](https://01.org/vaapi).

## Install libraries

You can use the apt package management tools to update your local package index. Afterwards, you can download and install gstreamer's programs:

```.sh
# GStreamer library and plugins
sudo apt install \
    libgstreamer1.0-dev \
    gstreamer1.0-plugins-good libgstreamer-plugins-good1.0-dev \
    gstreamer1.0-plugins-base libgstreamer-plugins-base1.0-dev \
    gstreamer1.0-plugins-bad libgstreamer-plugins-bad1.0-dev \
    gstreamer1.0-libav \
    gstreamer1.0-vaapi
# FFmpeg dev package
sudo apt install libavcodec-dev
```

## Benchmark tool

This is a program implemented as OpenCV sample application which allows user can select one of predefined video processing pipelines and measure its performance. The source code for this program can be found [here](https://github.com/opencv/opencv/blob/master/samples/cpp/gstreamer_pipeline.cpp)

To build it configure and build OpenCV as follows (Linux):
```.sh
cmake -D BUILD_EXAMPLES=ON -D WITH_GSTREAMER=ON -D WITH_FFMPEG=ON path_to_opencv_source
make -j4
```

For the experiment we measured performance of decoding/encoding of video streams with several popular codecs (mpeg2, mpeg4, h264, h265, mjpeg, vp8) and stored in several different containers (mkv, mp4, mov, avi).

The benchmark tool can be run in _decode_ and _encode_ modes and can use one of several configurations described below.

### Default configuration (GStreamer, FFmpeg)

VideoCapture/VideoWriter object created using file name, OpenCV builds processing pipelines automatically:
```.cpp
VideoCapture cap(file_name, CAP_GSTREAMER);
// or
VideoCapture cap(file_name, CAP_FFMPEG);
```
To use these configurations set backend option to _gst-default_ or _ffmpeg_.

### Basic configuration (GStreamer)

GStreamer pipeline is generated according to codec and file format, _bin_ elements automatically choose appropriate plugins to process video stream:
```.cpp
VideoCapture cap("filesrc location=<filename> ! avidemux ! decodebin ! appsink", CAP_GSTREAMER);
```
To use this configuration set backend option to _gst-basic_.

### HW-accelerated configuration (GStreamer)

Decode/encode elements are selected from VAAPI or MediaSDK GStreamer plugins according to selected codec:
```.cpp
VideoCapture cap("filesrc location=<filename> ! avidemux ! vaapidecodebin ! appsink", CAP_GSTREAMER);
// or
VideoCapture cap("filesrc location=<filename> ! avidemux ! mfxh264dec ! appsink", CAP_GSTREAMER);
```
To use these configurations set backend option to _gst-vaapi_ or _gst-mfx_.

### libav GStreamer plugin (GStreamer)

In this mode decoding/encoding elements are selected from libav GStreamer plugin:
```.cpp
VideoCapture cap("filesrc location=<filename> ! avidemux ! avdec_h264 ! appsink", CAP_GSTREAMER);
```
To use this configurations set backend option to _gst-libav_.


## Results

Test video: full HD video (1920x1080) with some default codec settings

Test platform: Ubuntu 17.10 / Intel® Core™ i5-6600 CPU @ 3.30GHz / Intel® HD Graphics 530 (Skylake GT2)

Some of the results are presented in the following tables.

Decoding (FPS):

| format | gst-libav | ffmpeg | gst-vaapi |
|:----------|----:|----:|:-----------:|
| mkv/mpeg2 | 266 | 244 | 198 (x0.74) |
| mkv/h264  | 126 | 158 |  59 (x0.37) |
| mkv/h265  | 185 | 255 |  65 (x0.26) |
| mkv/vp8   | 226 | 309 |  68 (x0.22) |
| mp4/mpeg2 | 343 | 258 | 364 (x1.06) |
| mp4/h264  | 167 | 169 | 376 (x2.2)  |
| mp4/h265  | 233 | 256 | 391 (x1.5)  |
| avi/mpeg2 | 306 | 243 | 328 (x1.07) |
| avi/h264  | 140 | 159 | 373 (x2.4)  |
| avi/vp8   | 299 | 309 | 386 (x1.3)  |

Encoding (FPS):

| format | gst-libav | ffmpeg | gst-vaapi |
|:----------|---:|----:|:----------:|
| mkv/mpeg2 | 81 | 106 | 124 (x1.2) |
| mkv/h264  | -  | 51  | 193 (x3.8) |
| mkv/vp8   | -  | 12  | 124 (x10.3)|
| mp4/h264  | -  | 51  | 194 (x3.8) |
| avi/mpeg2 | 81 | 106 | 123 (x1.2) |
| avi/h264  | -  | 50  | 185 (x3.7) |
| avi/vp8   | -  | 12  | 115 (x9.6) |
