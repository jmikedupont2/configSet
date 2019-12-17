google translated
# Jetson nano use
## Overview

/usr/local/cuda-10.0 comes with the system.
/ usr / src / tensorrt comes with it.

swap ???

Jetson Nano is an embedded high-performance edge AI device similar to the Raspberry Pi, equipped with a quad-core Cortex-A57 processor, equipped with 4GB of LPDDR4 memory, 16GB of eMMC 5.1 storage; a GPU equipped with a Maxwell architecture 128 CUDA core (large-scale Radiator cover), with 472 GFLOPS computing power, support 4K 60Hz video decoding, can be loaded into various terminal platforms in embedded form.

Not all the necessary accessories are included at this price. The following needs to be configured by yourself:
micro-SD card (minimum 16GB, 32GB micro-SD card is recommended, many things will be downloaded when the configuration environment is installed)
5V 2.5A Micro USB power supply
Ethernet cable

Here are some basic [introduction] (https://developer.nvidia.com/embedded/learn/get-started-jetson-nano-devkit), including how to burn the system img to the Sd card.
In the User Guide, it is recommended to flash the machine after burning the img.

Install system packages and common toolkits
Configure Python development environment
Install TensorFlow and Keras on Jetson Nano
Install the Jetson inference engine
Change the default camera
Classification and object detection with Jetson Nano

## Install system packages and common toolkits

After burning the img file, first install the required system packages and common toolkits
`` `bash
$ sudo apt-get install git cmake
$ sudo apt-get install libatlas-base-dev gfortran
$ sudo apt-get install libhdf5-serial-dev hdf5-tools

$ sudo apt-get install python3-dev
`` `
** Is python3 included with the system? Try it before pip python3-dev. **
which python
python --version
which python3
python3 --version

Seeing python3 get-pip.py realized that it might be python3
`` `bash
vxgunano @ vx-heaven: ~ $ which python
/ usr / bin / python
vxgunano @ vx-heaven: ~ $ python --version
Python 2.7.15rc1
vxgunano @ vx-heaven: ~ / cvexp $ which python3
/ usr / bin / python3
vxgunano @ vx-heaven: ~ / cvexp $ python3 --version
Python 3.6.8
`` `

## Configure Python development environment

Install the Python package manager pip,
`` `bash
$ wget https://bootstrap.pypa.io/get-pip.py
$ sudo python3 get-pip.py
$ rm get-pip.py
`` `

Using Python virtual environments can keep multiple Python development environments independent of each other, making it easy to maintain different development environments on one SD card.
It is a good habit to keep the environment from interfering with each other. For example, a Python + OpenCV project requires scikit-learn (v0.14), but others need a new version of scikit-learn (0.19).
There are many types of virtual environments, virtualenv + virtualenvwrapper is one, and you can also use conda or PyEnv.

Install virtualenv and virtualenvwrapper to manage the Python virtual environment,
`` `bash
$ sudo pip install virtualenv virtualenvwrapper
`` `
Update your ~ / .bashrc file and add the following lines:

`` `bash
# virtualenv and virtualenvwrapper
export WORKON_HOME = $ HOME / .virtualenvs
export VIRTUALENVWRAPPER_PYTHON = / usr / bin / python3
source /usr/local/bin/virtualenvwrapper.sh
`` `

Save and exit the editor and reload the ~ / .bashrc file:
`` `bash
$ source ~ / .bashrc
`` `
the belowing shows
`` `bash
virtualenvwrapper.user_scripts creating /home/vxnano/.virtualenvs/premkproject
virtualenvwrapper.user_scripts creating /home/vxnano/.virtualenvs/postmkproject
virtualenvwrapper.user_scripts creating /home/vxnano/.virtualenvs/initialize
virtualenvwrapper.user_scripts creating /home/vxnano/.virtualenvs/premkvirtualenv
virtualenvwrapper.user_scripts creating /home/vxnano/.virtualenvs/postmkvirtualenv
virtualenvwrapper.user_scripts creating /home/vxnano/.virtualenvs/prermvirtualenv
virtualenvwrapper.user_scripts creating /home/vxnano/.virtualenvs/postrmvirtualenv
virtualenvwrapper.user_scripts creating /home/vxnano/.virtualenvs/predeactivate
virtualenvwrapper.user_scripts creating /home/vxnano/.virtualenvs/postdeactivate
virtualenvwrapper.user_scripts creating /home/vxnano/.virtualenvs/preactivate
virtualenvwrapper.user_scripts creating /home/vxnano/.virtualenvs/postactivate
virtualenvwrapper.user_scripts creating /home/vxnano/.virtualenvs/get_env_details
`` `

You can now use the mkvirtualenv command to create a Python virtual environment and name the virtual environment cvnano.
`` `bash
$ mkvirtualenv cvnano -p python3
`` `
In addition, the name should be distinguished, such as
py3cv4
py3cv3
py2cv2

## Install TensorFlow and Keras

Before installing TensorFlow and Keras on Jetson Nano, you first need to install NumPy.

Use the workon command to ensure the virtual environment, then install NumPy:
`` `bash
$ workon cvnano
$ pip install numpy
`` `

whether numpy exist before install
installed both for two envs?
`` `bash
vxnano @ vx-heaven: ~ $ pip install numpy
WARNING: The directory '/home/vxnano/.cache/pip/http' or its parent directory is not owned by the current user and the cache has been disabled. Please check the permissions and owner of that directory. If executing pip with sudo , you may want sudo's -H flag.
WARNING: The directory '/home/vxnano/.cache/pip' or its parent directory is not owned by the current user and caching wheels has been disabled. Check the permissions and owner of that directory. If executing pip with sudo, you may want sudo's -H flag.
Requirement already satisfied: numpy in /usr/local/lib/python3.6/dist-packages (1.16.4)
`` `
`` `bash
(cvnano) vxnano @ vx-heaven: ~ $ pip install numpy
WARNING: The directory '/home/vxnano/.cache/pip/http' or its parent directory is not owned by the current user and the cache has been disabled. Please check the permissions and owner of that directory. If executing pip with sudo , you may want sudo's -H flag.
WARNING: The directory '/home/vxnano/.cache/pip' or its parent directory is not owned by the current user and caching wheels has been disabled. Check the permissions and owner of that directory. If executing pip with sudo, you may want sudo's -H flag.
Requirement already satisfied: numpy in ./.virtualenvs/cvnano/lib/python3.6/site-packages (1.16.4)
`` `

Installing NumPy on Jetson Nano takes about 10-15 minutes, as it must be compiled on the system (NumPy for Jetson Nano pre-built versions is not currently available).

The next step is to install Keras and TensorFlow on Jetson Nano, without using pip installtensorflow-gpu. Because NVIDIA has provided [TensorFlow for Jetson Nano] (https://devtalk.nvidia.com/default/topic/1048776/official-tensorflow-for-jetson-nano-/).
`` `bash
$ pip install --extra-index-url https://developer.download.nvidia.com/compute/redist/jp/v4
Send feedback
History
Saved
Community
