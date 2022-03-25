# Market_Prediction
Based on 301 features the return of a portfolio must be predicted. Two approaches were taken:<br>
1) Building a neural network with the functional tf API<br>
2) Building a LSTM model<br>
<br>
<h2>Approach 1: (Neural Network)<h2><br>
-Visualizing the data and getting more insights<br>
-Splitting the data<br>
-Remove outliers<br>
-Building a model and tune the hyperparameter using keras_tuner (two separate inputs: 1 feature & 300 features)<br>
-After finding the optimal parameters, the model was trained with the whole dataset and the right number of epochs<br>
<br>
# Approach 2: LSTM<br>
The dataset is allready quite larget (4GB). When creating the time series data it becomes way too large for the RAM.<br>
First the data was preprocessed and split in parts (LSTM_Preprocessing.ipynb), after that a model was created (LSTM_Model.ipynb):<br>
## Preprocessing the sequential data:<br>
-To reduce the memory usage float16 was used as dtype<br>
-Time series data cannot be shuffles & split like usually, because the sequences have info from the past values (->overfit)<br>
->Whole ares must be choosen for training, validation & test - these were picked pased in indexes:<br>
->First 5% for val, next 5% for test, next 20% for train, ... (20% for val, 20% for test, 60% for train)<br>
-11 datasets were created based on the indices<br>
-A function was written to preprocess them into sequences & datapiles:<br>
->takes as input the dataframes (feature & target) and the desired length of the sequences<br>
->created the sequences & adds them to a list (one for the sequential features, one for the target)<br>
->when the lists are large enough (31414 datapoints), shuffled them, create an array from them and dump it into the correct folder<br>
->16 files for validation, 16 files for testing, 57 for training (215GB)<br>
## Creating and training a LSTM model<br>
-A function was written to get all the data from the folders and shuffle them<br>
-Model was created<br>
-Created a custom callback to lower the RAM after each epoch (needs ~26GB while training)<br>
-When using .predict in a for loop RAM still explodes (memory leak)<br>
->model was trained with the whole data and saved after each epoch<br>
-Submission<br>
