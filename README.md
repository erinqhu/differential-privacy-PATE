# Differential Privacy and PATE Analysis for MNIST Dataset
## Project Background: 
We, as a student, has a labeled private dataset and an unlabeled public dataset. We would like to collaberate with certain number of teachers to label our public dataset by training their similar datasets. In order to protect the data privacy of the teachers, we agree to add global noise to the labels they return for the public dataset. Then we label our public dataset based on the labels that most teachers agree. We combine the new labels with the public dataset and train with our private dataset. <br><br>
PATE analysis is performed on teachers' predictions and the new labels with certain level of epsilon indicating how much information leakage is allowed.

## Project Application
In reality, a hospital needs to collaberate with other hospitals, as it may not have enough labeled data of a specific disease. This hospital asks other hospitals to fit models on their own data of the disease and sends the fitted models back to the hospital. The hospital labels its own data using all received models. In order to protect the data privacy of other hospitals, they agree and trust this hospital to add noise to the outputs of the models (global noise). The hospital can fit its model based on the labeled data.

## Data
Download the MNIST training (60,000) and test (10,000) datasets from `datasets.MNIST`.

## Approaches
* Divide the training set into `n` random and unique shares; `n` equals to the number of teachers.
* Build a simple neural network architecture that has four fully-connected layers; apply `Relu` and `Dropout` between layers.
* Split each share above into training and validation sets and train `n` models.
* Label the student's public and unlabeled dataset using each trained model; add Laplacian noise to output labels.
* Perform PATE analysis on the output labels before adding noise.
* Train the student's model using its private dataset as training set and labeled public dataset as validation set.

## Results
The model achieved a ***91.2%*** accuracy after 10 epochs training. <br><br>
PATE returned data dependent epsilon of 131.5129254649778 and data independent epsilon: 131.51292546497027.

*Note: data dependent epsilon is high when there is no strong agreement among teachers. Thus, the richness of information is shared with both general information and private information. data independent epsilon is high when PATE analysis is based on a high epsilon (e.g., epsilon=0.6).*
