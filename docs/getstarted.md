# How to use the YeastMate user interface

After installing YeastMate (and potentially setting up the Docker detection container), you can get right to processing your images by opening the user interface. It should open a terminal for the backend in the background, or two separate instances if you are using the local detection backend. If these are not opening or closing instantly, you can file a bug report [here](https://github.com/CALM-LMU/YeastMate/issues)

## Job dashboard

This page shows all currently queued and running tasks.

## Start a new job

From here you can start your inference jobs for a given path containing your images. You can only include or exclude specific files by setting their respective tags.

From there you can start three different jobs: 

* Preprocessing: If your images are not tiff/png/jpeg files, or need to align your images, you can preprocess your data first, else you can skip this step.

* Detection: The main job which performs inference on your images and save a segmentation mask and additional detection metadata.

* Export: If you want to further sort your detected objects or crop your images around specific objects, this job will perform additional export tasks.

## Correct and label your images

This page allows you to inspect and correct the predicted objects and masks, or to annotate your images from scratch if you want to re-train the neural network from scratch. Given the path containing the images, it will open a separate [napari](https://napari.org) window.

Check [Label your images](./label.md) for more information on labelling your data.

## Retrain your network

Here you can start a training run of the model on your own data. This may boost performance of the model on your specific dataset. Note that this only works with the Docker backend, and at least one fast GPU is recommended for acceptable training times.

Check [Train on your data](./train.md) for more information on training on your data.

## Benchmark network

Should we add this? Not sure.