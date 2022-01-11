# Setting up the Python environment

If you want to run YeastMate without the user interface and its backends and use it as a Python module directly to implement the detection in your Python scripts, we offer two simple solutions to set this environment up: 

* Anaconda environment files which will automatically install all dependencies

* A docker image that comes with Python and YeastMate already installed

Of course, you can also just install Python and install all dependencies within the environment files manually via pip following the ```requirements.txt``` file.

Furthermore, if you want to run one or two of the backends (detection and IO) manually or remotely, you can easily run their respective Python scripts as long as you have Python with YeastMate's dependencies installed.

**Compatibility with M1 Macs:** Currently, not all dependencies of the YeastMate module seem to be available for macOS on the Apple M1 (arm64) architecture via conda, preventing the use of the Python module on M1 Macs. Note that the [prebuilt binaries for macOS](./gui.md) will work thanks to Apple’s Rosetta2 x86 emulation, though with suboptimal performance. 

## Setting up a Conda Environment

First of all, you need to download and install [Anaconda 3](https://www.anaconda.com/products/individual) and download the code repository from Github for the YeastMate Python module [https://github.com/hoerlteam/YeastMate](https://github.com/hoerlteam/YeastMate).

You can then create your conda environment by navigating into the ```YeastMate``` folder and running the following command:

``` bash
conda env create -f env_yeastmate_linux.yaml
```

You might have to substitute the last part of the filename with the actual environment file for your system (linux/win/mac) that you want to use. 

You can then activate the conda environment with:

``` bash
conda activate yeastmate
```

## Use the YeastMate Python module

To install the YeastMate module, navigate into the ```YeastMate``` folder and run the following command:

``` bash
pip install -e .
```

After installation, you can access most functionality of YeastMate via the ```YeastMatePredictor``` class:

```python
from yeastmatedetector.inference import YeastMatePredictor

predictor = YeastMatePredictor('./models/yeastmate.yaml')

# load image as numpy array

detections, mask = predictor.inference(your_image)
```

By default, YeastMate will load the model weight file specified in the config file. This can either be a local path, or a weblink to a model file. If a remote file is set, YeastMate will download it into cache and reuse it; the default value in the config is our pre-trained model hosted on [OSF](https://osf.io/287fr/?view_only=99d1fddb563b4253957f226c19c4113f).

Alternatively, you can tell YeastMate to ignore the model path in the config and set the model path with a second argument like below. Note that this only works with local files, if you want to use a remote file you have to set the remote path in the config.

```python
predictor = YeastMatePredictor('./models/yeastmate.yaml', './models/yeastmate_weights.pth')
```

The [YeastMate repository](https://github.com/hoerlteam/YeastMate) contains an example notebook showcasing the Python API.

## Setting up a Docker container

First of all you need to have the Docker service installed. For Information on how to install Docker, refer to the [Docker homepage](https://docker.com).

The Docker image can be found on [Docker hub](https://hub.docker.com/davidbunk/YeastMate). You can download it from the command line with the following command:

``` bash
docker pull davidbunk/yeastmate:latest
```

The image can then be spun into containers and run like any other Docker image. 

If you want to use the (webservice) backends and expose them outside of the Docker container, you need to forward the internal container port that the backend is running on to the port you set in the user interface (default is 11002 for the IO backend and 11005 for the Detection backend).  

If you need GPU inference, you'll also need to give the container GPU access via the ```--gpus all``` flag. 

To run the detection backend with GPU support, run the following command:

``` bash
docker run -it -p HOSTPORT:CONTAINERPORT --shm-size=16G --rm --gpus all davidbunk/yeastmate:latest
```

To give the Docker container access to specific GPUs, you can specify the device:

``` bash
docker run -it -p HOSTPORT:CONTAINERPORT --shm-size=16G --rm --gpus '"device=0"' davidbunk/yeastmate:latest
```

The container will run until you quit with ```Ctrl-C```. If you want to disconnect from the Docker terminal while still keeping the processes inside running, you can use the shortcuts ```Ctrl-p``` and ```Ctrl-q``` after each other. You can re-attach to a running container using:

``` bash
docker attach ID_OF_CONTAINER
```
