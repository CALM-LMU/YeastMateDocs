# Setting up the Python backends manually

If you want to run one or two of the backends manually or remotely, you can easily run the two Python scripts as long as you have Python with YeastMate's dependencies installed. Additionally, you can also forgo the user interface and its backends and use our YeastMate Python module directly to implement the detection in your Python scripts. We offer two simple solutions to set this environment up: 

* Anaconda environment files which will automatically install all dependencies

* A docker image that comes with Python and YeastMate already installed

Of course, you can also just install Python and install all dependencies within the environment files manually via pip.

## Setting up a Conda Environment

First of all, you need to download and install [Anaconda 3](https://www.anaconda.com/products/individual) and download the respective code repositories from Github for the [Detection backend](https://github.com/hoerlteam/YeastMate) and/or the [IO backend](https://github.com/hoerlteam/YeastMateBackend).

You can then create your conda environment by navigating into the ```YeastMate``` or ```YeastMateBackend``` folder and running the following command:

``` bash
conda env create -f env_yeastmate_linux.yaml
```

You might have to substitute the last filename with the actual environment file for your system that you want to use. 

You can then activate the conda environment with:

``` bash
conda activate yeastmate
```

## Setting up a Docker container

First of all you need to have the Docker service installed. For Information on how to install Docker, refer to the [Docker homepage](https://docker.com).

The Docker image can be found on [Docker hub](https://hub.docker.com/davidbunk/YeastMate). You can download it from the command line with the following command:

``` bash
docker pull davidbunk/yeastmate:latest
```

The image can then be spun into containers and run like any other Docker image. 

To expose the backends outside of the Docker container, you need to forward the internal container port that the backend is running on to the port you set in the user interface (default is 11002 for the IO backend and 11003 for the Detection backend).  

If you need GPU inference, you'll also need to give the container GPU access via the ```--gpus all``` flag. 

To run the detection backend with GPU support, run the following command:

``` bash
docker run -it -p HOSTPORT:CONTAINERPORT --shm-size=16G --rm --gpus all davidbunk/yeastmate:latest
```

To give the Docker container access to specific GPUs, you can specify the device:

``` bash
docker run -it -p HOSTPORT:CONTAINERPORT --shm-size=16G --rm --gpus '"device=0"' davidbunk/yeastmate:latest
```

If you want to run your own training run (more on that at [Python - Train on your data](./train.md), you also need to give the Docker container access to your folder containing the training data and to an output folder where the network weights will be saved.

``` bash
docker run -it -p HOSTPORT:CONTAINERPORT --mount source=YOUR/INPUT/PATH,target=/home/appuser/input,type='bind' --mount source=YOUR/OUTPUT/PATH,target=/home/appuser/output,type='bind' --shm-size=32G --rm --gpus '"device=0"' davidbunk/yeastmate:latest
```

The Docker user on the host machine requires read access to the input folder and read/write access to the output folder. Check these permissions if the training fails with permission errors. 

If that doesn't solve these errors, you avoid this error by running commands as sudo. Although this is not necessarily problematic, it also comes with the usual risks of running commands as root.

The container will run until you quit with ```Ctrl-C```. If you want to disconnect from the Docker terminal while still keeping the processes inside running, you can use the shortcuts ```Ctrl-p``` and ```Ctrl-q``` after each other.
