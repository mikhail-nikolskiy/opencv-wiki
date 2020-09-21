Deep Learning is the most popular and the fastest growing area in Computer Vision nowadays. Since OpenCV 3.1 there is DNN module in the library that implements forward pass (inferencing) with deep networks, pre-trained using some popular deep learning frameworks, such as Caffe. In OpenCV 3.3 the module has been promoted from opencv_contrib repository to the main repository (https://github.com/opencv/opencv/tree/master/modules/dnn) and has been accelerated significantly.

The module has no any extra dependencies, except for libprotobuf, and libprotobuf is now included into OpenCV. 

The supported frameworks:

 * [Caffe](http://caffe.berkeleyvision.org/)
 * [TensorFlow](https://www.tensorflow.org/)
 * [Torch](http://torch.ch/)
 * [Darknet](https://pjreddie.com/darknet/)
 * Models in [ONNX](https://onnx.ai/) format (as the main method to import models from PyTorch and Keras for some cases)

The supported layers:

 * AbsVal
 * Accum
 * AveragePooling
 * BatchNormalization
 * BNLL
 * Concatenation
 * Convolution (1d, 2d, including dilated convolution, 3d)
 * Crop
 * CropAndResize (RCNN-specific layer)
 * Deconvolution, a.k.a. transposed convolution or full convolution
 * DetectionOutput (SSD-specific layer)
 * Dropout
 * Eltwise (+, *, max)
 * ELU
 * Expand
 * Flatten
 * FullyConnected
 * FlowWarp
 * Gather
 * Interpolation
 * LRN
 * LSTM
 * MaxPooling
 * MaxUnpooling
 * Mish
 * MVN
 * NormalizeBBox (SSD-specific layer)
 * Padding
 * Permute
 * Power
 * PReLU (including ChannelPReLU with channel-specific slopes)
 * PriorBox (SSD-specific layer)
 * ReLU
 * Region (for DarkNet models)
 * Reorg
 * Resize
 * RNN
 * ROI Pooling (RCNN-specific layer)
 * Scale
 * Shift
 * ShuffleChannel
 * Sigmoid
 * Slice
 * Softmax
 * Split
 * Swish
 * TanH

You also can write your own [Custom layer](https://docs.opencv.org/master/dc/db1/tutorial_dnn_custom_layers.html).

The module includes some SSE, AVX, AVX2 and NEON acceleration of the performance-critical layers as well as support of CUDA for the most of the layers. There is also constantly-improved Halide backend. OpenCL (libdnn-based) backend is being developed and should be integrated after OpenCV 3.3 release. Here you may find the up-to-date benchmarking results: [[DNN Efficiency|DNN-Efficiency]]

The provided API (for C++ and Python) is very easy to use, just load the network and run it. Multiple inputs/outputs are supported. Here are the examples: https://github.com/opencv/opencv/tree/master/samples/dnn.

There is Habrahabr article describing the module: https://habrahabr.ru/company/intel/blog/333612/ (in Russian).

The following networks have been tested and known to work:

---
#### Image classification
---
##### Caffe
 * [AlexNet](http://dl.caffe.berkeleyvision.org/)
 * [GoogLeNet](http://dl.caffe.berkeleyvision.org/)
 * [VGG](http://www.robots.ox.ac.uk/~vgg/research/very_deep/)
 * [ResNet](https://github.com/KaimingHe/deep-residual-networks)
 * [SqueezeNet](https://github.com/DeepScale/SqueezeNet)
 * [DenseNet](https://github.com/shicai/DenseNet-Caffe)
 * [ShuffleNet](https://github.com/farmingyard/ShuffleNet)
##### TensorFlow
 * [Inception](https://github.com/petewarden/tf_ios_makefile_example)
 * [Inception, MobileNet](https://github.com/tensorflow/models/tree/master/research/slim/nets)
 * [EfficientNet](https://github.com/tensorflow/tpu/tree/master/models/official/efficientnet)
##### Darknet: https://pjreddie.com/darknet/imagenet/
##### ONNX: https://github.com/onnx/models
 * AlexNet
 * GoogleNet
 * CaffeNet
 * RCNN_ILSVRC13
 * ZFNet512
 * VGG16, VGG16_bn
 * ResNet-18v1, ResNet-50v1
 * CNN Mnist
 * MobileNetv2
 * LResNet100E-IR
 * Emotion FERPlus
 * Squeezenet
 * DenseNet121
 * Inception v1, v2
 * Shufflenet
##### Torchvision: https://github.com/pytorch/vision
##### PyTorch Image Models: https://github.com/rwightman/pytorch-image-models
##### [PyTorch EfficientNet](https://github.com/lukemelas/EfficientNet-PyTorch)

---
#### Object detection
---
##### Caffe
 * [SSD VGG](https://github.com/weiliu89/caffe/tree/ssd)
 * [MobileNet-SSD](https://github.com/chuanqi305/MobileNet-SSD)
 * [Faster-RCNN](https://github.com/rbgirshick/py-faster-rcnn)
 * [R-FCN](https://github.com/YuwenXiong/py-R-FCN)
 * [OpenCV face detector](https://github.com/opencv/opencv/tree/master/samples/dnn/face_detector)
##### TensorFlow
 * [SSD, Faster-RCNN and Mask-RCNN from TensorFlow Object Detection API](https://github.com/tensorflow/models/tree/master/research/object_detection)
 * [EAST: An Efficient and Accurate Scene Text Detector](https://github.com/argman/EAST), paper: https://arxiv.org/abs/1704.03155v2
 * [EfficientDet from AutoML](https://github.com/google/automl/), [details](https://github.com/opencv/opencv/pull/17384), paper: https://arxiv.org/abs/1911.09070
##### Darknet
 * [YOLOv2, tiny YOLO, YOLOv3, Tiny YOLOv3, YOLOv4, Tiny Yolov4](https://github.com/AlexeyAB/darknet) [original repo](https://github.com/pjreddie/darknet)
##### ONNX: https://github.com/onnx/models
 * TinyYolov2
 * [PyTorch YOLOv3 and YOLOv3-tiny](https://github.com/ultralytics/yolov3) 
 * [PyTorch SSD VGG](https://github.com/amdegroot/ssd.pytorch) (using this [pull request](https://github.com/amdegroot/ssd.pytorch/pull/462)): 

---
#### Semantic segmentation
 * [FCN](https://github.com/shelhamer/fcn.berkeleyvision.org) (Caffe)
 * [ENet](https://github.com/e-lab/ENet-training) (Torch)
 * ResNet101_DUC_HDC (ONNX: https://github.com/onnx/models)
 * [DeepLab](https://github.com/tensorflow/models/blob/master/research/deeplab/g3doc/model_zoo.md) (TensorFlow)
 * [UNet, DeepLabV3, FPN from Segmentation Models PyTorch](https://github.com/qubvel/segmentation_models.pytorch)
 * [Unet, UNetPlus, BiSeNet from Human Segmenation PyTorch](https://github.com/thuyngch/Human-Segmentation-PyTorch)

---
#### Pose estimation
 * [OpenPose body and hands pose estimation](https://github.com/CMU-Perceptual-Computing-Lab/openpose) (Caffe)
 * [AlphaPose](https://github.com/MVIG-SJTU/AlphaPose/tree/pytorch) (PyTorch)

---
#### Image processing
 * [Colorization](https://github.com/richzhang/colorization) (Caffe)
 * [Fast-Neural-Style](https://github.com/jcjohnson/fast-neural-style) (Torch)
 * [Style Transfer](https://github.com/onnx/models/tree/master/vision/style_transfer/fast_neural_style) (ONNX)

---
#### Person identification
 * [OpenFace](https://github.com/cmusatyalab/openface) (Torch)
 * [Torchreid](https://github.com/KaiyangZhou/deep-person-reid) (PyTorch)
 * [Face Verification with MobileFaceNet](https://github.com/sirius-ai/MobileFaceNet_TF) (TensorFlow)

---
#### Text detection and Recognition
 * [EasyOCR](https://github.com/JaidedAI/EasyOCR) (PyTorch)
 * [CRNN] (https://github.com/meijieru/crnn.pytorch) (PyTorch)

---
### Depth Estimation
 * [Monodepth2 (PyTorch)](https://github.com/nianticlabs/monodepth2) [details](https://github.com/opencv/opencv/issues/16971)