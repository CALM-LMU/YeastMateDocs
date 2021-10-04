# Train on your own data

We provide an easy workflow for re-training the detection model on your own data. The model training requires at least one GPU and CUDA version >= 10.2.

Network training usually takes 4-5GB of GPU RAM, this can be further reduced by setting the batch size from 2 to 1 in the ```yeastmate.yaml``` configuration file.

## Start training

After annotating your images (see [Label your images](./label.md)), you can use these to train your own model. 

The training routine can be started with the following command

``` bash
python ./yeastmatedetector/train.py --config=/PATH/TO/YOUR/yeastmate.yaml
```

and expects a ```yeastmate.yaml``` configuration file to be parsed. The two config files can be found in [YeastMateDetector/yeastmatedetector/configs](https://github.com/hoerlteam/YeastMate/tree/main/yeastmatedetector/configs), both *yeastmate.yaml* and *yeastmate_advanced.yaml* are required.

In these configuration files you can set various training and network parameters, the most important being input and output directories, the batch size, the number of epochs, the learning rate and the number of dataloading workers.

* **INPUT_DIR**: The directory containing our 2D training images and *_mask.tif* and *_detections.json* annotation files.
* **OUTPUT_DIR**: The directory where the trained model snapshots will be stored.

Note that the default settings correspond to the locations when using our Docker container, adjust them as needed.

If you want to continue training from a previous snapshot, specify the path of that snapshot in **MODEL.WEIGHTS** in *yeastmate.yaml*.

## Notes on Training

While not necessary, it's recommended to use [tmux](https://github.com/tmux/tmux/wiki) or similar tools to let the training run in the background without risk of interruption. 

## Training in Docker container

If you want to run the training in a Docker container, you also need to give it access to:

* An input folder containing a folder named ```images``` with your 2D training images and the ```_mask.tif``` and ```_detections.json``` annotation files, the config files for your training, and optionally, a model weight to continue training on.

* An output folder where the trained model snapshots will be stored.

E.g. to run the container with mounted input and output folders, you can use the following command:

``` bash
docker run -it -p HOSTPORT:CONTAINERPORT --mount source=YOUR/INPUT/PATH,target=/home/appuser/input,type='bind' --mount source=YOUR/OUTPUT/PATH,target=/home/appuser/output,type='bind' --shm-size=32G --rm --gpus all davidbunk/yeastmate:latest
```

You can then use the following command to start the training:

``` bash
python ./yeastmatedetector/train.py --config=/home/appuser/input/yeastmate.yaml
```

The Docker user on the host machine requires read access to the input folder and read/write access to the output folder. Check these permissions if the training fails with permission errors. 

If that doesn't solve these errors, you can avoid this error by running commands as sudo. Although this is not necessarily problematic, it also comes with the usual risks of running commands as root.

## Using your own model weights

After training, you can use your config file and your saved model weights to run your custom detection server. It is recommended to let the training run for 200,000 iterations and use the model_0199999.pth weight.

You can then either set the paths to your config and weight file within the GUI (see [GUI - Settings](./settings.md)) or give these paths as command line arguments to the backend Python scripts if you run them manually (see [Python - Get Started](./python.md))