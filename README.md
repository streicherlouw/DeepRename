# What DeepRename does

DeepRename is a deep-learning-based file renamer that uses the FastAi library to train and use a neural network to rename images files based on their contents.

# Why I wrote DeepRename

In the early 2010s, I decided to embark on a scanning project to digitise my family's photographic history, both to preserve the images for the future, and to make them easier to share with my family.

While the scanners that I used for the project automatically applied exposure correction and dust removal, the process left me with 16 000 images that needed to be rotated manually.

After rotating a few hundred of the images by hand and almost dying of boredom, I decided to simply archive the scans and wait for a future where either:
I had the time to rotate them manually, or
technology had advanced to a point where a computer could do it for me.

Fast forward to 2020, and both of these futures arrived at once. When the first Australian corona-virus lockdown descended upon Melbourne in late 2020, I suddenly had some indoor time to spare, and I decided to take an online course in AI programming.

DeepRename is the result of my experimentation with the FastAi library, and was made to save me the time it would take to rotate the scanned images by hand.

# How to use DeepRename

To use DeepRename, you will need to have Python, Pytorch, FastAI and Jupyter Notebook installed on your computer. The FastAi documentation explains how to install both Pytorch as well as the FastAi library in a few easy steps. If you are unfamiliar with Linux, or do not have a compatible GPU in your computer, you could also use Google Colab to run the code.

The code requires two inputs: A set of directories containing your training data, and a directory of images you want to rename based on what the model learned from the training data.

As the program will use the training data directory names as data labels, it is important to name your training directories with the text you want the program to add to the renamed files.

A training directory structure configured as below will create training labels "000", "090", "180" and "270", resulting in an input file called "1234.jpg" being renamed "090_1234.jpg" if it is judged to resemble the images in training directory "090". 

```
.fastai
└── data 
    └── familyphotos_small 
        ├── 000
        ├── 090
        ├── 180
        └── 270
 ```

The only options you really need to set in the program is the training directory root path in variable "path", the learning rate in variable "base_lr", and the directory containing the files in need of renaming in variable "directory_in_str"

# How DeepRename works

If you are interested in the inner workings of the DeepRename code and the thoughts that went into designing it, I would like to invite you to read an article I wrote about the creation of this tool for the online journal Towards Data Science.
