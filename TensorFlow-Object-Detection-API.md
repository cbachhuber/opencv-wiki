This wiki describes how to work with object detection models trained using [TensorFlow Object Detection API](https://github.com/tensorflow/models/tree/master/research/object_detection). OpenCV 3.4.1 or higher is required.

## Run network in TensorFlow
Deep learning networks in TensorFlow are represented as graphs where an every node is a transformation of it's inputs. They could be common layers like `Convolution` or `MaxPooling` and implemented in C++. Custom layers could be built from existing TensorFlow operations in python.

TensorFlow object detection API is a framework for creating deep learning networks that solve object detection problem. There are already trained models in [Model Zoo](https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/detection_model_zoo.md). You can build you own model as well.

The result of training is a binary file with extension `.pb` contains both topology and weights of trained network. You may download one of them from Model Zoo, in example `ssd_mobilenet_v1_coco` (MobileNet-SSD trained on COCO dataset).

Create and run a python script to test a model on specific picture:
```python
import numpy as np
import tensorflow as tf
import cv2 as cv

# Read the graph.
with tf.gfile.FastGFile('frozen_inference_graph.pb', 'rb') as f:
    graph_def = tf.GraphDef()
    graph_def.ParseFromString(f.read())

with tf.Session() as sess:
    # Restore session
    sess.graph.as_default()
    tf.import_graph_def(graph_def, name='')

    # Read and preprocess an image.
    img = cv.imread('example.jpg')
    rows = img.shape[0]
    cols = img.shape[1]
    inp = cv.resize(img, (300, 300))
    inp = inp[:, :, [2, 1, 0]]  # BGR2RGB

    # Run the model
    out = sess.run([sess.graph.get_tensor_by_name('num_detections:0'),
                    sess.graph.get_tensor_by_name('detection_scores:0'),
                    sess.graph.get_tensor_by_name('detection_boxes:0'),
                    sess.graph.get_tensor_by_name('detection_classes:0')],
                   feed_dict={'image_tensor:0': inp.reshape(1, inp.shape[0], inp.shape[1], 3)})

    # Visualize detected bounding boxes.
    num_detections = int(out[0][0])
    for i in range(num_detections):
        classId = int(out[3][0][i])
        score = float(out[1][0][i])
        bbox = [float(v) for v in out[2][0][i]]
        if score > 0.3:
            x = bbox[1] * cols
            y = bbox[0] * rows
            right = bbox[3] * cols
            bottom = bbox[2] * rows
            cv.rectangle(img, (int(x), int(y)), (int(right), int(bottom)), (125, 255, 51), thickness=2)

cv.imshow('TensorFlow MobileNet-SSD', img)
cv.waitKey()
```
![](https://user-images.githubusercontent.com/25801568/35504975-a5db962c-04f5-11e8-9a9f-1d803f86af7f.png)

## Run network in OpenCV
OpenCV needs an extra configuration file to import object detection models from TensorFlow. It's based on a text version of the same serialized graph in protocol buffers format (protobuf).

### Use existing config file for your model
You can use one of the configs that has been tested in OpenCV. Choose it depends on your model and TensorFlow version:

| Model | Version | ||
|-------|-------------|----|----|
| MobileNet-SSD v1 | 2017_11_17 | [weights](http://download.tensorflow.org/models/object_detection/ssd_mobilenet_v1_coco_2017_11_17.tar.gz) | [config](https://github.com/opencv/opencv_extra/blob/master/testdata/dnn/ssd_mobilenet_v1_coco_2017_11_17.pbtxt)
| MobileNet-SSD v1 PPN | 2018_07_03 | [weights](http://download.tensorflow.org/models/object_detection/ssd_mobilenet_v1_ppn_shared_box_predictor_300x300_coco14_sync_2018_07_03.tar.gz) | [config](https://github.com/opencv/opencv_extra/blob/master/testdata/dnn/ssd_mobilenet_v1_ppn_coco.pbtxt)
| MobileNet-SSD v2 | 2018_03_29 | [weights](http://download.tensorflow.org/models/object_detection/ssd_mobilenet_v2_coco_2018_03_29.tar.gz) | [config](https://github.com/opencv/opencv_extra/blob/master/testdata/dnn/ssd_mobilenet_v2_coco_2018_03_29.pbtxt)
| Inception-SSD v2 | 2017_11_17 | [weights](http://download.tensorflow.org/models/object_detection/ssd_inception_v2_coco_2017_11_17.tar.gz) | [config](https://github.com/opencv/opencv_extra/blob/master/testdata/dnn/ssd_inception_v2_coco_2017_11_17.pbtxt)
| Faster-RCNN Inception v2 | 2018_01_28 | [weights](http://download.tensorflow.org/models/object_detection/faster_rcnn_inception_v2_coco_2018_01_28.tar.gz) | [config](https://github.com/opencv/opencv_extra/blob/master/testdata/dnn/faster_rcnn_inception_v2_coco_2018_01_28.pbtxt)
| Faster-RCNN ResNet-50 | 2018_01_28 | [weights](http://download.tensorflow.org/models/object_detection/faster_rcnn_resnet50_coco_2018_01_28.tar.gz) | [config](https://github.com/opencv/opencv_extra/blob/master/testdata/dnn/faster_rcnn_resnet50_coco_2018_01_28.pbtxt)
| Mask-RCNN Inception v2 | 2018_01_28 | [weights](http://download.tensorflow.org/models/object_detection/mask_rcnn_inception_v2_coco_2018_01_28.tar.gz) | [config](https://github.com/opencv/opencv_extra/blob/master/testdata/dnn/mask_rcnn_inception_v2_coco_2018_01_28.pbtxt)


### Generate a config file
Use one of scripts which generate a text graph representation for a frozen `.pb` model depends on it's architecture:
* [tf_text_graph_ssd.py](https://github.com/opencv/opencv/blob/master/samples/dnn/tf_text_graph_ssd.py)
* [tf_text_graph_faster_rcnn.py](https://github.com/opencv/opencv/blob/master/samples/dnn/tf_text_graph_faster_rcnn.py)
* [tf_text_graph_mask_rcnn.py](https://github.com/opencv/opencv/blob/master/samples/dnn/tf_text_graph_mask_rcnn.py)

Pass a [configuration file](https://github.com/tensorflow/models/tree/master/research/object_detection/samples/configs) which was used for training to help script determine hyper-parameters.

```
python tf_text_graph_faster_rcnn.py --input /path/to/model.pb --config /path/to/example.config --output /path/to/graph.pbtxt
```


Try to run the model using OpenCV:

```python
import cv2 as cv

cvNet = cv.dnn.readNetFromTensorflow('frozen_inference_graph.pb', 'graph.pbtxt')

img = cv.imread('example.jpg')
rows = img.shape[0]
cols = img.shape[1]
cvNet.setInput(cv.dnn.blobFromImage(img, size=(300, 300), swapRB=True, crop=False))
cvOut = cvNet.forward()

for detection in cvOut[0,0,:,:]:
    score = float(detection[2])
    if score > 0.3:
        left = detection[3] * cols
        top = detection[4] * rows
        right = detection[5] * cols
        bottom = detection[6] * rows
        cv.rectangle(img, (int(left), int(top)), (int(right), int(bottom)), (23, 230, 210), thickness=2)

cv.imshow('img', img)
cv.waitKey()
```

![](https://user-images.githubusercontent.com/25801568/35520173-58e6f99c-0527-11e8-80fc-8a32d1923e04.png)

## References
* [TensorFlow library](https://www.tensorflow.org/)
* [COCO dataset](http://cocodataset.org/#home)
* [Google Protobuf](https://developers.google.com/protocol-buffers/)
* OpenCV object detection sample: [C++](https://github.com/opencv/opencv/blob/master/samples/dnn/object_detection.cpp), [Python](https://github.com/opencv/opencv/blob/master/samples/dnn/object_detection.py)
* [OpenCV Mask R-CNN sample](https://github.com/opencv/opencv/blob/master/samples/dnn/mask_rcnn.py)