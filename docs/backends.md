# Python - Start Backends

To start the backends, download the [YeastMateBackend](https://github.com/hoerlteam/YeastMateBackend) repository and set up the Python environment as described in [Python - Installation](./environment.md). Then activate your conda environment or enter your Docker container.

## Detection backend

The detection server requires a model snapshot and a model configuration file. The default configuration files are located in the `models` directory of the repository. You need to download our model weights file from [OSF](https://osf.io/287fr/?view_only=99d1fddb563b4253957f226c19c4113f) and add them to the `models` directory, or alternatively use your own model snapshot.

You can then start the Detection backend with:

``` bash
python yeastmate_server.py
```

It comes with multiple optional command line arguments:

* ```--gpu``` : Add this flag if you want to run the Detection on GPU. Default is ```False```.
* ```--gpu_index``` : The index of the GPU to use. Only used if ```--gpu```  flag is given. Default is ```0```.
* ```--port``` : The port on which the backend should listen on. Default is ```11005```.
* ```--config``` : Path to the config file for the Detection. Only necessary if you re-trained the model. Default is ```'models/yeastmate.yaml'```.
* ```--model``` : Path to the model weight file for the Detection. Only necessary if you re-trained the model. Default is ```'models/yeastmate_weights.pth'```.

## IO backend

You can start the IO backend with:

``` bash
python hueyserver.py
```

It takes the following optional command line argument:

* ```--port``` : The port on which the backend should listen on. Default is ```11002```.