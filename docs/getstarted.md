# How to use the YeastMate user interface

After installing YeastMate (and potentially setting up the Docker detection container), you can get right to processing your images by opening the user interface. It should open a terminal for the backend in the background, or two separate instances if you are using the local detection backend. If these are not opening or closing instantly, you can file a bug report [here](https://github.com/CALM-LMU/YeastMate/issues)

## Job dashboard

This page shows all currently queued and running tasks.

## Starting a new detection job

To start detecting on your images, click ```Start detection job``` in the sidebar.
From here you can start your inference jobs for a given path containing your images. You can only include or exclude specific files by setting their respective tags.

[screenshot]
[explain options of submit a new job]



### Input data format

YeastMate expects the input folder to contain TIFF files or a folder called ```yeastmate-preprocessed``` containing TIFF files. We support multiple channels or timepoints in files, in which case the dimension order should be TZCYX (default for TIFF images saved by ImageJ/Fiji). If the dimension order of your images differs, you can optionally resave them in the correct format via the Preprocessing options.

### Output format

After YeastMate detects cells in your images, it will save the single cell instances segmentation masks as ```[input_file_name]_mask.tif``` as well as asignments of the individual cells to multicellular events in a JSON file called ```[input_file_name]_detections.json```, which has the following format:

```json
{

}
```


## Options

From there you can start three different jobs: 

* Preprocessing: If your images are not tiff/png/jpeg files, or need to align your images, you can preprocess your data first, else you can skip this step.

* Detection: The main job which performs inference on your images and save a segmentation mask and additional detection metadata.

* Export: If you want to further sort your detected objects or crop your images around specific objects, this job will perform additional export tasks.

## Correct and label your images

This page allows you to inspect and correct the predicted objects and masks, or to annotate your images from scratch if you want to re-train the neural network from scratch. Given the path containing the images, it will open a separate [napari](https://napari.org) window.

Check [Label your images](./label.md) for more information on labelling your data.

## Retraining the model

You can start a training run of the model on your own data after annotating it like above. This may boost performance of the model on your specific dataset. Note that this only works with the Docker backend, and at least one fast GPU is recommended for acceptable training times.

Check [Train on your data](./train.md) for more information on training on your data.
