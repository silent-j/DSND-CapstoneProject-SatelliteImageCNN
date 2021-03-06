# I. Project Overview

The repository is dedicated to an independent data science project for completion of the Udacity Data Science Nanodegree. This project leverages the application of transfer learning on satellite image data. The capacity to distinguish geographic features from satellite images can be essential for a variety of applications including environmental surveying, risk assessment, and urban planning. Using deep learning for the monitoring of land cover can streamline  tasks previously conducted by human analysts using conventional GIS softwares. 

The accompanying blog post about this project can be found here: https://medium.com/@james23mcdermott/land-cover-classification-using-keras-9f9036a07a3

### Objective:
The goal of this project is to create a solution that can classify an image as 1 of 10 different land cover types. This will be achieved by  training a CNN with a pre-trained model architecture. The end solution should be able to take an image file as an input, and plot the photo with predicted class label and probability. 

### Deliverables:
1. A Jupyter Notebook showcasing data exploration and model tuning
2. A command-line application to facilitate the training of a model
3. A command-line application to allow for prediction of an image
4. Deployment of the model to a Flask web service

### Evaluation Metrics:
The categorical accuracy of the validation data is monitored during the training process. As this is a multi-class problem, it will be useful to be able to generalize the overall model performance through the evaluation of some common information retrieval metrics. A confusion matrix will also be used to visualize misclassifications of subsets of data. 
The metrics considered in assessing model performance will be Precision, Recall and an F-beta  score, globally averaged. I have set out to achieve a Global F-score of 0.8 or greater. An F-Score is the weighted harmonic mean between the precision and recall of predictions. It allows for a streamlined interpretation of how the model is performing in predicting all classes. The decision to micro-average vs. over macro-averaging was made in order to achieve a single score across all classes. Precision, recall and a confusion matrix are used to evaluate individual class performance.

# II. Requirements & Dependencies

- Python 3.x

- tensorflow==1.12.0

- keras==2.3.0

- flask==1.0.2

Model training was completed in a GPU-enabled Kaggle kernel.  

# III. Data
Data is provided publicly by the Deutsches Forschungszentrum für Künstliche Intelligenz (German Research Center for Artificial Intelligence). 

The dataset contains 27,000 64x64p Sentinel-2 Images in RGB mode of various land classifications. The dataset is divided into 10 class labels ranging from natural to urban geographic features. The data can be downloaded, and passing the path to the data's directory as an argument to preprocessing.py will split the dataset into training and testing directories, based on a provided 'test_size' argument. Class size distributions and labels are explored in the jupyter notebook.

Data must be downloaded at: http://madm.dfki.de/downloads

# IV. Files

  - repo
  
    - \predict.py: command-line application to predict land cover on an image file
    
    - \preprocessing.py: command-line application to split the dataset directory into training & testing directories
    
    - \train.py: command-line application for training a model
    
    - \utils.py: utility file
    
    - \EUROSAT_NB.ipynb: data exploration, model training and evaluation
    
    - \api
    
      - \app.py: Deploy trained model to API endpoint using Flask

      - \run_prediction.py: command-line application for predicting land cover on an image file

# V. Usage
The repo contains command-line applications for training a model, and for predicting land cover in an input image using the trained model. The model can also be deployed as a simple REST API.

## a. Running train.py and predict.py:

1. download the data from http://madm.dfki.de/downloads from under the 'Datasets for Machine Learning' section. Data generator is titled 'EUROSAT (RGB color space images)'.

2. pass the path to the downloaded directory as argument to 'preprocessing.py', and a float representing the proportion of the data to use as a testing set

3. run train.py:

  - [-h] train_dir str, training set directory
  - [-h] test_dir str, testing set directory
  - [-h] save_path str, path to save trained model to
  - [--epochs] default=100, number of epochs for training
  - [--lr] default=0.01, learning rate
  - [--batch_size] default=128, batch size for image generators
  - [--fine_tune] default=True, turns on fine-tuning during the training process
  - [--eval] default=True, evaluate model performance on testing data. Display performance metrics

4. run predict.py:

  - [-h] input_path str, path to image file for prediction
  - [-h] model_path str, path to trained model
  
## b. Deploying model as REST API:

1. open a terminal in api subdirectory; enter 'flask run'

2. open a new terminal; enter 'python run_prediction.py [-h] PATH_TO_IMAGE.JPG

# VI. Sources

- Deutsches Forschungszentrum für Künstliche Intelligenz (German Research Center for Artificial Intelligence): http://madm.dfki.de/downloads
- Keras.io: https://blog.keras.io/building-a-simple-keras-deep-learning-rest-api.html

