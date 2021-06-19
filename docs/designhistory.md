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

### The dataset we were provided

### CNN with Mel-Spectrogram

Building a simple CNN with only a few convolutional layers, which a dense layer classifying whether there is a gunshot or not, worked quite well, with precision and recall above 80% on our validation sets! However, this method on noisy images did not work well, noisy images being a Mel-spectrogram with a lot of different sounds, such as below. Although it has an OK precision and recall, we cannot guarantee all the gunshots will be the only sounds occuring at once. Below you can see an example of a gunshot which can be detected using a CNN, and a gunshot that cannot be detected using a CNN.

<p float="left">
  <img src="assets/mfc.png" alt="Clear gunshot"/>
  <img src="assets/specrogram.png" alt="Noisy gunshot"/>
</p>

### CNN and RNN with MFCC



### Object Detection with Mel-Spectrogram
👷‍♂️


## Build

### Use of cloud technology
👷‍♂️

### Custom Vision
👷‍♂️

### Yolov4
👷‍♂️

### Faster-RCNN
👷‍♂️
