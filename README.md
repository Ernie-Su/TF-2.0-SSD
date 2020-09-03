# Brief Log of My SSD processing

## Use PC as server for ssd inference and Raspberry Pi as client

**[2020-09-03]**

* In order to make the server and client communicate, I started to learn how to use socket in TCP/IP. With socket, I could send the result of ssd model inference(detected class and bounding box vertices) back to Raspberry, which is my socket client. 

***

**[2020-09-02]**

* Implemented a gstreamer pipeline that can capture frames from RPi Camera and send them from RPi to my PC through udp. At first, I got 30fps with an extremely long  delay(15 seconds). 

However, I found there were two main reasons that caused the long delay :

1. The capturing fps on RPi is too high for ssd to inference. I used 40 fps for testing before and forgot to change. Now I use 24 fps for inference.

2. The queue element in gstreamer pipeline delayed a lot. Don't know why I saw a guy on stackoverflow said that adding queue can shorten delay.

***

**[2020-09-01]**

* The OpenCV's python library is built in my general anaconda (base) environment but my cuda and cudnn were installed in my anaconda (tf2.2-gpu) environment. Thus, I downloaded cuda and cudnn in my C:/ to use OpenCV and cuda at the same time. The reason why I didn't do this earlier is that all these cuda, cudnn, tensorflow version conflicts had killed me many many times when I started the project, and also, '''conda install cudatoolkit, cudnn''' in anaconda environment is so convinient.

***

**[2020-08-31]**

* Installed Gstreamer for windows. Uninstalled opencv-python and build OpenCV on Windows because opencv-python was not built with gstreamer.

* It's important to check whether you installed gst-libav or not. I couldn't use avdec_h264 because I didn't check it during installation.

***

## Try to use TensorRT to optimize ssd model

**[2020-08-30]**

* TensorRT doesn't support python API on winodws, so I used google colab, which is built in ubuntu, to install TensorRT on my google drive. The converted TensorRT model is not as convinient as Tensorflow model. After a lot tries, I gave up this solution.

***

**[2020-08-28]**

* Used Jetson Nano to do the conversion of TensorRT. However, conversion cost a lot more memory than model inference. Jetson Nano killed the conversion process due to OOM even after I increased the swapfile to 8G. This made me learned that Jetson Nano has really few memory again.

***

## Use cv2.VideoCapture() as ssd inference input

**[2020-08-26]**

* Used Jetson Nano to predict, got really poor fps of 1.8, also a 5 seconds delay. Used gstreamer pipeline as source.

* Used my ASUS notebook, which has GTX GeForce 1060, to predict and get 30 fps. Used a webcam as source.

* Another error was that the input had to be a square image, otherwise there would be an error related to ssd input shape.

***

## Change PIL to OpenCV

**[2020-08-25]**

* PIL reads an image to an image class, which needs an extra conversion from PIL image class to numpy array for further image process.

* On the other hand, Opencv directly reads a numpy array. It's estimated that PIL conversion makes it slower when comparing the process speed to OpenCV.

Some different points when it comes to converting PIL to OpenCV : 

1. ImageFont and ImageDraw vs. cv2.putText

2. draw.rectangle(receives left **top** coordinates) vs. cv2.rectangle(receives left **bottom** coordinates)

3. draw.textsize vs. cv2.getTextSize

***

## Data Augmentation (Training Succeeded)

* Found the cause of low accuracy of ssd were miss-edited xmls (bounding box's vertices) during the 512 to 300 resize.

* Didn't find it out until I wanted to do data augmentation to increase the accuracy and started to show each image's rotated bounding box. Definitely a Win-Win.

Date       | training time | pretrained weight                | loss  | val-loss | batch    | epoch
---------- | :------------ | :------------------------------- | :---: | :------: | :------- | -----
2020-08-24 | 50 minutes    | ep036-loss0.635-val_loss0.867.h5 | 0.629 | 0.755    | (16, 16) | (20, 40)
2020-08-24 | 60 minutes    | ep069-loss0.778-val_loss0.975.h5 | 0.635 | 0.867    | (8, 8)   | (20, 40)
2020-08-23 | 102 minutes   | ssd_model.h5                     | 0.778 | 0.975    | (8, 16)  | (40, 80)

***

## Switch from Tensorflow Object Detection API to TF2 SSD

**[2020-08-21]**

* Changed class labels from 5(forward, backward, left, right, stop) to 1(cyclist), tried to get higher accuracy. 

* Accuarcy seemed increased, but was still very low(conf_thred=1e-3).

***

**[2020-08-18]**

* Changed image size from 512 to 300, finally got rid of errors. Started to train ssd from scratch. 

* Training succeeded but got poor accuarcy(conf_thred=3e-5).

***

**[2020-08-16]**

* Got errors because of input dimension imcompatibility. 

* Found https://github.com/bubbliiiing/ssd-tf2, which really helped me a lot.

***

**[2020-08-12]**

* Decided to build a ssd model with tf2.

***

## Start with Tensorflow Object Detection API

**[2020-08-11]**

* Tried tf1.13, tf1.14, tf1.15, and Tensorflow 2.0 Object Detection API with tf2.0, tf2.2. None of them worked.

***

**[2020-08-07]**

* Got lots of errors while running legacy/train.py. Most of them came up due to complex version conflicts.

***

**[2020-08-03]**

* Started to deal with ssd with online Tensorflow Object Detection API tutorials.

***

## Get Image Set

**[2020-08-02]**

* Used LabelImg to do the annotation.

***

**[2020-07-31]**

* Took 523 pictures of me riding on uBike.
