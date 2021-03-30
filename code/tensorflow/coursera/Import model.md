[[Tensorflow-coursera]]
#neuralstyletransfer #stylestranfer #coursera  #tensorflow #python

## Neural Style Transfer with Tensorflow

https://www.coursera.org/learn/neural-style-transfer/ungradedLti/5sCS6/neural-style-transfer-with-tensorflow

### Import the model
the vgg19 model is easily accessible. 

import with this code in the top box: 

```
import tensorflow as tf
tf.enable_eager_execution()

from tensorflow.python.keras.applications.vgg19 import VGG19
```

notice VGG19 is all caps, that is the model!

then click the run button: 

![[jupiter run button.png]]  

### instatiate the model
Next, we instatiate the model in the second box under "Import the model"

```
model = VGG19(
	include_top = False, //this is for the original layer, we don't want that
	weights = 'imagenet'
)

model.trainable = False //we just want outputs, not to train something else.
model.summary()
```

about 800mb so could take a minute