# NNIO package

[**nnio**](https://nnio.readthedocs.io/en/latest/) is a light-weight python package for easily running neural networks. It was designed specifically fo using with Fast Sense X.

It supports running models on CPU as well the edge devices present on platform:

* [Google Coral Edge TPU](https://coral.ai/)
* Intel integrated GPUs
* [Intel Myriad VPU](https://www.intel.ru/content/www/ru/ru/products/processors/movidius-vpu/movidius-myriad-x.html)

For each device there exists an own library and a model format. We wrap all those in a single well-defined python package.

Look at this simple example:

```python
import nnio

# Create model and put it on a Google Coral Edge TPU device
model = nnio.EdgeTPUModel(
    model_path='path/to/model_quant_edgetpu.tflite',
    device='TPU',
)
# Create preprocessor
preproc = nnio.Preprocessing(
    resize=(224, 224),
    batch_dimension=True,
)

# Preprocess your numpy image
image = preproc(image_rgb)

# Make prediction
class_scores = model(image)
```

More info can be found at the [**documentation page**](https://nnio.readthedocs.io/en/latest/) and the [**GitHub repository**](https://github.com/FastSense/nnio).
