**WIP**

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
    img = cv.imread('004545.jpg')
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
| MobileNet-SSD | TensorFlow >= 1.4 | [weights](http://download.tensorflow.org/models/object_detection/ssd_mobilenet_v1_coco_2017_11_17.tar.gz) | |
| Inception v2 SSD | TensorFlow >= 1.4 | [weights](http://download.tensorflow.org/models/object_detection/ssd_inception_v2_coco_2017_11_17.tar.gz) | [config](https://github.com/opencv/opencv_extra/tree/master/testdata/dnn/ssd_inception_v2_coco_2017_11_17.pbtxt) |
| MobileNet-SSD | TensorFlow < 1.4 | [weights](http://download.tensorflow.org/models/object_detection/ssd_mobilenet_v1_coco_11_06_2017.tar.gz) | [config](https://github.com/opencv/opencv_extra/blob/master/testdata/dnn/ssd_mobilenet_v1_coco.pbtxt) |



### Get a text graph representation
You can use the following script to make a text graph representation. It removes weights nodes and some unused fields.

```python
import tensorflow as tf

# Read the graph.
with tf.gfile.FastGFile('graph.pb') as f:
    graph_def = tf.GraphDef()
    graph_def.ParseFromString(f.read())

# Remove Const nodes.
for i in reversed(range(len(graph_def.node))):
    if graph_def.node[i].op == 'Const':
        del graph_def.node[i]
    for attr in ['T', 'data_format', 'Tshape', 'N', 'Tidx', 'Tdim',
                 'use_cudnn_on_gpu', 'Index', 'Tperm', 'is_training',
                 'Tpaddings']:
        if attr in graph_def.node[i].attr:
            del graph_def.node[i].attr[attr]

# Save as text.
tf.train.write_graph(graph_def, "", "graph.pbtxt", as_text=True)
```
### Generate a config file
Run `optimize_for_inference.py` tool to make your model simpler:
```bash
python ~/tensorflow/tensorflow/python/tools/optimize_for_inference.py \
  --input frozen_inference_graph.pb \
  --output opt_graph.pb \
  --input_names image_tensor \
  --output_names "num_detections,detection_scores,detection_boxes,detection_classes" \
  --frozen_graph
```

Run a [graph transformation tool](https://github.com/tensorflow/tensorflow/blob/master/tensorflow/tools/graph_transforms/README.md#using-the-graph-transform-tool) to fuse constant nodes.

Run [tf_text_graph.py]() script. If your model has different values of `num_classes`, `min_scale`, `max_scale`, `num_layers` or `aspect_ratios` comparing to [origin configuration files](https://github.com/tensorflow/models/tree/master/research/object_detection/samples/configs), specify it in the script arguments.

## References
* [TensorFlow library](https://www.tensorflow.org/)
* [COCO dataset](http://cocodataset.org/#home)
* [Google Protobuf](https://developers.google.com/protocol-buffers/)