# Market_Prediction
Based on 301 features the return of a portfolio must be predicted. Two approaches were taken:<br>
1) Building a neural network with the functional tf API<br>
2) Building a LSTM model<br>
<br>
# Approach 1: (Neural Network)<br>
-Visualizing the data and getting more insights<br>
-Splitting the data<br>
-Remove outliers<br>
-Building a model and tune the hyperparameter using keras_tuner (two separate inputs: 1 feature & 300 features)<br>
-After finding the optimal parameters, the model was trained with the whole dataset and the best number of epochs
<br>
# Approach 2: LSTM<br>
The dataset is allready quite larget (4GB). When creating the time series data it becomes way too large for the RAM.<br>
First the data was preprocessed and split in parts, after that a model was created:
### Preprocessing the sequential data:<br>
-
