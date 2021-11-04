#colab #googlecolab #art #javascript  

https://medium.com/@shivamrawat_756/how-to-prevent-google-colab-from-disconnecting-717b88a128c0

### Keep Colab Open

Javascript: In console, enter  

```
function ClickConnect(){  
	console.log("Working");   
	document.querySelector("colab-toolbar-button#connect").click()   
}

setInterval(ClickConnect,60000)
```

Python version:

```
#@markdown #**Anti-Disconnect for Google Colab**
#@markdown ## Run this to stop it from disconnecting automatically 
#@markdown **disconnects anyhow after 6 - 12 hrs for using the free version of Colab.)**
#@markdown *(Pro users will get about 24 hrs usage time[depends])*
#@markdown ---

  

import IPython
js_code = '''
function ClickConnect(){
	console.log("Working");
	document.querySelector("colab-toolbar-button#connect").click()
}

setInterval(ClickConnect,60000)
'''

display(IPython.display.Javascript(js_code))
```