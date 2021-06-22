# Installation

## Stand-alone GUI
YeastMate is available with prebuilt installers for Windows, Linux and Mac on [Github](https://github.com/CALM-LMU/YeastMate/releases).

The installer will install the user interface and the backends in your user folder and create a shortcut on your Desktop.

YeastMate for Windows requires the Microsoft Visual C++ libraries. While these are usually already installed on most systems, you can download them [here](https://www.microsoft.com/en-US/download/details.aspx?id=26368) and [here](https://aka.ms/vs/16/release/vc_redist.x64.exe), or alternative find them within the installation folder.

## FIJI plugin


## Detection backend
The detection backend comes in two versions; a local executable application for prediction on CPU as well as a Docker image with GPU capabilities for workstations and servers.

The local application is automatically installed if you selected the complete package binary on the Github page.

The Docker image can be found on [Docker hub](https://hub.docker.com/CALM/YeastMate). The image can then be spun into containers and run like any other Docker image. You need to forward the internal docker port 5000 to the port you set in the user interface (default is 5000) so that the container can communicate with the user interface and other backend. If you need GPU inference, you'll also need to give the container GPU access. An example command could look like this:

``` bash
docker start -it -p 5000:5000 --gpus all YeastMate:latest
```