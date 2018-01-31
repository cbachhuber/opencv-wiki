This wiki describes how to work with object detection models trained using [TensorFlow Object Detection API](https://github.com/tensorflow/models/tree/master/research/object_detection).

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
with tf.gfile.FastGFile('frozen_inference_graph.pb') as f:
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
| MobileNet-SSD | TensorFlow >= 1.4 | [weights](http://download.tensorflow.org/models/object_detection/ssd_mobilenet_v1_coco_2017_11_17.tar.gz) | [config](https://gist.github.com/dkurt/45118a9c57c38677b65d6953ae62924a) |
| Inception v2 SSD | TensorFlow >= 1.4 | [weights](http://download.tensorflow.org/models/object_detection/ssd_inception_v2_coco_2017_11_17.tar.gz) | [config](https://github.com/dkurt/opencv_extra/blob/tf_ave_pooling/testdata/dnn/ssd_inception_v2_coco_2017_11_17.pbtxt) |
| MobileNet-SSD | TensorFlow < 1.4 | [weights](http://download.tensorflow.org/models/object_detection/ssd_mobilenet_v1_coco_11_06_2017.tar.gz) | [config](https://github.com/opencv/opencv_extra/blob/master/testdata/dnn/ssd_mobilenet_v1_coco.pbtxt) |

### Generate a config file
Use [tf_text_graph_ssd.py](https://github.com/dkurt/opencv/blob/dnn_tool_ssd_text_graph/samples/dnn/tf_text_graph_ssd.py) script to generate a text graph representation. If your model has different values of `num_classes`, `min_scale`, `max_scale`, `num_layers` or `aspect_ratios` comparing to [origin configuration files](https://github.com/tensorflow/models/tree/master/research/object_detection/samples/configs), specify it in the script arguments.

Try to run the model using OpenCV:

```python
import cv2 as cv

cvNet = cv.dnn.readNetFromTensorflow('frozen_inference_graph.pb', 'graph.pbtxt')

img = cv.imread('example.jpg')
rows = img.shape[0]
cols = img.shape[1]
cvNet.setInput(cv.dnn.blobFromImage(img, 1.0/127.5, (300, 300), (127.5, 127.5, 127.5), swapRB=True, crop=False))
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

### Troubleshooting
If you have problems at `readNetFromTensorflow` or at `forward` stages, perhaps, your model requires some of the following transformations before making a text graph:

1. Try to run `optimize_for_inference.py` tool to make your model simpler:
```bash
python ~/tensorflow/tensorflow/python/tools/optimize_for_inference.py \
  --input frozen_inference_graph.pb \
  --output opt_graph.pb \
  --input_names image_tensor \
  --output_names "num_detections,detection_scores,detection_boxes,detection_classes" \
  --placeholder_type_enum 4 \
  --frozen_graph
```

2. Try fuse constant nodes by a [graph transformation tool](https://github.com/tensorflow/tensorflow/blob/master/tensorflow/tools/graph_transforms/README.md#using-the-graph-transform-tool).

```bash
~/tensorflow/bazel-bin/tensorflow/tools/graph_transforms/transform_graph \
  --in_graph=frozen_inference_graph.pb \
  --out_graph=opt_graph.pb \
  --inputs=image_tensor \
  --outputs="num_detections,detection_scores,detection_boxes,detection_classes" \
  --transforms="fold_constants(ignore_errors=True)"
```

You you have difficulties with your model feel free to ask for help at http://answers.opencv.org.

## References
* [TensorFlow library](https://www.tensorflow.org/)
* [COCO dataset](http://cocodataset.org/#home)
* [Google Protobuf](https://developers.google.com/protocol-buffers/)