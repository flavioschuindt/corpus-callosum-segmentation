# Corpus Callosum Segmentation using U-Net

This repository contains a [U-Net](https://lmb.informatik.uni-freiburg.de/people/ronneber/u-net/) based segmentation approach to segment the Corpus Callosum in MR Sagittal images. Network was training using [OASIS images](http://www.oasis-brains.org/) that contains healthy subjects and [ABIDE images](https://sites.google.com/site/hpardoe/cc_abide) that contains subjects with autism.
The code here was heavily inspired by the implementation developed by Marko Jocic that you can also find more [here](https://www.kaggle.com/c/ultrasound-nerve-segmentation/discussion/21358) and [here](https://github.com/jocicmarko/ultrasound-nerve-segmentation).

## Foundations

If you have enough knowledge about Deep Learning architectures and you know at least the basics, you can jump directly in the code. If not, I would **strongly recommend** that you read my [dissertation](https://www.cos.ufrj.br/uploadfile/publicacao/2829.pdf) where you will find the basic theory to understand.

## Requirements

The code was developed in [Python 3.6](https://www.python.org/downloads/release/python-360/) using [Keras](https://keras.io/) with [Tensorflow](https://www.tensorflow.org/) as backend and runs in [Jupyter Notebook](https://jupyter.org/). The best you can do to easily start running this project is to create a **python virtualenv** using [miniconda](https://docs.conda.io/en/latest/miniconda.html) and install all dependencies in this virtualenv. In order to do it:

* Install miniconda following the [official guide](https://docs.conda.io/en/latest/miniconda.html)
* Create the virtualenv: ```conda create -n cc python=3.6```
* Activate the virtualenv: ```source activate cc```
* Go into the ```src``` folder of this project and then: ```pip install -r requirements.cpu.txt``` if you are running this in **CPU** or ```pip install -r requirements.gpu.txt``` for **GPU**.

The last requirement is that you **must** have dataset in order to train and test the images. Like mentioned before, the two datasets used here are OASIS and ABIDE. I didn't add the images to this repository because it's a quite expensive process and there are some limitations with GitHub related to the size of this repository. So, I'm adding these images in Google Drive, so you can use them. You can download [OASIS](https://drive.google.com/drive/folders/1CU5RvkGqMFGIwFI3Ta5aojUFjvLENKDx) and [ABIDE](https://drive.google.com/drive/folders/1WPgQXK6miAT-Wk-YbTASdjRO3jFoTYoD). Make sure you download all the images to their respective folder inside the ```src/datasets``` folder of this repository.

## Acessing the notebooks

After you completed the requirements section, you can just go into the ```src``` folder of this project and then:

* ```jupyter notebook```
* Notebook will be running by default in port ```8888``` in your computer. Just grab the output of the command and copy and paste in your preferred browser and you should be good:
```
To access the notebook, open this file in a browser:
        file:///run/user/1000/jupyter/nbserver-24134-open.html
    Or copy and paste one of these URLs:
        http://localhost:8888/?token=d515bc088626d0a820cc9435edff0dde1120dc276a93782d
```

## Understanding the notebooks

There are two notebooks in this repository. The ```generate-dataset``` notebook like the name says, will generate all the training files required into the file system that will be used later by the ```train``` notebook. You can always refer to the notebook to see what it's doing, but in a nutshell:

* Get all images for the two datasets available in the datasets folder
* Generate three datasests (**train**, **validation** and **test**) in [pickle](https://docs.python.org/3/library/pickle.html) format into the disk

The ```train``` notebook will:

* Load the three pickle datasets into memory
* Augment the train dataset
* Pre-processing all datasets
* Define the U-Net Model
* Train Model
* Show model metrics
* Evaluate
* Predict segmentation masks in the test dataset
* Show results

**ATTENTION**: I've run these notebooks several times and some cells can be with a stack trace error output. Probably this is just for one of the test modifications that I did, but if you run it again you should be good!

**ATTENTION 2**: The train notebook, in the  Data augmentation cell part of the code is commented. This is because I generated the augmentation once and I don't want to keep generating it all the time. So, if this is your first time running it, uncomment it and let it generate. For subsequent tries, you'll already have the data augmented in the file system, so you can just skip, i.e., comment all the code in this cell expect the last line which will only load from the file system.

**ATTENTION 3**: I didn't add in this repo the pickle datasets because they are huge. I'm just adding the raw datasets images. However, if you follow strictly and run all cells for both notebooks you should be good because the code will take care of generating the pickle datasets for you.