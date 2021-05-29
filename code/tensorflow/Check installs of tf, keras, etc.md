### Check installs of tf, keras, etc

tags:
```#tensorflow #tensorflowtutorials #tutorials #tf-gpu #nst #neuralstyletransfer #conda```

url:  
[How-to setup GPU Accelerated TensorFlow & Keras on Windows 10 with Anaconda 3 | by Dr. Martin Berger | Medium](https://medium.com/@martin.berger/how-to-setup-gpu-accelerated-tensorflow-keras-on-windows-10-with-anaconda-3-bf844a720aa3)
[python 3.x - How to check if cuda is installed correctly on Anaconda - Stack Overflow](https://stackoverflow.com/questions/52027384/how-to-check-if-cuda-is-installed-correctly-on-anaconda) 
<hr>
activate the environments
type `python`
then `import tensorflow as tf`
![](https://miro.medium.com/max/1101/1*Biq5Tc7rV4oyPzGDw-OscA.png)

```
import tensorflow as tf  
tf.__version__  
import keras  
keras.__version__
```

To check if TensorFlow is now able **to utilize CPU and/or GPU,** execute the following commands:

```
from tensorflow.python.client import device_lib  
print(device_lib.list_local_devices())
```
should bring up both a CPU **and** a GPU device, if TensorFlow correctly identifies your GPU

![](https://miro.medium.com/max/979/1*EOxYaBCCzdfB1CKKWtnfWg.png)

If you install numba via anaconda, you can run `numba -s` which will confirm whether you have a functioning CUDA system or not. 

```

(base) >numba -s
System info:

__Time Stamp__
2018-08-27 09:17:58.167285

__Hardware Information__
Machine               : AMD64
CPU Name              : haswell
CPU Features          :
aes avx avx2 bmi bmi2 cmov cx16 f16c fma fsgsbase lzcnt mmx movbe pclmul popcnt
rdrnd sse sse2 sse3 sse4.1 sse4.2 ssse3 xsave xsaveopt

__OS Information__
Platform              : Windows-7-6.1.7601-SP1
Release               : 7
System Name           : Windows
Version               : 6.1.7601
OS specific info      : 76.1.7601SP1Multiprocessor Free

__Python Information__
Python Compiler       : MSC v.1900 64 bit (AMD64)
Python Implementation : CPython
Python Version        : 3.6.4
Python Locale         : sv_SE cp1252

__LLVM information__
LLVM version          : 5.0.0

__CUDA Information__
CUDA driver library cannot be found or no CUDA enabled devices are present.
Error class: <class 'numba.cuda.cudadrv.error.CudaSupportError'>

__Conda Information__
conda_build_version   : not installed
conda_env_version     : 4.5.9
platform              : win-64
python_version        : 3.6.4.final.0
root_writable         : True

__Current Conda Env__
alabaster                 0.7.10           py36hcd07829_0
apptools                  4.4.0                    py36_0    conda-forge
asn1crypto                0.24.0                   py36_0
astroid                   1.6.1                    py36_0
babel                     2.5.3                    py36_0
backports                 1.0                      py36_1    conda-forge
backports.functools_lru_cache 1.5                        py_1    conda-forge
bleach                    2.1.2                    py36_0
blosc                     1.14.3               he51fdeb_0
bzip2                     1.0.6                    vc14_1  [vc14]  conda-forge
ca-certificates           2018.4.16                     0    conda-forge
certifi                   2018.4.16                py36_0    conda-forge
cffi                      1.11.4           py36hfa6e2cd_0
chardet                   3.0.4            py36h420ce6e_1
cloudpickle               0.5.2                    py36_1
colorama                  0.3.9            py36h029ae33_0
conda                     4.5.9                    py36_0    conda-forge
conda-env                 2.6.0                h36134e3_1
configobj                 5.0.6                    py36_0
console_shortcut          0.1.1                h6bb2dd7_3
cryptography              2.1.4            py36he1d7878_0
cudatoolkit               8.0                           3    anaconda
curl                      7.59.0                   vc14_1  [vc14]  conda-forge
cycler                    0.10.0           py36h009560c_0
decorator                 4.2.1                    py36_0
docutils                  0.14             py36h6012d8f_0
entrypoints               0.2.3            py36hfd66bb0_2
envisage                  4.5.1                    py36_0    conda-forge
expat                     2.2.5                    vc14_0  [vc14]  conda-forge
fastcache                 1.0.2                    py36_0    conda-forge
freetype                  2.7                      vc14_1  [vc14]  conda-forge
future                    0.16.0                   py36_0    conda-forge
hdf4                      4.2.13                   vc14_0  [vc14]  conda-forge
hdf5                      1.10.1                   vc14_2  [vc14]  conda-forge
html5lib                  1.0.1            py36h047fa9f_0
icc_rt                    2017.0.4             h97af966_0
icu                       58.2             vc14hc45fdbb_0  [vc14]  anaconda
idna                      2.6              py36h148d497_1
imagesize                 1.0.0                    py36_0
intel-openmp              2018.0.0             hd92c6cd_8
ipykernel                 4.8.2                    py36_0
ipython                   6.2.1            py36h9cf0123_1
ipython_genutils          0.2.0            py36h3c5d0ee_0
ipywidgets                7.1.2                    py36_0
isort                     4.3.4                    py36_0
jedi                      0.11.1                   py36_0
jinja2                    2.10             py36h292fed1_0
jpeg                      9b               vc14h4d7706e_1  [vc14]  anaconda
jsoncpp                   1.8.1                    vc14_0  [vc14]  conda-forge
jsonschema                2.6.0            py36h7636477_0
jupyter                   1.0.0                    py36_4
jupyter_client            5.2.2                    py36_0
jupyter_console           5.2.0            py36h6d89b47_1
jupyter_core              4.4.0            py36h56e9d50_0
keyring                   13.2.1                   py36_0    conda-forge
krb5                      1.14.6                   vc14_0  [vc14]  conda-forge
lazy-object-proxy         1.3.1            py36hd1c21d2_0
libiconv                  1.15                     vc14_0  [vc14]  conda-forge
libnetcdf                 4.4.1.1                 vc14_10  [vc14]  conda-forge
libpng                    1.6.32           vc14h5163883_3  [vc14]  anaconda
libssh2                   1.8.0                    vc14_2  [vc14]  conda-forge
libtiff                   4.0.9                    vc14_0  [vc14]  conda-forge
libxml2                   2.9.8                    vc14_0  [vc14]  conda-forge
llvmlite                  0.22.0           py36ha794a7c_0
lz4-c                     1.8.1                    vc14_0  [vc14]  conda-forge
m2w64-gcc-libgfortran     5.3.0                         6
m2w64-gcc-libs            5.3.0                         7
m2w64-gcc-libs-core       5.3.0                         7
m2w64-gmp                 6.1.0                         2
m2w64-libwinpthread-git   5.0.0.4634.697f757               2
markupsafe                1.0              py36h0e26971_1
matplotlib                2.1.0                    py36_0    conda-forge
mayavi                    4.6.1               py36_vc14_0  [vc14]  conda-forge
mccabe                    0.6.1            py36hb41005a_1
menuinst                  1.4.11           py36hfa6e2cd_0
mistune                   0.8.3                    py36_0
mkl                       2018.0.1             h2108138_4
mpi4py                    2.0.0                    py36_1
mpmath                    1.0.0                      py_0    conda-forge
msys2-conda-epoch         20160418                      1
nbconvert                 5.3.1            py36h8dc0fde_0
nbformat                  4.4.0            py36h3a5bc1b_0
notebook                  5.4.0                    py36_0
numba                     0.37.0          np113py36h3a37915_0
numexpr                   2.6.5                    py36_0    conda-forge
numpy                     1.13.3           py36hb69e940_3
numpydoc                  0.7.0            py36ha25429e_0
openssl                   1.0.2o                   vc14_0  [vc14]  conda-forge
packaging                 16.8             py36ha0986f6_1
pandoc                    1.19.2.1             hb2460c7_1
pandocfilters             1.4.2            py36h3ef6317_1
parso                     0.1.1            py36hae3edee_0
pickleshare               0.7.4            py36h9de030f_0
pip                       9.0.1            py36h226ae91_4
prompt_toolkit            1.0.15           py36h60b8f86_0
psutil                    5.4.3            py36hfa6e2cd_0
py4j                      0.10.7                    <pip>
pycodestyle               2.3.1            py36h7cc55cd_0
pycosat                   0.6.3            py36h413d8a4_0
pycparser                 2.18             py36hd053e01_1
pyface                    6.0.0                      py_1    conda-forge
pyflakes                  1.6.0            py36h0b975d6_0
pygments                  2.2.0            py36hb010967_0
pylint                    1.8.2                    py36_0
pyopenssl                 17.5.0           py36h5b7d817_0
pyparsing                 2.2.0            py36h785a196_1
pyqt                      5.6.0            py36h764d66f_6    conda-forge
pysocks                   1.6.7            py36h698d350_1
pytables                  3.4.3                    py36_8    conda-forge
python                    3.6.4                h6538335_1
python-dateutil           2.6.1            py36h509ddcb_1
pytz                      2018.3                   py36_0
pywin32                   222              py36hfa6e2cd_0
pywin32-ctypes            0.1.2                    py36_0    conda-forge
pywinpty                  0.5.1                    py36_0
pyzmq                     16.0.3           py36he714bf5_0
qt                        5.6.2                    vc14_1  [vc14]  conda-forge
qtawesome                 0.4.4            py36h5aa48f6_0
qtconsole                 4.3.1            py36h99a29a9_0
qtpy                      1.3.1            py36hb8717c5_0
requests                  2.18.4           py36h4371aae_1
rope                      0.10.7           py36had63a69_0
ruamel_yaml               0.15.35          py36hfa6e2cd_1
scipy                     1.0.0            py36h1260518_0
send2trash                1.5.0                    py36_0
setuptools                38.4.0                   py36_0
sfepy                     2018.1                   py36_0    conda-forge
simplegeneric             0.8.1                    py36_2
sip                       4.18                     py36_1    conda-forge
six                       1.11.0           py36h4db2310_1
snappy                    1.1.7                    vc14_1  [vc14]  conda-forge
snowballstemmer           1.2.1            py36h763602f_0
sphinx                    1.7.1                    py36_0
sphinxcontrib             1.0              py36hbbac3d2_1
sphinxcontrib-websupport  1.0.1            py36hb5e5916_1
spyder                    3.3.0                    py36_2    conda-forge
spyder-kernels            0.2.4                      py_2    conda-forge
sqlite                    3.20.1           vc14h7ce8c62_1  [vc14]  anaconda
sympy                     1.1.1                    py36_0    conda-forge
tbb                       2018_20171205            vc14_0  [vc14]  conda-forge
TC-Python                 2018.2.14768              <pip>
terminado                 0.8.1                    py36_1
testpath                  0.3.1            py36h2698cfe_0
tornado                   4.5.3                    py36_0
traitlets                 4.3.2            py36h096827d_0
traits                    4.6.0                    py36_1    conda-forge
traitsui                  6.0.0                      py_1    conda-forge
typing                    3.6.4                    py36_0
urllib3                   1.22             py36h276f60a_0
vc                        14                   h0510ff6_3
vs2015_runtime            14.0.25123                    3
vtk                       8.1.0             py36_vc14_200  [vc14]  conda-forge
wcwidth                   0.1.7            py36h3d5aa90_0
webencodings              0.5.1            py36h67c50ae_1
wheel                     0.30.0           py36h6c3ec14_1
widgetsnbextension        3.1.4                    py36_0
win_inet_pton             1.0.1            py36he67d7fd_1
wincertstore              0.2              py36h7fe50ca_0
winpty                    0.4.3                    vc14_2  [vc14]  conda-forge
wrapt                     1.10.11          py36he5f5981_0
wxpython                  4.0.0rc1.dev3440+0f9b36e          py36_0    conda-forg
e
yaml                      0.1.7            vc14hb31d195_1  [vc14]  anaconda
zlib                      1.2.11           vc14h1cdd9ab_1  [vc14]  anaconda
--------------------------------------------------------------------------------

If requested, please copy and paste the information between
the dashed (----) lines, or from a given specific section as
appropriate.

=============================================================
IMPORTANT: Please ensure that you are happy with sharing the
contents of the information present, any information that you
wish to keep private you should remove before sharing.
=============================================================
```
