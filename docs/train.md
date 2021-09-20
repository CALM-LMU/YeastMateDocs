# Train on your own data

We provide an easy workflow for re-training the detection model on your own data. The model training requires at least one GPU and CUDA version >= 10.2.

Network training usually takes 4-5GB of GPU RAM, this can be further reduced by setting the batch size from 2 to 1 in the *yeastmate.yaml* config file.

## Prepare your data

After annotating your images as in [Label your images](./label.md), you can use these images to train your own model.
The training script expects two folders:

* An input folder containing a folder named **train** with your training images and *_mask.tif* and *_detections.json* annotation files, the config files for your training, and optionally, a model weight to continue training on.

* An output folder where the model weights will be saved in.

The two config files can be found in [YeastMate/BioDetectron/biodetectron/configs](https://github.com/davidbunk/YeastMate/BioDetectron/biodetectron/configs), both *yeastmate.yaml* and *yeastmate_advanced.yaml* are required.

If you want to continue training on existing model weights, add them next to the config files and set their name in **MODEL.WEIGHTS** in *yeastmate.yaml* . 


## Start training within Docker container

Create and run the Docker container as explained in [Prepare environment](./environment.md).

You can then start the training process with:

``` bash
python ./yeastmatepredictor/train.py --config=/home/appuser/input/yeastmate.yaml
```

## Start training without Docker

You can also run the training scripts without the Docker image. For this you need to setup your Python environment as in [Deploy and Build](./build.md).

You need to change your input path within [YeastMate/BioDetectron/biodetectron/datasets.py](https://github.com/davidbunk/YeastMate/BioDetectron/biodetectron/datasets.py) to your real input folder, and set your real output path in the *yeastmate.yaml* config file, which needs to be in the same folder as *yeastmate_advanced.yaml*. 

From the BioDetectron folder, you can then execute:

``` bash
python ./biodetectron/train.py --config=/PATH/TO/YOUR/yeastmate.yaml
```

While not necessary, it's recommended to use [tmux](https://github.com/tmux/tmux/wiki) or similar tools to let the training run in the background without risk of interruption. 