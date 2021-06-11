[__Back to home__](index.md)

# Meeting Minutes

## 27/04/2021

### Agenda:
1.	Write single page A4 summary of meeting with client 
2.	Technical questions we may need to ask Microsoft:
- Azure ML Studio (no code solution, can convert to spectrogram using this? or feed spectrogram images) vs Azure Notebooks (using keras)
- Custom Vision Azure https://azure.microsoft.com/en-gb/services/cognitive-services/custom-vision-service/, https://www.customvision.ai/ 
- Migrating the MS Teams dataset (from Peter) from Cornell to Azure storage
- Azure cloud storage and passes them to Azure Video Indexer to obtain quick insights into a video.
3.	Technical questions we have amongst ourselves
- Splitting and labelling dataset (pydub)
- Spectrogram (use python lib) 
- Using convolutional neural network (CNN) and other computer vision techniques
4.	Check everyone is up to date on using Azure services, and has been added to the subscription

### Minutes:

1.	Write a single page – done, checked, all good 
2.	Set up recurring meeting with Microsoft and Client at 5.30pm on Thursdays
3.	Spectrogram – use librosa for mfcc, scipy uses multiple Fourier transforms but mfcc uses other method
4.	Everyone can see the subscription   

### Questions for Microsoft: 

-	Notebook vs Running a project file – best way to run python project other than using notebook on Azure
-	How to transfer the dataset from box?
-	 Good azure tools for splitting up the audio files in order to use for testing, extracting certain audio from the files for the test set. Aka can there be an automation on Azure somewhere, to go through files and run a python script?
-	We are comfortable with the machine learning side; the main thing will be the pre-processing of the data.

## 28/04/2021

### Agenda

1.	Set up a meeting with the IC supervisor for next week - signal processing for machine learning research
2.	Any useful resources people have found
3.	Benefits of RNN and MFCC

### Minutes
1.	Spectrograms are visual representations of the frequency and amplitude of sound over a specified span of time, and are constructed from an array of frequencies. 
2. use Librosa, an open-source Python library known for its convenience and versatility in audio analysis and manipulation. Librosa allows us to pass our samples to a function that would then compute the appropriate Fourier transforms needed to compose a valid spectrogram.
3.	Spectrogram vs Mel-Spectrogram vs MFCC, we can ask Wei Dai what he thinks. https://medium.com/prathena/the-dummys-guide-to-mfcc-aceab2450fd
4.	The advantage of MFCC is that it is good in error reduction and able to produce a robust feature when the signal is not affected by noise. SVD/PCA technique is used to extract the important features out of the B-Distribution representation.
5. Reason to choose RNN is it takes time into account, we can test it out.
6. Toughest part is the data processing and splitting and forming a good dataset

## 29/04/2021

### Agenda

1. Discussion 
2. Meet with Microsoft

### Minutes

1. Custom Vision – a tool to create custom computer vision models, very simple and only for images
2. Notebook vs Running a project file – best way to run python project other than using notebook, https://docs.microsoft.com/en-us/azure/machine-learning/tutorial-1st-experiment-sdk-train
3. Training is good on Azure ML Studio deployment on container
4. Hosting only supports GPU, need KB to host it, instead we can publish it on container instances, good for training not good for hosting
5. https://docs.microsoft.com/en-us/azure/machine-learning/how-to-train-keras
6. Make sure we close the instances it’ll cost more
7. Batch and real time inferences (real time straight away response), batch you have to wait until you get a certain amount of values, batch can be done with ML compute and you can use GPU. Good for us because its every 4 months as a batch (using AKS).
8. Data migration from Cornell to Azure:
  - https://docs.microsoft.com/en-us/azure/storage/files/storage-how-to-create-file-share?tabs=azure-portal
  - https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-blobs-upload?toc=/azure/storage/blobs/toc.json
