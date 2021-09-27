# Train on your own data

We provide an easy workflow for re-training the detection model on your own data. The model training requires at least one GPU and CUDA version >= 10.2.

Network training usually takes 4-5GB of GPU RAM, this can be further reduced by setting the batch size from 2 to 1 in the *yeastmate.yaml* config file.

## Prepare your data

After annotating your images as in [Label your images](./label.md), you can use these images to train your own model. 

The training script expects two folders:

* An input folder containing a folder named **train** with your 2D training images and *_mask.tif* and *_detections.json* annotation files, the config files for your training, and optionally, a model weight to continue training on.

* An output folder where the model weights will be saved in.

The two config files can be found in [YeastMateDetector/yeastmatedetector/configs](https://github.com/hoerlteam/YeastMate/tree/main/yeastmatedetector/configs), both *yeastmate.yaml* and *yeastmate_advanced.yaml* are required.

If you want to continue training on existing model weights, add them next to the config files and set their name in **MODEL.WEIGHTS** in *yeastmate.yaml* . 


## Start training within Docker container

Create and run the Docker container as explained in [Python - Installation](./environment.md).

You can then start the training process with:

``` bash
python ./yeastmatedetector/train.py --config=/home/appuser/input/yeastmate.yaml
```

## Start training without Docker

You can also run the training scripts without the Docker image. For this you need to setup your Python environment as in [Python - Get Started](./python.md).

You need to change your input and output paths within [YeastMateDetector/yeastmatedetector/configs/yeastmate.yaml](https://github.com/hoerlteam/YeastMate/blob/main/yeastmatedetector/configs/yeastmate.yaml) to your real input and output folders.

From the BioDetectron folder, you can then execute:

``` bash
python ./yeastmatedetector/train.py --config=/PATH/TO/YOUR/yeastmate.yaml
```

While not necessary, it's recommended to use [tmux](https://github.com/tmux/tmux/wiki) or similar tools to let the training run in the background without risk of interruption. 

## Using your own model weights

After training, you can use your config file and your saved model weights to run your custom detection server. It is recommended to let the training run for 200,000 iterations and use the model_0199999.pth weight.

You can then either set the paths to your config and weight file within the GUI (see [GUI - Settings](./settings.md)) or give these paths as command line arguments to the backend Python scripts if you run them manually (see [Python - Get Started](./python.md))