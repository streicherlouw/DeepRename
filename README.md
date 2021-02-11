# What DeepRename does

DeepRename is a deep-learing-based file renamer that uses the fast.ai library and some simple python code to train a model based on some input photos, and then rename some images based on the learned characteristics.

# Why I made DeepRename

In the early 2010s, I decided to embark on a scanning project to digitise my family's 50-year long archive of photographic slides and negatives.
While the scanners that I used for the project automatically applied exposure correction and dust removal, the process left me with 16 000 images that needed to be rotated manually.

After trying to rotate a few hundred of the scans by hand, I eventually simply archived the scans, and told myself I would wait for a future where I either had the time to rotate them manually, or technology had advanced to a point where a computer could do it for me.
Fast forward to 2020, and both futures arrived at once. 

When the great Australian corona-virus lockdown descended upon Melbourne in late 2020, I suddenly had some indoor time to spare, and decided to take an online course in AI programming. Practical Deep Learning for Coders is free to follow, and teaches you how to use a specific type of machine learning called deep learning.

# How it works
Initially, my idea was to simply get the AI system to automatically rotate my images. Unfortunately, a large percentage of the images were in jpg format because of the way the film scanner software worked. Modifying jpg images is a bit like dubbing tapes in that every time you open-modify-and-save a jpg image, some of the details of the image are lost.
As I also wanted to add some cropping and colour correction in a later step of my scan processing workflow, I decided to build a system that would not rotate my images, but instead simply rename them by adding a prefix that indicated their rotation. 

Doing this meant that I could then identify them later by name in my workflow without having to open-modify-and-save them repeatedly. 
This also had the side benefit of pivoting the design from being a single purpose file rotator to being a generic content-based file renaming solution that I could also use for other purposes.

As its input, the system is provided with an arbitrary number of directories, each containing a set of images that has been selected to share some characteristic. In my case, I made four directories containing images that I had manually rotated to be either upright, rotated left, rotated right or upside down.
These directories are processed by a number of functions that loads them into memory and attempts to learn what the  files in each directory has in common.

After completing the training phase, the system outputs a model file containing the trained neural network as well as a description of the categories. Storing the file to disk insetad of just using it immediately for inferrence has two benefits: it allows running the sorting tool in future without having the repeat the training if the computer is tuned off, and it allows running the training step on a cloud service like google collab if you do not have a GPU enabled machine at home.

The second part of the program loads the model file, and then proceeds to present each image to be evaluated to the neural network. The result of the neral network calculation is a list of lieklyhoods of a specific image belonging to each of the origional categories. In my case, with the four rotation categories, a given image might score a 83% chance of being upright, 7% chance of being rotated left, 6% change of being rotated right, and 4% change of being upside down. If any of the categories score more than 50%, the program renames the file by prefixing the filename with name of the most liekly category.
