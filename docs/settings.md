# Settings

Here be settings

## Train settings

For the normal use case, you can just use YeastMate as is, but in case you need to retrain the network on new data, you can set various hyperparameter of the neural network and its training procedure here.

For more information about the training step check out [Train on your data](./train.md)

## Preprocessing settings

This page contains the settings for preprocessing and alignment of your images. 

YeastMate supports tiff and Nikon ND2 files, with experimental support for other proprietary file format (e.g. Zeiss .czi) that can be read by BioFormats.
ND2 files need to be converted into tiff files first, thus requiring this postprocessing step. 

YeastMate can additionally perform alignment of microscopy images taken by two cameras. The different image channels can be assigned to the cameras and set as reference channels for the alignment.

If you don't need to align your images, and you already have tiff images, you can skip the preprocessing step.

## Detection settings

This page contains the various settings for the detection backend:

* If you are running the detection backend on a separate server than the user interface, you can set the respective IP adress

* YeastMate detects objects on a non-fluorescent overview channel. If your images have multiple channels, you can set the channel to detect on.

* YeastMate is trained on images acquired with XX magnification / XX pixel size. If this differs from your images, setting the factor of difference may boost network performance.

* YeastMate performs detection on single-plane images. If your image is a z-stack you can check this setting, and a single middle slice of your stack will be used for detection.

* If you wish to detect objects in a time-series, you can set the detection to be done on all frames separately, or only on the first or last frame with the result then taken for all frames.

## Export settings

The detection job already saves its results as a segmentation mask and a json file containing additional metadata. This page contains the settings if you wish to further process these results:

* YeastMate will save the bounding boxes of the detected objects exactly around the respective segmentation. You can expand these boxes you wish to set a static bounding box size for all objects.

* YeastMate can save crops of the detected objects of the original image and the segmentation mask. This can be done for each class separately, and also customized if you have different classes from your retrained network.

* If the image is a time-series, YeastMate will save the segmentation masks as stacks as well. This setting allows you to split the time frames your images and masks into separate files.

* YeastMate saves all detected objects, even if their probability score is low, to allow fine-tuning of the results. This setting allows to balance false positives and false negatives.