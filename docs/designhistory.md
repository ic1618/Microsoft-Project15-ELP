[__Back to home__](index.md)

# Design History

From concept, implementation and build...

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

#### Multi-layer perceptron

The multi-layer peceptron is a common machine learning model used for things such as regression or classification, from our knowledge of machine learning we believed this network would not perform well due to its 'global approach' limitation, where all values are passed into the network at once. This will also have an extremely high complexity with the data representation of sounds we are using.

#### Convolutional Neural Network (CNN)

#### Recurrent Neural Network (RNN)

A recurrent neural network is a special type of network which can recognise sequencing, and therefore we believed it would work very well in order the detect gunshots. This is because a gunshot typically has an initial impulse and then a trailing echo, an RNN would be able to learn this impulse and trailing echo type scenario and output whether it was a gunshot or something else.

#### Object Detection 


