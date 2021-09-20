# Installation

## Stand-alone GUI

YeastMate is available with prebuilt installers for Windows, Linux and Mac on [Github](https://github.com/hoerlteam/YeastMate/releases). 

YeastMate for Windows requires the Microsoft Visual C++ libraries. While these are usually already installed on most systems, you can download them [here](https://www.microsoft.com/en-US/download/details.aspx?id=26368) and [here](https://aka.ms/vs/16/release/vc_redist.x64.exe).

## FIJI plugin

You can download the Fiji plugin from https://github.com/hoerlteam/FijiYeastMate/releases. Just put the single ```.jar``` file into the ```plugins``` folder of you Fiji installation and YeastMate should appear under ```Plugins->YeastMate``` the next time you start Fiji.

## Detection backend

The detection backend comes in two versions; a prebuilt executable application as well as a Python Flask server for easy deployment on external servers.

If you installed the prebuilt packages, the local application is automatically installed and can be started from within the GUI.

If you want to run the Python server script directly, you need to prepare the Python environment as described in [Prepare environment](./environment.md). The easiest way is our [Docker image](https://hub.docker.com/hoerlteam/YeastMate), but you can also set up a Python environment yourself.

You can then run the detection server with:

``` bash
python yeastmate_server.py --port PORT
```

## Uninstalling YeastMate

* On Windows, the cleanest way to remove YeastMate is via the Control Panel under ```Programs > Programs and Features```.
* On macOS, you can just delete the YeastMate.app application.
* On Linux, ???