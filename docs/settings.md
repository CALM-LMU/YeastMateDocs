# Settings

All settings come with a default preset with standard values. You can add new presets if you wish to save different settings for your different datasets. While the default preset will be reset everytime you start YeastMate, new presets will be saved and will still be there the next time you start YeastMate again.

## Detection settings

This page contains the various settings for the detection backend:

* If you are running the detection backend on a separate server than the user interface, you can set the respective IP adress and port.

* YeastMate detects objects on a non-fluorescent overview channel. If your images have multiple channels, check this setting and set the channel to detect on.

* YeastMate performs detection on single-plane images. If your image is a z-stack, check this setting, and select where a single plane will be taken from the stack (e.g. 50% for the middle slice).

* If you wish to detect objects in a time-series, you can set the detection to be done on the first or last frame of your stack. If you wish to detect on every frame separately, please split your stack into single frames first.

## Advanced detection settings

Flip this switch to access advanced settings for the detection:

* YeastMate is trained on images acquired with a pixel size of 110nm. If this differs from your images, set your pixel size and the images will be rescaled to match the image scale of the model.

* YeastMate automatically performs image normalization on the 1.5-98.5% quantile. This should yield good results for most images, but you can change this here.

* Detected objects are automatically discarded if their score is below 0.9 for single cells and 0.75 for mating and budding events. This should yield generally good results, but if you encounter too many false positives, you can set these thresholds higher, or lower if too many objects are missed.

* If you trained your own model with images with a different pixel size than 110nm, you can set your pixel size here, so that the rescaling of images is done in relation to this pixel size.

## Preprocessing settings

This page contains the settings for preprocessing and alignment of your images. 

YeastMate only supports tif/tiff files for the actual detection. If you have proprietary microscopy images (e.g. Nikon .nd2) or similar that can be openend by Bioformats, YeastMate can automatically convert them into ImageJ-like .tif files. This feature was only tested on Nikon .nd2, and while it should also work for Zeiss, Leica etc. files, you might have to convert your images first in ImageJ if this step fails.

YeastMate can additionally perform alignment of microscopy images taken by two cameras. The different image channels can be assigned to the two cameras and set as reference channels for the alignment. You can also set a channel to be removed after alignment/

If you have time stacks, you can set them to be split into separate frame images. While the detection step can handle time steps, if you want to perform detection on every frame separately, you can split them here.

If you don't need to align your images, and you already have ImageJ-compatible tif images, you can skip the preprocessing step. 

## Export settings

The detection job saves its results as a segmentation mask and a json file containing additional metadata. This page contains the settings if you wish to crop objects in your images and masks. Cropped masks will only contain labelled cells from the cropped object.

Further settings include:

* YeastMate will save the bounding boxes of the detected objects exactly around the respective segmentation. You can set a static crop size for all objects.

* If you wish to instead just scale your size of the crop by a factor, you can set this factor here. As it will automatically crop exactly around the object, this setting can make the crops nicer.

* YeastMate can save crops of the detected objects of the original image and the segmentation mask. This can be set for each class separately, and also customized if you have different classes from your retrained network.
