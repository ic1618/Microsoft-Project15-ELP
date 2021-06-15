[__Back to home__](index.md)

# Design History

From concept, implementation, to build...

## Overview

<img src="assets/slide.png" alt="Overview"/>

## Concept

The concept of our system was to train a machine learning model in order to classify sound. A sound classification model would be to detect whether or not there was a gunshot.

### Signal Processing

Trying to detect gunshots directly from sound waveform is hard because it does not give you much information to work with, only amplitude. Hence, we needed to do some signal processing to extract some features from the sound.

Initially we began research by reading papers and watching video lectures in signal processing. All sources of research we used can be found in ["Code and resources used"](coderesources.md).

What we found were two common signal processing techniques in order to analyse sound, the Mel-Frequency Cepstrum Coefficients (MFCCs, on the left below) and the Mel-Spectrogram (on the right below). Since MFCCs was a smaller representation and most commonly used in audio machine learning for speech and sound classification, we believed it would be a great place to start, and build a dataset on.

<p float="left">
  <img src="assets/mfcc.png" alt="MFCC"/>
  <img src="assets/spectrogram.png" alt="Spectrgram"/>
</p>

