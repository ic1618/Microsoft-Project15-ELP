[__Back to home__](index.md)

# Design History

From concept to implementation and build...

## Overview

<img src="assets/slide.png" alt="Overview"/>

## Concept

The concept of our system was to train a machine learning model in order to classify sound. A sound classification model would be to detect whether or not there was a gunshot.

### Signal Processing

Trying to detect gunshots directly from sound waveform is hard because it does not give you much information to work with, only amplitude. Hence, we needed to do some signal processing to extract some features from the sound.

Initially we began research by reading papers and watching video lectures in signal processing. All sources of research we used can be found in ["Code and resources used"](coderesources.md).

What we found were two common signal processing techniques in order to analyse sound, the Mel-Frequency Cepstrum Coefficients (MFCCs, on the left below) and the Mel-Spectrogram (on the right below).

<p float="left">
  <img src="assets/mfcc.png" alt="MFCC"/>
  <img src="assets/spectrogram.png" alt="Spectrgram"/>
</p>

Since MFCCs were a smaller representation and most commonly used in audio machine learning for speech and sound classification, we believed it would be a great place to start, and build a dataset on. We also built a dataset with Mel-spectrograms.

### Machine Learning

#### Multi-layer perceptron (MLP)

The multi-layer peceptron is a common machine learning model used for things such as regression or classification, from our knowledge of machine learning we believed this network would not perform well due to its 'global approach' limitation, where all values are passed into the network at once. This will also have an extremely high complexity with the data representation of sounds we are using as we would have to flatten all the 3D arrrays into a single 1D array and input all of this data at once.

#### Convolutional Neural Network (CNN)

CNNs are mainly applied to analyse visual 2D data therefore we do not have to flatten our data like we have to do with MLP. Using this you can classify an image to find whether or not a gunshot is present since is "scans through" the data and looks for patterns, in our case a gunshot pattern. We could use both MFCC or Mel-spectrograms to train this.

#### Recurrent Neural Network (RNN)

A recurrent neural network is a special type of network which can recognise sequencing, and therefore we believed it would work very well in order the detect gunshots. This is because a gunshot typically has an initial impulse and then a trailing echo, an RNN would be able to learn this impulse and trailing echo type scenario and output whether it was a gunshot or something else. This would be trained with MFCCs.

#### Object Detection 

Although usually a larger architecture, object detection would work well in order to detect gunshots from Mel-Spectrograms due to a gunshots unique shape. This means that we can detect whether there is a gunshot present, but also how many gunshots are present as Object Detection won't classify the entire image like a CNN would, it would classify regions of the image.

## Implementation

### The Dataset

**The data we were given was a key factor and had a direct impact in which models worked for us and did not.**

We were given thousands of hours of audio data, each file being 24 hours long. Since we were provided with 'relative' gunshot locations in audio clips, our dataset was very noisy, the time locations we were given usually contained a gunshot within 12 seconds of the given time, and sometimes contained multiple gunshots. Due to the lack of time on this project, it was not realistic to listen to all of the sound clips and manually relabel all our data by ear, also, gunshots are sometimes very hard to distinguish from other rainforests sounds by ear, and many of these other sounds were very new to us. This is why we took a 12 second window in our signal processing, to ensure all of our data contains the gunshot(s). 

Luckily, in our testing of different machine learning techniques, we found an approach to solve the problem of detecting gunshots in noisy data, as well as building a clean dataset for the future!

### CNN with Mel-Spectrogram

Building a simple CNN with only a few convolutional layers, which a dense layer classifying whether there is a gunshot or not, worked quite well, with precision and recall above 80% on our validation sets! However, this method on noisy images did not work well, noisy images being a Mel-spectrogram with a lot of different sounds, such as below. Although it has an OK precision and recall, we cannot guarantee all the gunshots will be the only sounds occuring at once. Below you can see an example of a gunshot which can be detected using a CNN, and a gunshot that cannot be detected using a CNN.

<p float="left">
  <img src="assets/mfc.png" alt="Clear gunshot"/>
  <img src="assets/specrogram.png" alt="Noisy gunshot"/>
</p>

### CNN and RNN with MFCC

This method suffered a similar problem with noise as the [CNN with Mel-Spectrogram](#CNN-with-Mel-Spectrogram) did. However with a clean dataset, we think an RNN with MFCC would work extremely well!


### Object Detection with Mel-Spectrogram

Object Detection won't classify the entire image like a CNN would, it would classify regions of the image, and therefore it can ignore other sound events on a Mel-spectrogram. In our testing we found that object detection worked very well in detecting gunshots on a mel-spectrogram, and could even be trained to detect other sound events such as raindrops hitting the acoustic recorder, monkey alarm calls and thunder!

What this allowed us to do was to also get the extact start and end times of gunshots, and hence automatically building a clean dataset that can be used to train networks in the future with much cleaner data that contains the exact location of these sound events! This method also allowed us to count the gunshots by seeing how many were detected in the 12s window, as you can see below.

<img src="assets/mfc.png" alt="Multi-Gunshots"/>

## Build

### Use of cloud technology

In this project, the use of cloud technology allowed us to speed up many processes, such as building the dataset. We used Microsoft Azure to store our thousands of hours of sound files, and Azure Machine Learning studio to train some of our models, pre-process our data and build our dataset!

#### Storage

In order to store all of our sound files, we used blob storages on Azure. This meant that we could import these large 24 hour audio files into Azure ML studio for building our dataset. Azure ML studio allowed us to create IPYNB notebooks to run our scripts to find the gunshots in the files, extract them and build our dataset.

<img src="assets/mfc.png" alt="Blob storage"/>

#### Data labelling

Azure ML studio also provided us with a Data Labelling service where we could label our Mel-spectrograms for gunshots and build our dataset to train our object detection models. These object detection models (Yolov4 and Faster-RCNN) use XML files in training, Azure ML studio allows us to export our labelled data in a  COCO format in a JSON file. The conversion from COCO to the XML format we needed to train our models was done with ease.

<img src="assets/mfc.png" alt="Data Labelling"/>

### Custom Vision

The Custom Vision model is the simplest model of the three to train. We did this by using [Azure Custom Vision](https://customvision.ai), it allowed us to upload images, label the images and train models with no code at all!

### Yolov4
👷‍♂️

### Faster-RCNN
👷‍♂️
