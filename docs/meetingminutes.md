[__Back to home__](index.md)

# Meeting Minutes

Overview of KEY decisions taken:
- Signal Processing method, Spectrogram vs MFCC, [1](# 28/04/2021), [2](# 30/04/2021)
- Classification vs Object Detection [3](25/05/2021)

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
3.	Spectrogram vs Mel-Spectrogram vs MFCC, we can ask IC supervisors opinion. https://medium.com/prathena/the-dummys-guide-to-mfcc-aceab2450fd
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

## 30/04/2021

### Agenda
1.	Look at the data and how we will label it

### Minutes
1. Met up, set up the notebook to see how it works and uploaded a dataset to test it out
2. MFCC not very good with noisy signals but we will test it out, all of us to watch this series https://www.youtube.com/playlist?list=PLhA3b2k8R3t2Ng1WW_7MiXeh1pfQJQi_P

## 01/04/2021

### Agenda:
1.	Look through code Yiming made for MFCC - periodogram 
2.	Compare against spectrogram

### Minutes:
1.	Extract key data from signals and put it into a json file, the y axis to x axis and the energy somehow to y axis. 
2.	Think we can only generate a periodogram from the time series signal, when you move to MFCC you cannot really generate a periodogram since you have 3D graph, time, frequency and amplitude.
3. Can use scipy.signal.periodogram if we wanted a periodogram representation.
4.	Kapre doing same thing as our current MFCC extractor, all good

## 4/05/2021

### Agenda:

1.	Discuss the feature engineering and the features we can extract from our data, can we use the non cepstrum values i.e. the graph, normalise it and then use a CNN
2.	Look at the MLP model
3.	Discuss how to prevent false positives

### Minutes:
1.	We have got new data, different types of gunshots, can use that for classification and see how well using MFCC to classify it goes
2.	Figuring out who to import blob storage to Azure ML studio

## 6/05/2021

### Agenda:

1.	Look at the classifier we made for the different gun types
2.	Look at the CNN we made for gunshot detection, made two, one using the values but means everything has to be the same length audio clip, and other one is generate the PNG images and then reimport and convert to array of certain size.
3.	Decide spectrogram vs cepstrums, can we extract any other features?

Minutes:
1.	Name, sound file, data length, label in csv file
2.	Main task data normalisation – we will try two method, PNG method and data normalisation of the MFCC
3.	We want to split the large 24 hour audio clips into smaller clips, and then pass the data into the model and see what comes up as false positives, when we find this data we want to save that filename and then we can use it for training
4.	Use mounting to get each file, https://docs.microsoft.com/en-us/azure/machine-learning/how-to-train-with-datasets#mount-vs-download through a network drive


## 7/05/2021

### Agenda:
1.	What is everyone doing and what to do next?

### Minutes:

#### What did we accomplish last week?
-	Processing data, loading file, MFCC coefficients + Spectrum
-	Lots of reading 
-	Getting to know the dataset
-	Making small models
#### What will we accomplish this week? by next Thursday
-	Breaking down long files to get false positive data
-	Figuring out how to normalise the MFCC 
-	Brainstorming leaflet ideas
-	Create CSV file for whole dataset (pnnn and eco) file name, duration, sample rate, labels initial: gun or not gun first,  combine dataset into one single CSV file
-	Everyone up to date with the theory
Is anything blocking you?
-	Need to build proper dataset before we can train models in full

## 08/05/2021

### Agenda:
1.	Brainstorming

### Minutes:
 
1.	Produced brainstorm of ideas

## 11/05/2021

### Agenda
1.	Discuss developments of the tasks set on 07/05/2021 
2.	Show the CNN model using spectrogram, suggest as demo
3.	Look through the leaflet/flyer examples together

### Minutes 
1.	Normalising the data will be sound clip length
2.	Meet IC supervisor wednesday 10am
3.	https://www.youtube.com/playlist?list=PL-wATfeyAMNrtbkCNsLcpoAyBBRJZVlnf 10-15 look at pre-processing, save as a JSON file, 
4.	Dynamic time warping as an idea


## 12/05/2021

### Agenda:
1.	Meet with IC supervisor, discuss different methods of audio signal processing, MFCC, Spectrograms etc

### Minutes:
1.	Cloud allows users to access this capability easily, to make this impact broader so more people can sue it around the world, for people who do not have the infrastructure to support all the task, tune it towards this end (developing countries can acknowledge this more easily)
2.	Pipeline of the building blocks, keeping costs down, efficient and economical solution to users
3.	Understand the data we have and the goal we want to achieve
4.	Pre-process the data, cut the sound files into smaller clips, use a method MFCC feature extraction to train a network for the features. Currently we are using a CNN (DL method), store the MFCC in a JSON file, we can use decision tree and SVM which allows us to reduce computer power and costs. Can also use an RNN, LSTM.
5.	 Find a suitable network and find the suitable weightings on the models. Can use transfer learning on our existing model.
6.	Ask Peter (client) if padding the signal is ok (Peter has good background in signals)


## 13/05/2021

### Agenda:
1.	Team discussion
2.	Ask Peter if padding signal is ok for spectrogram and MFCC 
3.	Ask about a recommended frame length
4.	Talk about increase in FN and decrease in FP, causing higher precision, lower recall (may be due to unbalanced dataset)

### Minutes:
1.	Need to find an even split of our data, and generate some more data using data augmentation
2.	Demo’d the CNN and recorded for Peter to watch
3.	We can generate data using time stretching but pitch changing, amplitude changing not as effective

## 14/05/2021

### Agenda:
1.	Discuss JSON generation
2.	Split up tasks, and talk about what the completion of a good training dataset will allow us to start testing models
3.	Talk about good methods of data augmentation
4.	Meet with Peter

### Minutes:
1.	Augmentation: TIMESHIFTING
2.	Pad ecoguns and pnnn guns to 12 seconds, padding on either side, could use white noise or rainforest sounds
3.	Write script to find FP in the meantime (Peter now provided with FP samples)
4.	Overlap the 12s clips of sound for detection
	
## 17/05/2021

### Agenda:
1.	Explain the false positive data
2.	Discuss number of cepstrums in MFCC we want, possibly generate identical training sets with different number of cepstrums

### Minutes:
1.	Added batch normalisation, may normalise when generating 
2.	Added LSTM testing
3.	Overlapping the data to see if it adds some time shifting augmentation

## 18/05/2021

### Agenda:
1.	Work on training the model

### Minutes:
1.	Worked out how to generate the test set using JSON files

## 20/05/2021

### Agenda:
1.	Meet with Microsoft

### Minutes
#### What did you accomplish last week?
1.	Prepared dataset
2.	Tested out different (CNN, LSTM/RNN)
3.	Analysis on the dataset (distribution of test and train data seemed to be different)
4.	RNN 
#### What will you accomplish this week?
1.	Testing different representations of our data (number of MFCC) and seeing what data works well on our models
2.	Standardising our code into .py rather than .ipynb (create functions)
3.	Continue training and testing models

#### Is anything blocking you?
1.	How would Peter prefer the system to run, upload all the data to cloud then run into ML model OR locally process data, then use cloud to determine gunshot or not (full cloud solution vs hybrid solution)

## 21/05/2021

### Agenda
1.	Updates

### Minutes:
1.	Want to change the data representation because we are plateauing at 0.9 precision which will still throw a lot of false positives, therefore we are doing a split of background noise, hard negative, gunshot. 0,1,2.
2.	For tomorrow generate the dataset

## 25//05/2021
### Agenda
1. Re-evaluate the MFCC method
2. Talk about the distribution difference between test and train data, MFCC extremely effected by noise
3. Other options?

### Minutes
1. Deciding on taking an object detection method due to noisy dataset, we can find gunshot 'shape'
2. Tested MFCC when merging train and test data and shuffling, it still trained to background noises!
3. Found Azure data labelling service, also testing out Azure Custom Vision

## 26/05/2021

### Agenda:
1.	Meet and label the data on Azure Data Labelling service

### Minutes:
 
#### What did you accomplish last week?
1.	Tested different representations to see what is best, found that MFCC is not picking up the gunshots properly
2.	Testing object detection techniques using azure custom vision
3.	Drew the bounding boxes for the gunshots
### What will you accomplish this week?
1.	Pre-process data and train yolov3 and see its results
2.	Test out more azure custom vision methods
3.	Continue standardising code

## 01/06/2021

### Agenda:
1. Team discussion
2. Discuss different object detection architectures we are testing

### Minutes:
1.	Want to export the gunshot locations using bbox ratio
2.	Spoke about the custom vision model, and Faster-RCNN model, faster-rcnn slower but better

## 03/06/2021

#### What did you accomplish last week?
1.	Tested and trained our custom vision models (iteration 6, high precision, OK recall)
2.	Labelled lots of data
3.	Built a Faster-RCNN network that works much better (it can detect the difference between ak47/automatic rifle and shotguns. It also knows when something is a mangabey (monkey) alarm call or raindrop.

#### What will you accomplish this week?
1.	Continue testing out the Faster-RCNN model by adding more labels and training data
2.	Testing the F-RCNN model on 24 hour sound clips to see real time performance
Is anything blocking you?

## 09/06/20213

### Minutes
1. Met with Dmitry (Microsoft), told us the use of MFCC could be key, with a smaller sliding window, however our dataset would require manual labelling and time permitting is not possible. 
2. Another solution we proposed is that we can check the bbox coorindates and we know that the lower y value of bbox will not be above a certain value, so we don’t consider it as gunshot (high frequency event will most likely not be a gunshot, they mainly all start from bottom of spectrogram).
3. Our ML solution actually generates more data that can be used in training, and we also generate the bbox with it, this can be used for a more accurate dataset and in the future used to train a 2s sliding window model using MFCC

## 10/06/2021

### Agenda
1. Meet with Microsoft
2. Mention solution of using our model after the current detector runs, therefore we will have all amplitude spike locations, and our model can act as a filter.

### Minutes
1. The first pass could be current detector, and second pass could be our model. 
2. Found that our model doesnt detect every single gunshot when there are multilpe gunshots going off within 0.5 second of eachother, but it will get at least one, usually 33% of the closely packed gunshots from a 12s selection so they are not missed, as the gunshots are essentially overlapping.
3. Our model can detect gunshots which are far away and do not have as big of an amplitude spike which might be missed by first pass
4. Discussed about how we train our model against typical false positives such as raindrops, electrical ticks, thunder, monkey alarm calls.

#### What did you accomplish last week?
1. Tested our models, Yolov4, Faster-RCNN and Custom Vision and compared against Peters detector
2. Labelled lots of data
3. Trained the models against false positives we found it getting

#### What will you accomplish this week?
1. Finish off training the models and continue testing
2. Clean up code and file structure ready for deployment
3. Prepare for the demonstration of our model
