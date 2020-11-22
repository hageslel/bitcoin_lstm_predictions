## Overview 
The objective of this project was to build and train custom LSTM RNN models and compare model 
performance in predicting Bitcoin closing prices.  One model was built and trained leveraging
prior Bitcoin closing price data, while the other model was built and trained using Fear & Greed
Index sentiment values.  For consistency of model comparison, each model was built with the 
following parameters: 

- 10 Day Rolling Window of Data
- Batch Size of 15 
- 10 Units Input Per Model
- Dropout of 20% Per Model
- Adam Optimizer
- Mean Squared Error Loss Function
- 10 Epochs Per Model

## Findings
The model fit with closing data performed far superior to the model fit with FNG values, with loss 
values of 0.008 vs. 0.069, respectively.  When analyzing the graphs of predictions vs. actual closing
prices it is obvious that the model fit with prior closing prices is much stronger.  This model
predicted values fairly accurately to the actual prices, as can be seen on the graph.  Conversely, 
the model fit with FNG values was not even close when predicting closing prices for just about the 
entire period.  When compiling each model for analysis, window sizes ranging from 1 to 10 were utilized.
A window size of 10 was found to fit the model best, when used in conjunction with the used batch size, 
loss function, and optimizer function.  Numerous batch sizes, loss functions, and optimizer functions 
were tested on each model in an effort to maximize performance.  In the end it was found that a batch
size of 15, the Adam optimizer, and the Mean Squared Error loss function performed best.  A Sigmoid
activation function was tested and going to be utilized in the output layer, but it was eventually 
discovered that with modified batch sizes the Sigmoid function was not needed and would not positively
impact performance of the model.  

### Data Preprocessing
After reading in data for each model, a function to provide window data (rolling 10 days) was utilized.
This allowed X and y variables to be defined for analysis in each model.  The X (feature) and y (target)
variables both contained closing price data on the first model (model utilizing closing price data).
On the second model (model utilizing FNG data), the feature column was the column with FNG 
data, while the target column was the closing price data.  
This is because the goal of each model was to predict closing prices of Bitcoin. 
The data was then manually split to 70% training data and 30% testing data.  A manual split was done
to ensure no randomization of the data, as the data being utilized is time series data.  Both X and y 
variables were scaled via the MinMaxScaler to ensure all values would be scaled between 0 and 1.  In 
order to fit the LSTM model, the X data had to be reshaped to a vertical array.  Once this was done, 
the model was ready to be built and trained. 

### Model Build & Train 
Each model was built and trained with the same parameters to ensure consistency.  A Sequential model
was first defined, with a total of 10 input units and a dropout of 20%.  Adding a dropout layer with 
each hidden layer prevents the model from being overfit.  A total of three hidden layers were created
on each model.  Originally, the Sigmoid activation function was going to be utilized with the output 
layer, but after modifying batch size it was determined that including the Sigmoid function actually 
led to worse model performance. Each model was then compiled with the Adam optimizer and Mean Squared
Error loss function.  Finally, the models were fit with 10 epochs and a batch size of 15.  Shuffle was
set to False on each model to ensure no randomization of data, as the data is time series and needs to 
be kept in sequence for model analysis.  

### Model Performance
Each model was evaluated with test data to determine performance.  The model fit with prior closing 
data performed superior to the model fit with FNG values.  The model with closing data yielded a 
loss value of 0.008 vs. the model with FNG values having a loss value of 0.069.  As can be noticed
when comparing the graphs of each model, the predictions of prices closely followed actual values 
on the model fit with prior closing prices.  This was not the case with the model fit with FNG values, 
as the predictions were significantly off in comparison to actual values.  




