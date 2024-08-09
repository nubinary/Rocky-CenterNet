# Installation (CPU mode)

install anaconda
open anaconda powershell
conda install m2-base
install cuda toolkit 12.4, download cudnn 9.2 and unzip contents into C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v12.4
To find cuda <> cudnn compatibility use: https://docs.nvidia.com/deeplearning/cudnn/latest/reference/support-matrix.html
conda create --name rock-tech python
conda activate rock-tech
git clone git@github.com:nubinary/Rocky-CenterNet.git
cd Rocky-CenterNet
pip install -r requirements.txt
cd ./src/lib/models/networks/DCNv2
python setup.py build develop
cd ..\..\..\external\
make
Get model from https://drive.google.com/file/d/15EkBUSIB_mDNhkXTHLzLJdrM_2azG1Am/view?usp=sharing and place in models folder


# Original Installation process

The code was tested on Ubuntu 18.04, with [Anaconda](https://www.anaconda.com/download) Python 3.6 and [PyTorch]((http://pytorch.org/)) v1.4. NVIDIA GPUs are needed for both training and testing. Installation can be done via conda, pip or Docker.
In the case of Docker, a Dockerfile is included with the repository, with this a container with all installed packages and dependencies can be quickly obtained.
After installing Anaconda:

0. [Optional but recommended] create a new conda environment.

    ~~~
    conda create --name RockyCenterNet python=3.6
    ~~~
    And activate the environment.

    ~~~
    conda activate RockyCenterNet
    ~~~

1. Install pytorch 1.4:

    ~~~
    conda install pytorch=1.4.1 torchvision -c pytorch
    ~~~

1. (non-conda) Install pytorch 1.4

    ~~~
    pip install -q torch==1.4 torchvision==0.5 -f https://download.pytorch.org/whl/cu101/torch_stable.html
    ~~~

2. Install [COCOAPI](https://github.com/cocodataset/cocoapi):

    ~~~
    # COCOAPI=/path/to/clone/cocoapi
    git clone https://github.com/cocodataset/cocoapi.git $COCOAPI
    cd $COCOAPI/PythonAPI
    make
    python setup.py install --user
    ~~~

3. Clone this repo:

    ~~~
    CenterNet_ROOT=/path/to/clone/Rocky-CenterNet
    git clone https://github.com/amtc-rock-detectors/Rocky-CenterNet $RockyCenterNet_ROOT
    ~~~


4. Install the requirements

    ~~~
    pip install -r requirements.txt
    ~~~


5. Compile deformable convolutional (from [DCNv2](https://github.com/CharlesShang/DCNv2/tree/pytorch_0.4)).

    ~~~
    cd $RockyCenterNet_ROOT/src/lib/models/networks/DCNv2
    ./make.sh
    ~~~

6. Complie NMS

    ~~~
    cd $RockyCenterNet_ROOT/src/lib/external
    make
    ~~~

7. Download pertained models for [detection]() or [pose estimation]() and move them to `$RockyCenterNet_ROOT/models/`. More models can be found in [Model zoo](MODEL_ZOO.md).
