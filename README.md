# Brief Log of My SSD processing
## Data Augmentation (Training Succeeded)

* Found the cause of low accuracy of ssd were miss-edited xmls (bounding box's vertices) during the 512 to 300 resize.

* Didn't find it out until I wanted to do data augmentation to increase the accuracy and started to show each image's rotated bounding box. Definitely a Win-Win.

Date       | training time | pretrained weight                | loss  | val-loss | batch    | epoch
---------- | :------------ | :------------------------------- | :---: | :------: | :------- | -----
2020-08-24 | 60 minutes    | ep069-loss0.778-val_loss0.975.h5 | 0.635 | 0.867    | (8, 8)   | (20, 40)
2020-08-23 | 102 minutes   | ssd_model.h5                     | 0.778 | 0.975    | (8, 16)  | (40, 80)

***

## Switch from Tensorflow Object Detection API to TF2 SSD

[2020-08-21] 

* Changed class labels from 5(forward, backward, left, right, stop) to 1(cyclist), tried to get higher accuracy. 

* Accuarcy seemed increased, but was still very low(conf_thred=1e-3).

***

[2020-08-18] 

* Changed image size from 512 to 300, finally got rid of errors. Started to train ssd from scratch. 

* Training succeeded but got poor accuarcy(conf_thred=3e-5).

***

[2020-08-16]

* Got errors because of input dimension imcompatibility. 

* Found https://github.com/bubbliiiing/ssd-tf2, which really helped me a lot.

***

[2020-08-12] 

* Decided to build a ssd model with tf2.

***

## Started with Tensorflow Object Detection API

[2020-08-11] 

* Tried tf1.13, tf1.14, tf1.15, and Tensorflow 2.0 Object Detection API with tf2.0, tf2.2. None of them worked.

***

[2020-08-07] 

* Got lots of errors while running legacy/train.py. Most of them came up due to complex version conflicts.

***

[2020-08-03] 

* Started to deal with ssd with online Tensorflow Object Detection API tutorials.

***

## Get Image Set

[2020-08-02] 

* Used LabelImg to do the annotation.

***

[2020-07-31] 

* Took 523 pictures of me riding on uBike.
