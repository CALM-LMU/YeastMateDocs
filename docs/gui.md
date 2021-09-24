# How to use the YeastMate user interface

## Installing the stand-alone YeastMate application

YeastMate is available with prebuilt installers for Windows, Linux and Mac on [Github](https://github.com/hoerlteam/YeastMate/releases). 

This will install the user interface, the Python data IO backend and the Python detection backend. The backends are packaged with PyInstaller with all their dependencies and don't require a Python installation on your system. Both backends can then be started from within the GUI.

The user interface and the packaged backends were tested on Windows 10, Ubuntu 18.04 and MacOS 11.5.2. If any errors or bugs occure, you can report them on [Github](https://github.com/hoerlteam/YeastMate/issues). 

YeastMate for Windows requires the Microsoft Visual C++ libraries. While these are usually already installed on most systems, you can download them [here](https://www.microsoft.com/en-US/download/details.aspx?id=26368) and [here](https://aka.ms/vs/16/release/vc_redist.x64.exe).

## Uninstalling YeastMate

* On Windows, the cleanest way to remove YeastMate is via the Control Panel under ```Programs > Programs and Features```.
* On macOS, you can just delete the YeastMate.app application.
* On Linux, ???

## Get Started

After installing YeastMate, you can get right to processing your images by opening the user interface.

The actual processing of your images happens not within the user interface, but within two additional Python backend applications. While these can also be set up independently by yourself (see [Python - Get Started](./python.md)), already packaged instances of these can be locally started from the user interface. 

The user interface and the two backends communicate via HTTP requests and thus need to listen and send requests over some ports of your system. Depending on your system and firewall you might encounter a warning that YeastMate requests internet access. Unless you specifically tell YeastMate to use the internet to connect to a remote backend, YeastMate will NOT initiate any internet connection, and only communicate locally on your PC via these ports.

On the following pages you will find a status display for the backends with a button to start the backends. These backends are automatically set up to run locally and start on an automatically found free port. Starting the backends will open two additional terminal windows, which will take a moment to initalize and start. A message in those terminal windows as well as the status block in the GUI will indicate when they're running and ready to go.

## Starting a new detection job

The landing page allows you to start the IO and Detection backends and submit new jobs to it.

If you have setup external backends, you can point the GUI to these at the [Backend settings](./settings.md); else you can just start the local backends with the ```Start backends``` button. 

Set the path to the folder directly containing the images you want to detect on (or preprocess them). YeastMate will not look into sub-directories, apart from a folder ```yeastmate-preprocessed`` which will contain the output of the preprocessing step if you use it.

You can also set tags to include or exclude files containing them:

# ![Screenshot](imgs/newjob.png)

## Options

From there on you can select the presets you set on their respective [settings pages](./settings.md) for three different jobs: 

* Detection: The main job which performs inference on your images and save a segmentation mask and additional detection metadata.

* Preprocessing: If your images are not tiff/png/jpeg files, or you need to align your images, you can preprocess your data first, else you can skip this step.

* Export: If you want to further sort your detected objects or crop your images around specific objects, this job will perform additional export tasks.

### Input data format

YeastMate expects the input folder to contain TIFF files or a folder called ```yeastmate-preprocessed``` containing TIFF files. We support multiple channels or timepoints in files, in which case the dimension order should be TZCYX (default for TIFF images saved by ImageJ/Fiji). If the dimension order of your images differs, you can optionally resave them in the correct format via the Preprocessing options.

### Output format

After YeastMate detects cells in your images, it will save the single cell instances segmentation masks as ```[input_file_name]_mask.tif``` as well as asignments of the individual cells to multicellular events in a JSON file called ```[input_file_name]_detections.json```, which has the following format:

```json
{

}
```

## Job dashboard

# ![Screenshot](imgs/newjob.png)

This page shows the status of the backends and all currently queued and running tasks.

## Correct and label your images

# ![Screenshot](imgs/annotate.png)

This page allows you to inspect and correct the predicted objects and masks, or to annotate your images from scratch if you want to re-train the neural network from scratch. Given the path containing the images, it will open a separate [napari](https://napari.org) window.

Check [Label your images](./label.md) for more information on labelling your data.

## Retraining the model

You can start a training run of the model on your own data after annotating it like above. This may boost performance of the model on your specific dataset. You need to setup a [Python - Get Started](./python.md), and at least one fast GPU is recommended for acceptable training times.

Check [Train on your data](./train.md) for more information on training on your data.
