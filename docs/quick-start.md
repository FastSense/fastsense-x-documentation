# Bring Up

Check you have our FastSenseX platform, Corals, Myriads and WIFI...

# Docker setup

Install Docker from the [instructions](https://docs.docker.com/engine/install/ubuntu/).

Pull our docker image:
```
docker pull fastsense/ros_ai
```

> Если расширять данный шаг, то можно повзаимоствовать [отcюда](https://github.com/FastSense/edge_ai_demo/blob/main/docker/README.md).

# Run your first demo

Manually crate a container:
```
docker run -it -v / dev /: / dev / --net = host --privileged fastsense / ros_ai / bin / bash
```

Upgrade [NNIO](https://nnio.readthedocs.io/en/latest/):
```
pip3 install -U nnio
```

## The simplest example

```
# Простейший пример инференса на примере ssd mobilenet на сохранённой картинке

# Вставить простой пример будет правильнее, т. к. для запуска Edge AI Demo сразу
# нужно будет сделать слишком много шагов для получения первого результата
# (Подключить Realsense, например), а также иметь набор из пяти девайсов.

import nnio
import cv2

# Load model
model = nnio.zoo.edgetpu.detection.SSDMobileNet(device='TPU') # TBD Framework description

# Get preprocessing function
preproc = model.get_preprocessing()

input_image = cv2.imread('TBD path')

# Preprocess your numpy image
image = preproc(image_rgb)

# Make prediction
boxes = model(image)

# TBD some text output with cv2.imshow(...)
```

## What's next?

Try to run our [__Edge AI Demo__](https://github.com/FastSense/edge_ai_demo), in which five neural networks are launched in parallel in [ROS](http://wiki.ros.org/Documentation) to process the video stream from two cameras.

Look at the ready to launch on the edge devices networks from the [__NNIO Model Zoo__](https://nnio.readthedocs.io/en/latest/zoo.html).