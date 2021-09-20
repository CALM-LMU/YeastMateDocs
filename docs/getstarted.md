# How to use the YeastMate user interface

After installing YeastMate (and potentially setting up the detection server yourself), you can get right to processing your images by opening the user interface.

## Starting a new detection job

The landing page allows you to start the IO and Detection backends and submit new jobs to it.

If you have setup external backends, you can point the GUI to these at the [Backend settings](./settings.md); else you can just start the local backends with the ```Start backends``` button. A terminal window will appear for each backend; with their status showing in the GUI. If you have set external backends, the GUI will send status requests and also show their status.

You can set tags to include or exclude files containing them:

# ![Screenshot](imgs/newjob.png)

### Input data format

YeastMate expects the input folder to contain TIFF files or a folder called ```yeastmate-preprocessed``` containing TIFF files. We support multiple channels or timepoints in files, in which case the dimension order should be TZCYX (default for TIFF images saved by ImageJ/Fiji). If the dimension order of your images differs, you can optionally resave them in the correct format via the Preprocessing options.

### Output format

After YeastMate detects cells in your images, it will save the single cell instances segmentation masks as ```[input_file_name]_mask.tif``` as well as asignments of the individual cells to multicellular events in a JSON file called ```[input_file_name]_detections.json```, which has the following format:

```json
{

}
```

## Options

From there you can select the presets you set on their respective [settings pages](./settings.md) for three different jobs: 

* Detection: The main job which performs inference on your images and save a segmentation mask and additional detection metadata.

* Preprocessing: If your images are not tiff/png/jpeg files, or need to align your images, you can preprocess your data first, else you can skip this step.

* Export: If you want to further sort your detected objects or crop your images around specific objects, this job will perform additional export tasks.

## Job dashboard

This page shows the status of the backends and all currently queued and running tasks.


## Correct and label your images

This page allows you to inspect and correct the predicted objects and masks, or to annotate your images from scratch if you want to re-train the neural network from scratch. Given the path containing the images, it will open a separate [napari](https://napari.org) window.

Check [Label your images](./label.md) for more information on labelling your data.

## Retraining the model

You can start a training run of the model on your own data after annotating it like above. This may boost performance of the model on your specific dataset. You need to setup a [Python environment](./environment.md), and at least one fast GPU is recommended for acceptable training times.

Check [Train on your data](./train.md) for more information on training on your data.
