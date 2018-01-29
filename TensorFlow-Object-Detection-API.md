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

## References
* [TensorFlow library](https://www.tensorflow.org/)
* [COCO dataset](http://cocodataset.org/#home)