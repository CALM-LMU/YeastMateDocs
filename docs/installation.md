# Installation

## Stand-alone GUI

YeastMate is available with prebuilt installers for Windows, Linux and Mac on [Github](https://github.com/CALM-LMU/YeastMate/releases).

**We suggest to download the ```YeastMate-allinone``` package, which includes the detection backend (CPU-only) and network weights but can also make use of a separate detection server.** If you want to set up a (GPU) detection backend yourself, you can download the ```YeastMate-clientonly``` package, which does not include a local detection backend. The installer will install the user interface and the backends in your user folder and create a shortcut on your Desktop.

YeastMate for Windows requires the Microsoft Visual C++ libraries. While these are usually already installed on most systems, you can download them [here](https://www.microsoft.com/en-US/download/details.aspx?id=26368) and [here](https://aka.ms/vs/16/release/vc_redist.x64.exe), or alternatively find them within the installation folder.

## FIJI plugin

You can download the Fiji plugin from https://github.com/CALM-LMU/FijiYeastMate/releases. Just put the single ```.jar``` file into the ```plugins``` folder of you Fiji installation and YeastMate should appear under ```Plugins->YeastMate``` the next time you start Fiji.

## Detection backend

The detection backend comes in two versions; a local executable application for prediction on CPU as well as a Docker image with GPU capabilities for workstations and servers.

If you installed ```YeastMate-allinone```, the local application is automatically installed and will start automatically if you launch YeastMate.

If you want to run GPU-accelerated detection or remote detection, the easiest way is to use our Docker image. For Information on how to install Docker, refer to https://docker.com.
The Docker image can be found on [Docker hub](https://hub.docker.com/CALM/YeastMate). The image can then be spun into containers and run like any other Docker image. You need to forward the internal docker port 5000 to the port you set in the user interface (default is 5000) so that the container can communicate with the user interface and other backend. If you need GPU inference, you'll also need to give the container GPU access via the ```--gpus all``` flag. To run the detection backend with GPU support, run the following command:

``` bash
docker run -it -p 5000:5000 --rm --gpus all PICKAGOODNAMEHERE:latest
```

The container will run until you quit with ```Ctrl-C```. Note that you have to keep the terminal window in which you started the container open. If you want to run the container in the background, you can add the ```-d``` flag to the ```docker run command```.

## Running the detection backend without Docker

Running the detection backend without Docker can be tricky as it requires compatible versions of CUDA, PyTorch and Detectron2 to be installed. For detailed instructions, refer to [LINK]

## Uninstalling YeastMate

* On Windows, the cleanest way to remove YeastMate is via the Control Panel under ```Programs > Programs and Features```.
* On macOS, you can just delete the YeastMate.app application.
* On Linux, ???