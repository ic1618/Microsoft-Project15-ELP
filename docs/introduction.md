[__Back to home__](index.md)

# Introduction

## Context

The Elephant Listening Project (ELP) began in 2000, our client Peter Howard Wrege took over in 2007 as director https://elephantlisteningproject.org/.

ELP focuses on helping protect one of three types of elephants, the forest elephant which has a unique lifestyle and is adapted to living in dense vegetation such as the forest. They depend on fruits found in the forest and are known as the architect of the rainforest since they disperse seeds all around the forest. 

Since they spend their time in the forest it is extremely hard to track them since the canopy of the rainforest is so thick, you cannot see the forest floor, so ELP use an acoustic recorder to record vocalisations of the elephants to track them. Currently they have put one acoustic recorder per 25 square kilometre. These devices can detect elephant calls in a 1km radius and gunshots 2-2.5km radius around each recording site.

![image](https://user-images.githubusercontent.com/48328956/123100837-5f26e980-d42b-11eb-9a89-f2896160c685.png)

The dots on above show the location of the various acoustic recorders. Currently the recordings are recorded to an SD card, and then collection from all the sites takes a total of 21 days in the forest. This happens every 4 months.

Once all the data is collected it goes through a simple ‘template detector’ which has 7 examples of gunshot sounds, cross correlation analysis is carried out, locations in the audio file with a high correlation get flagged as a gunshot.

The problem with the simple cross correlation method is that it produces an extremely large amount of false positives, such as tree branch falls and even things as simple as raindrops hitting the recording device. This means that there is a 15-20 day analysis effort, however it is predicted that with a better detector, this analysis effort can be cut down to a 2-3 day effort!

Our client wants us to create a detector that is much better at detecting than the simple and inefficient template detector that is currently in place. Their main goal is to make a detector that works really well. This can be achieved using cloud computing and future technology. 

A discussion on recall and precision was had. Currently the client’s detector has an extremely high recall, but a very bad precision (0.5%!!!). The ideal scenario would be to improve the precision, in order to remove these false positives and make sure that when a gunshot is detected, the gunshot is in fact a gunshot (high precision).

The expectation is to have a much better detector than the one in place, that can detect gunshots to a very high precision with a reasonable accuracy. Distinguishing between automatic weapons (eg AK-47) and shotguns is also important, since automatic weapons are usually used to poach elephants. This is an important first step to real time detection.

## Our solution

We provide three models with different features for the client to run. Our strongest model Faster R-CNN  fulfils all our clients expectations, you can see the concept to implementation and build in [Design History.](designhistory.md)
