### tensorflow-gpu  
#tensorflow #tensorflowtutorials #tutorials #tf-gpu #nst #neuralstyletransfer #conda

url:  
[PSIML/MachineSetup.md at master · Petlja/PSIML](https://github.com/Petlja/PSIML/blob/master/docs/MachineSetup.md)
[antoniosehk/keras-tensorflow-windows-installation: 10 easy steps to install Tensorflow-GPU and Keras in Windows](https://github.com/antoniosehk/keras-tensorflow-windows-installation)
[Setting up Tensorflow-GPU with Cuda and Anaconda on Windows | by Mathanraj Sharma | Towards Data Science](https://towardsdatascience.com/setting-up-tensorflow-gpu-with-cuda-and-anaconda-onwindows-2ee9c39b5c44)
[How-to setup GPU Accelerated TensorFlow & Keras on Windows 10 with Anaconda 3 | by Dr. Martin Berger | Medium](https://medium.com/@martin.berger/how-to-setup-gpu-accelerated-tensorflow-keras-on-windows-10-with-anaconda-3-bf844a720aa3)
[Build from source on Windows  |  TensorFlow](https://www.tensorflow.org/install/source_windows)
[python 3.x - How to check if cuda is installed correctly on Anaconda - Stack Overflow](https://stackoverflow.com/questions/52027384/how-to-check-if-cuda-is-installed-correctly-on-anaconda) 
[antoniosehk/keras-tensorflow-windows-installation: 10 easy steps to install Tensorflow-GPU and Keras in Windows 2019 Update](https://github.com/antoniosehk/keras-tensorflow-windows-installation)


1. Install #[[Miniconda]] python 
1.2: Update #[[conda]]
```
conda update conda
conda update --all
```

1. If you have GPU, install [[CUDA]] and [[cuDNN]]
2.1 Install [[CUDA Tookit]]
2.2: Download cuDNN
2.3: Add cuDNN into Environment PATH [Tutorial](https://kb.wisc.edu/cae/page.php?id=24500)

Add the following path in your Environment. Subjected to changes in your installation path.

`C:\\cudnn-9.0-windows10-x64-v7\\cuda\\bin`

3. Install TensorFlow
3.1: Create an Anaconda environment with Python=3.6
Open Anaconda prompt (**as an administrator**) and type the following command
`conda create -n tensorflow python=3.6`
3.2: Activate TensorFlow environment
In the command prompt type the following command
activate tensorflow
3.3: Install TensorFlow package
If you have a GPU, install GPU version of TensorFlow by running the following command
pip install --ignore-installed --upgrade tensorflow-gpu
4. Install Keras
In the command prompt type the following command
pip install keras

can install specific cuda version with:
`conda install python=3.8`

#### final checks:
to check installs are correct, go here: [[Check installs of tf, keras, etc]] 