# Visual Perception and Recogntion for Autonomous Driving
This is one graduation design named "Visual Perception and Recogntion for Autonomous Driving".

## Requirements

The code requires [Python 2.7](https://www.python.org/download/releases/2.7/), [Tensorflow 1.0](https://www.tensorflow.org/install/), as well as the following python libraries: 

* matplotlib
* numpy
* Pillow
* scipy
* runcython
* commentjson

Those modules can be installed using: `pip install numpy scipy pillow matplotlib runcython commentjson` or `pip install -r requirements.txt`.


## Setup

1. Clone this repository: `https://github.com/MPIG/Visual-Perception-and-Recognition-for-Autonomous-Driving.git`
2. Initialize all submodules: `git submodule update --init --recursive`
3. `cd submodules/KittiBox/submodules/utils/ && make` to build cython code
4. [Optional] Download Kitti Road Data:
    1. Retrieve kitti data url here: [http://www.cvlibs.net/download.php?file=data_road.zip](http://www.cvlibs.net/download.php?file=data_road.zip)
    2. Call `python download_data.py --kitti_url URL_YOU_RETRIEVED`
5. [Optional] Run `cd submodules/KittiBox/submodules/KittiObjective2/ && make` to build the Kitti evaluation code (see [submodules/KittiBox/submodules/KittiObjective2/README.md](https://github.com/MarvinTeichmann/KittiBox/blob/1073ab1ef6c53adc78c5340f42ce3468797d50b4/submodules/KittiObjective2/README.md) for more information)
    
Running the model using `demo.py` only requires you to perform step 1-3. Step 4 and 5 is only required if you want to train your own model using `train.py`. Note that I recommend using `download_data.py` instead of downloading the data yourself. The script will also extract and prepare the data. See Section [Manage data storage](README.md#manage-data-storage) if you like to control where the data is stored.

##### To update the code do:

1. Pull all patches: `git pull`
2. Update all submodules: `git submodule update --init --recursive`

If you forget the second step you might end up with an inconstant repository state. You will already have the new code for MultiNet but run it old submodule versions code. This can work, but I do not run any tests to verify this.


### Getting started

Run: `python demo.py --gpus 0 --input data/demo/um_000005.png` to obtain a prediction using [demo.png](data/demo/um_000005.png) as input.

Run: `python evaluate.py` to evaluate a trained model. 

Run: `python train.py --hypes hypes/model3.json` to train.


### Modifying Model & Train on your own data

The model is controlled by the file `hypes/model3.json`. This file points the code to the implementation of the submodels. The MultiNet code then loads all models provided and integrates the decoders into one neural network. To train on your own data, it should be enough to modify the hype files of the submodels. A good start will be the [KittiSeg](https://github.com/MarvinTeichmann/KittiSeg#kittiseg) model, which is very well documented.

```
    "models": {
        "segmentation" : "../submodules/KittiSeg/hypes/KittiSeg.json",
        "detection" : "../submodules/KittiBox/hypes/kittiBox.json",
    },
```

