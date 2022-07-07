[[code-toc]] 

#colab #googlecolab #tips  

[10 tricks for a better Google Colab experience | by Cyprien NIELLY | Towards Data Science](https://towardsdatascience.com/10-tips-for-a-better-google-colab-experience-33f8fe721b82#b714) 
[5 Amazing Google Colab Hacks You Should Try Today (analyticsvidhya.com)](https://www.analyticsvidhya.com/blog/2020/04/5-amazing-google-colab-hacks-you-should-try-today/) 

#### Mount gdrive
This feature is useful to get access to files that are stored on your Google Drive. It is also the perfect way to save your models and data. To do so, just enter the following code snippet:

```
from google.colab import drive  
drive.mount('/content/gdrive')
```

#### keep colab open

[[Keep Colab Open]]

#### RUN BASH COMMANDS

Bash commands can be run by prefixing the command with ‘!’.  
Example:

-   **Download** dataset from the web with `!wget <ENTER URL>`
-   **Install** libraries with `!pip install <LIBRARY>`or `!apt-get install <LIBRARY>`
-   **Run** an existing .py script with `!python script.py`
-   **Clone** a git repository with `!git clone <REPOSITORY URL>`  

#### short cuts
![[Pasted image 20211123004916.png]]  

