# Python - Get Started

After you set up your Python environment, you can run the backends manually, or use the YeastMate Python API to implement the detection in your own scripts. We provide example Jupyter Notebooks how to access the YeastMate detection functions.

## Start the backends manually

To start the backends, download the [YeastMateBackend](https://github.com/hoerlteam/YeastMateBackend) repository and set up the Python environment as described in [Python - Installation](./environment.md). Then activate your conda environment or enter your Docker container.

### IO backend

You can start the IO backend with:

``` bash
python hueyserver.py
```

It takes the following optional command line argument:

* ```--port``` : The port on which the backend should listen on. Default is ```11002```

### Detection backend

You can start the Detection backend with:

``` bash
python yeastmate_server.py
```

It comes with multiple optional command line arguments:

* ```--gpu``` : Add this flag if you want to run the Detection on GPU. Default is ```False```.
* ```--gpu_index``` : The index of the GPU to use. Only used if ```--gpu```  flag is given. Default is ```0```.
* ```--port``` : The port on which the backend should listen on. Default is ```11005```.
* ```--config``` : Path to the config file for the Detection. Only necessary if you re-trained the model. Default is ```'models/yeastmate.yaml'```.
* ```--model``` : Path to the model weight file for the Detection. Only necessary if you re-trained the model. Default is ```'models/yeastmate_weights.pth'```.

## Use the YeastMate Python module

You can also use the YeastMate Python module directly in your scripts. It's recommended to use the Jupyter Notebooks within the [YeastMate repository](https://github.com/hoerlteam/YeastMate) as a base.