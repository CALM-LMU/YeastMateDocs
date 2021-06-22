# How to use the YeastMate user interface
Normal pages
## Job dashboard

Here you can see what tasks are running right now

## Start a new job

Here you can start a new task.

## Correct and label your images


## Retrain your network

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

Here you tune this

## Export settings

Here you can set how to export your results.