[[Tensorflow-coursera]]
#neuralstyletransfer #stylestranfer #coursera  #tensorflow #python #tensorflowlibraries

## Importing Libraries and Helper Functions

https://www.coursera.org/learn/neural-style-transfer/ungradedLti/5sCS6/neural-style-transfer-with-tensorflow

Now we need to import some helper functions and libraries.

good idea to check out the eager execution course
this helps us to get the inputs as tensors, and these functions help with that

```
from tensorflow.python.keras.preprocessing.image import load_img, img_to_array  
from tensorflow.python.keras.applications.vgg19 import preprocess_input
from tensorflow.python.keras.models import Model

import numpy.py
import matplotlib.pyplot as plt

%matplotlib inline //show inline
```
line 1 uses two functions, load_img to load images, and img_to_array to put them in arrays
line 2 uses an application and transforms array into the format that the model expects
line 3 instatiates a few different models based on vgg19 model