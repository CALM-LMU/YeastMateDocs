If you want to run GPU-accelerated detection or remote detection, the easiest way is to use our Docker image. For Information on how to install Docker, refer to https://docker.com.
The Docker image can be found on [Docker hub](https://hub.docker.com/CALM/YeastMate). The image can then be spun into containers and run like any other Docker image. You need to forward the internal docker port 5000 to the port you set in the user interface (default is 5000) so that the container can communicate with the user interface and other backend. If you need GPU inference, you'll also need to give the container GPU access via the ```--gpus all``` flag. To run the detection backend with GPU support, run the following command:

``` bash
docker run -it -p 5000:5000 --rm --gpus all PICKAGOODNAMEHERE:latest
```

The container will run until you quit with ```Ctrl-C```. Note that you have to keep the terminal window in which you started the container open. If you want to run the container in the background, you can add the ```-d``` flag to the ```docker run command```.

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

If you don't want to expose all of your GPUs, you can select a specific GPU device like this:

``` bash
docker run -it --shm-size=50G --mount source=YOUR/INPUT/PATH,target=/home/appuser/input,type='bind' --mount source=YOUR/OUTPUT/PATH,target=/home/appuser/output,type='bind' --gpus '"device=0"' davidbunk/yeastmatedetectron:latest
```

The Docker container automatically starts as root user. To change to a non-root user for training type in:

``` bash
su appuser
```

The Docker user on the host machine requires read access to the input folder and read/write access to the output folder. Check these permissions if the training fails with permission errors. 

If that doesn't solve these errors, you can train as root user by skipping the command above. Although this is not necessarily problematic, it also comes with the usual risks of running commands as root.