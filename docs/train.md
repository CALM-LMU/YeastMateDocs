# Train on your own data

We provide an easy workflow for re-training the detection model on your own data. The model training requires at least one GPU and CUDA version >= 10.1.

## Prepare your data

After annotating your images as in [Label your images](./label.md), you can use these images to train your own model.
The training script expects two folders:

* An input folder containing a folder named **train** with your training images and *_mask.tif* and *_detections.json* annotation files, the config files for your training, and optionally, a model weight to continue training on.

* An output folder where the model weights will be saved in.

The two config files can be found in [YeastMate/BioDetectron/biodetectron/configs](https://github.com/davidbunk/YeastMate/BioDetectron/biodetectron/configs), both *yeastmate.yaml* and *yeastmate_advanced.yaml* are required.

If you want to continue training on existing model weights, add them next to the config files and set their name in **MODEL.WEIGHTS** in *yeastmate.yaml* . 

## Prepare your Docker container

We provide a Docker image with a prepared environment for easy training with only a few commands. If you don't want to use the Docker training image, skip to [Start training without Docker](#start-training-without-docker).

If you don't already have Docker installed, you can find an installation guide at the [Docker docs](https://docs.docker.com/engine/install/).

When Docker is ready, download the training image with:

``` bash
docker pull davidbunk/yeastmatedetectron:latest
```

You can then start the training container with the following command. Change the source input and output paths to your respective folders.

``` bash
docker run -it --shm-size=50G --mount source=YOUR/INPUT/PATH,target=/home/appuser/input,type='bind' --mount source=YOUR/OUTPUT/PATH,target=/home/appuser/output,type='bind' --gpus all davidbunk/yeastmatedetectron:latest
```

The Docker container automatically starts as root user. To change to a non-root user for training type in:

``` bash
su appuser
```

The Docker user on the host machine requires read access to the input folder and read/write access to the output folder. Check these permissions if the training fails with permission errors. 

If that doesn't solve these errors, you can train as root user by skipping the command above. Although this is not necessarily problematic, it also comes with the usual risks of running commands as root.

## Start training in Docker container

You can then start the actual training process with:

``` bash
python ./biodetectron/train.py --config=/home/appuser/input/yeastmate.yaml
```

## Start training without Docker

You can also run the training scripts without the Docker image. For this you need to setup your Python environment as in [Deploy and Build](./build.md).

You need to change your input path within [YeastMate/BioDetectron/biodetectron/datasets.py](https://github.com/davidbunk/YeastMate/BioDetectron/biodetectron/datasets.py) to your real input folder, and set your real output path in the *yeastmate.yaml* config file, which needs to be in the same folder as *yeastmate_advanced.yaml*. 

From the BioDetectron folder, you can then execute:

``` bash
python ./biodetectron/train.py --config=/PATH/TO/YOUR/yeastmate.yaml
```

While not necessary, it's recommended to use [tmux](https://github.com/tmux/tmux/wiki) or similar tools to let the training run in the background without risk of interruption. 