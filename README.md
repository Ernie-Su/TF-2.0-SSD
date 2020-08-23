# Brief Log of SSD processing
## Data Augmentation

[2020-08-23] training time = 102 minutes, pretrained weight = ssd_model.h5, input = 2092 images, loss = 0.778, val_loss = 0.975

## Switch from Tensorflow Object Detection API to TF2 SSD

[2020-08-21] Changed class labels from 5 to 1, tried to get higher accuracy. Accuarcy seemed increased, but was still very low(conf_thred=1e-3).

[2020-08-18] Changed image size from 512 to 300, finally got rid of errors. Started to train ssd from scratch. Training succeed but got negligible accuarcy(conf_thred=3e-5).

[2020-08-16] Got errors because of input dimension imcompatibility. Found https://github.com/bubbliiiing/ssd-tf2 .

[2020-08-12] Decided to build a ssd model with tf2.

## Started with Tensorflow Object Detection API

[2020-08-11] Tried tf1.13, tf1.14, tf1.15, and Tensorflow 2.0 Object Detection API with tf2.0, tf2.2. None of them worked.

[2020-08-07] Got lots of errors while running legacy/train.py. Most of them came up due to complex version conflicts.

[2020-08-03] Started to deal with ssd with online Tensorflow Object Detection API tutorials.

## Get Image Set

[2020-08-02] Used LabelImg to do the annotation.

[2020-07-31] Took 523 pictures of me riding on uBike.
