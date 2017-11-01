### Building OpenCV with MediaSDK support
1. Install MediaSDK
2. Make sure corresponding environment variable is set, Windows: INTELMEDIASDKROOT, Linux: MFX_HOME
3. Build with `-DWITH_MFX` option turned on:
    ```.cpp
    cmake -DWITH_MFX=ON <path-to-opencv-sources>
    cmake --build .
    ```
### Decoding
Media containers are not supported yet, so it is only possible to decode raw video stream stored in a file. It can be extracted from a container manually using the FFmpeg tool ([source1](https://stackoverflow.com/questions/19300350/extracting-h264-raw-video-stream-from-mp4-or-flv-with-ffmpeg-generate-an-invalid), [source2](https://superuser.com/questions/678897/extract-hevc-bitstream-with-ffmpeg)) or any other tools:
```.sh
# H264
ffmpeg -i video.avi -vcodec copy -an -bsf:v h264_mp4toannexb video.264
# H265
ffmpeg -i in.mkv -c:v copy -bsf hevc_mp4toannexb out.h265
```

Then you can use [VideoCapture](https://docs.opencv.org/master/d8/dfe/classcv_1_1VideoCapture.html) object to decode the resulting file:
```.cpp
VideoCapture cap(“video.264”, CAP_INTEL_MFX);
```
**Note!** 
The file extension is important, because it will be used to [determine](https://github.com/opencv/opencv/blob/ec2409157857a5dabf159e6c052ec001e7110bf5/modules/videoio/src/cap_mfx_reader.cpp#L21-L31) the codec. It can be one of `.264`, `.h264`, `.mp2`, `.mpeg2`, `.265` or `.hevc`.

### Encoding
Use the [VideoWriter](https://docs.opencv.org/master/dd/d9e/classcv_1_1VideoWriter.html) object:
```.cpp
int fourcc = VideoWriter::fourcc('H', '2', '6', '4');
VideoWriter writer(filename, CAP_INTEL_MFX, fourcc, fps, frameSize, isColor);
```
Where `fourcc` can be one of `MPG2`, `H264`, `X264`, `AVC `, `H265` or `HEVC`.
