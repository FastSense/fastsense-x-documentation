# Converting models

## Converting to OpenVINO

To use MYRIADs or Intel GPU, one needs to convert a model to the OpenVINO compatible format.  
It consists of two files: `.bin` and the `.xml` one. Also there sometimes is `.mapping` file, but we aren't going to need that.

Intel provides us with an OpenVINO conveter called `model_optimizer`. It is capable of converting models from TensoFlow, Caffe, ONNX and a few other frameworks into its own format. The easiest way to run `model_optimizer` is to use docker `openvino/ubuntu18_dev`.
To run the docker container, use the following command:

```bash
docker run --rm -it \
-v /etc/timezone:/etc/timezone:ro \
-v /etc/localtime:/etc/localtime:ro \
-v "$(pwd):/input" openvino/ubuntu18_dev
```

Your current working directory will be mounted to `/input` path.

Let's say your model is stored in the diretory from which docker was run: `/input/model.onnx`. Then to convert it to openvino, simply run:

```bash
python3 deployment_tools/model_optimizer/mo.py \
--input_model /input/model.onnx \
--model_name model_fp16 \
--data_type FP16 \
--output_dir /input/
```

This will create files `model_fp16.bin` and `model_fp16.xml` in your working directory.

To use `model_optimizer` with PyTorch, first export the model to onnx as shown [here](https://pytorch.org/tutorials/advanced/super_resolution_with_onnxruntime.html). With TensorFlow it can be used directly as shown [here](https://docs.openvinotoolkit.org/latest/openvino_docs_MO_DG_prepare_model_convert_model_Convert_Model_From_TensorFlow.html), or agian through onnx proxy, using [tf2onnx](https://github.com/onnx/tensorflow-onnx).

## Converting to tflite

To use Google Coral TPU, one needs to export the model to the tflite format. It is a procedure which requires multiple steps:

First, the model needs to be quantized so it can be run in the `int8` precision. This process is fully described [here](https://www.tensorflow.org/lite/performance/post_training_quantization).

```python
import tensorflow as tf
converter = tf.lite.TFLiteConverter.from_saved_model(saved_model_dir)
converter.optimizations = [tf.lite.Optimize.DEFAULT]
converter.representative_dataset = representative_dataset
tflite_quant_model = converter.convert()
```

You will also need a couple of hundreds of images as `representative_dataset` to make all tensors scaled properly inside the model, so that the convertion to `int8` does not harm model accuracy too much.

Second, you need to run `edgetpu_compiler` on the saved quantised model. The installation and usage is described [here](https://coral.ai/docs/edgetpu/compiler/#download). A typical command looks like:

```bash
edgetpu_compiler model_quant.tflite model_quant_edgetpu.tflite
```

[Here](https://github.com/google-coral/edgetpu/tree/master/test_data) you can find a set of already compiled models.

### PyTorch to tflite

It is possible to convert even PyTorch models to tflite. But there is one trick: tflite only supports `NHWC` (a.k.a. channels last) image format and PyTorch only supports `NCHW` (a.k.a. channels first) format. To overcome that, you first need to convert your model to openvino as described above. Then you can use [this tool](https://github.com/PINTO0309/openvino2tensorflow) to convert from openvino to TensorFlow changing the dimensions ordering. Then the model can be exported to tflite just like any other TensorFlow model.

This might look tricky, but this was successfully done for exemple with person Re-Identification model, which is [available](https://nnio.readthedocs.io/en/latest/zoo.html#nnio.zoo.edgetpu.reid.OSNet) in nnio.
