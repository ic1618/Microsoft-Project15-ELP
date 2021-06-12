[__Back to home__](index.md)

# How to run

Once you have completed the [Getting Started](gettingstarted.md) step, you are now ready to run the detector on sound clips!

## Choosing the clips for detection

In the model files, there should be a folder called 'sounds', if not then simply create one in the main directory. The reason it may not be there is because sometimes sites like Github remove empty folders from projects. 

This 'sounds' folder is there to put the clips in that you want to detect!

The way the detector is designed is you can put multiple clips (at least 12s each) into the 'sounds' folder, then run the detector which would then detect the gunshots within each of those clips and generate a csv file of the results.

Putting in a 24 hour clip will scan through the whole 24 hours, it would work the same with a 1 hour, 2 hour or 10 minute clip.

IMPORTANT: the detector works in 12 second chunks, so the clips have to be minimum 12 seconds long, and preferably multiples of 12 seconds, but when it comes to longer clips it doesn't necessarily need to be a multiple of 12 seconds (i.e may be too hard, or you dont mind if the last x seconds (less than 12) will be cut off.

### For Faster-RCNN 

You should have the folders below:

<img src="assets/folders.png" alt="Folders" width="400"/>

### For Yolov4

You should have the folders below:

<img src="assets/yolofolders.png" alt="Folders" width="400"/>

### For Custom Vision

You should have the folders below:

<img src="assets/cvfolders.png" alt="Folders" width="400"/>

## Running the detector
