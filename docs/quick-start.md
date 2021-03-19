# Getting Started

## Bring Up

Perform some easy steps for run [Fast Sense X Robotics AI Platform](https://www.fastsense.tech/robotics_ai) (all required accessories are included).

  1. Connect all required devices:
    - **monitor** via miniDP-to-DP adapter;
    - **keyboard** via micro USB B 2.0 to USB A 2.0 jack cable;
    - **mouse** via micro USB B 2.0 to USB A 2.0 jack cable;
    - **usb-wifi stick** via micro USB B 3.0 to USB A 3.0 jack adapter;
    - **power supply** via adapter cable. Power supply should be rated for >30W (for example 12V 3A). Input voltage 7V to 35V are supported.
  2. Wait for a couple of minutes for system boot.
  3. Log in to the system. Default credentials are robot/fastsense (login/password).
  4. Find the WiFi network you are interested in among the available ones and connect to it.

You are ready to continue!

## Docker setup

By default, [Docker](https://docs.docker.com/engine/install/ubuntu/) is already installed on the operating system.

It is highly recommended to run everything inside a [docker container](https://hub.docker.com/r/fastsense/ros_ai) from our [Docker Hub](https://hub.docker.com/u/fastsense).

The container can be started with the following command:

```bash
docker run -it -v /dev/:/dev/ --net=host --privileged fastsense/ros_ai /bin/bash
```

## Run your first demo

Update [NNIO](https://nnio.readthedocs.io/en/latest/):

```bash
pip3 install -U nnio
```

To get started, download the test image:

```bash
wget https://habrastorage.org/webt/bs/26/rf/bs26rf28a9ze_noyyw5jlcylas8.jpeg -O input.jpeg
```

Create a simple python script:

```python
import cv2
import nnio

# Load image
img = cv2.imread('./input.jpeg')

# Load model (For EdgeTPU)
model = nnio.zoo.edgetpu.detection.SSDMobileNet(device='TPU')

# Preprocess your numpy image
preproc = model.get_preprocessing()
img_prep = preproc(img)

# Make prediction
boxes = model(img_prep)

for box in boxes:
    box.draw(input_img)
    print('"%s" detected!' % box.label)

# Save output image
cv2.imwrite('./output.jpeg')
```

Now you can see the image `output.jpeg` with the bounding boxes drawn on it, as well as the output in the terminal of the objects found on the input image.

If you want to run inference on another device, replace the model initialization line:

* `model = nnio.zoo.openvino.detection.SSDMobileNetV2(device='MYRIAD')` for OpenVINO framework;
* `model = nnio.zoo.onnx.detection.SSDMobileNetV1()` for ONNX framework.

## What's next?

Try to run our [__Edge AI Demo__](https://github.com/FastSense/edge_ai_demo), in which five neural networks are launched in parallel in [ROS](http://wiki.ros.org/Documentation) to process the video stream from two cameras.

Some popular models are already built in [nnio](https://nnio.readthedocs.io/). Look at the ready-to-use on the edge devices networks from the [__NNIO Model Zoo__](https://nnio.readthedocs.io/en/latest/zoo.html).

Finally, you can convert your models to run on devices using [Converting models guide](./software-guide/converting.md).
