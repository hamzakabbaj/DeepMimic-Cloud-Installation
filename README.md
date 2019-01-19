# DeepMimic Installation in Google Cloud (takes 10 minutes !!)

The purpose of this repository is to help students of MVA master install DeepMimic and run tests as fast as possible.
We actually lost several days attempting to make these installations. I hope it wouldn't be the case for you.


We will be using Google cloud Virtual Machines.

Note that there are two parts in DeepMimic :
- First, visualising the results 
- Second, launching trainings

We will show only how to launch trainings which is the most important part of the project.
One advice, start testing trainings early !! it takes minimum 24 hours for each test.


## Create a Google cloud Virtual Machine 
- Go to Compute Engine / VM Instances
- Create a new VM
- Choose a VM with 16vCPU
- Choose Ubuntu 16.04 LTS

## DeepMimic Installation

- Clone the repository 
```bash
git clone https://github.com/hamzakabbaj/DeepMimic_Cloud_Installation.git
```

- install packages
``` bash
sudo apt-get update
sudo apt-get install cmake build-essential clang llvm python-dev freeglut3-dev libbullet-dev libbullet-extras-dev  libglew-dev swig libopenmpi-dev  python3-pip
```
- install virtualenv 
``` bash
pip3 install virtualenv
```

- Create a virtual environement and activate it (working with a virtual environment is necessary)
``` bash
virtualenv env_deep_mimic
source env_deep_mimic/bin/activate
```
- install python packages
``` bash
pip install pyopengl mpi4py tensorflow numpy
```
- install requirements
``` bash
cd DeepMimic_Cloud_Installation/DeepMimic
pip install -r requirements.txt
```
- change Makefile and install DeepMimicCore
``` bash
cd DeepMimicCore
vi Makefile
```
``` python
# DONT FORGET TO CHANGE EIGEN PATH !!!!!
EIGEN_DIR = /home/ubuntu/DeepMimic_Cloud_Installation/eigen 
BULLET_INC_DIR = /usr/include/bullet 

PYTHON_INC = /usr/include/python3.5m
PYTHON_LIB = /usr/lib/ -lpython3.5m
```
- launch DeepMimicCore installation :
``` bash
make python
``` 
- CONGRATULATION !! You can now launch training
``` bash
cd ../
python mpi_run.py --arg_file args/train_humanoid3d_kick_args.txt --num_workers 16
``` 
