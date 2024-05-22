# Stock Price Prediction

## AIM

To develop a Recurrent Neural Network model for stock price prediction.

## Problem Statement and Dataset
Develop a Recurrent Neural Network (RNN) model to predict the stock prices of Google. The goal is to train the model using historical stock price data and then evaluate its performance on a separate test dataset. The prediction accuracy of the model will be assessed by comparing its output with the true stock prices from the test dataset.

Dataset: The dataset consists of two CSV files:

trainset.csv: This file contains historical stock price data of Google, which will be used for training the RNN model. It includes features such as the opening price of the stock.

testset.csv: This file contains additional historical stock price data of Google, which will be used for testing the trained RNN model. Similarly, it includes features such as the opening price of the stock.

Both datasets contain multiple columns, but for this task, only the opening price of the stock (referred to as 'Open') will be used as the feature for predicting future stock prices.

The objective is to build a model that can effectively learn from the patterns in the training data to make accurate predictions on the test data.

![DATASET](/dataset.png)

## Design Steps

### Step 1:
import required header files


### Step 2:
read the csv file using pd.read_csv


### Step 3:
use minmaxscaler to set range of feature



### Step 4:
train the dataset



### Step 5:
compile the training set



### Step 6:
fit the training set






## Program

#### Name: SABARI S
#### Register Number: 212222240085

```python
import numpy as np
import matplotlib.pyplot as plt
import pandas as pd
from sklearn.preprocessing import MinMaxScaler
from keras import layers
from keras.models import Sequential

dataset_train = pd.read_csv('trainset.csv')

dataset_train.columns

dataset_train.shape

dataset_train = pd.read_csv('trainset.csv')

dataset_train.head()

train_set = dataset_train.iloc[:,1:2].values

type(train_set)

train_set.shape

sc = MinMaxScaler(feature_range=(0,1))
training_set_scaled = sc.fit_transform(train_set)

training_set_scaled.shape

X_train_array = []
y_train_array = []
for i in range(60, 1259):
  X_train_array.append(training_set_scaled[i-60:i,0])
  y_train_array.append(training_set_scaled[i,0])
X_train, y_train = np.array(X_train_array), np.array(y_train_array)
X_train1 = X_train.reshape((X_train.shape[0], X_train.shape[1],1))

X_train.shape

length = 60
n_features = 1

model = Sequential()
model.add(layers.SimpleRNN(60,input_shape=(length,n_features)))
model.add(layers.Dense(1))
model.compile(optimizer='adam', loss='mse')

print("Name: SABARI S      Register Number: 212222240085          ")
model.summary()

model.fit(X_train1,y_train,epochs=100, batch_size=32)

dataset_test = pd.read_csv('testset.csv')

test_set = dataset_test.iloc[:,1:2].values

test_set.shape

dataset_total = pd.concat((dataset_train['Open'],dataset_test['Open']),axis=0)

inputs = dataset_total.values
inputs = inputs.reshape(-1,1)
inputs_scaled=sc.transform(inputs)
X_test = []
for i in range(60,1384):
  X_test.append(inputs_scaled[i-60:i,0])
X_test = np.array(X_test)
X_test = np.reshape(X_test,(X_test.shape[0], X_test.shape[1],1))

X_test.shape

predicted_stock_price_scaled = model.predict(X_test)
predicted_stock_price = sc.inverse_transform(predicted_stock_price_scaled)

print("Name:SABARI S   Register Number:212222240085  ")
plt.plot(np.arange(0,1384),inputs, color='red', label = 'Test(Real) Google stock price')
plt.plot(np.arange(60,1384),predicted_stock_price, color='blue', label = 'Predicted Google stock price')
plt.title('Google Stock Price Prediction')
plt.xlabel('Time')
plt.ylabel('Google Stock Price')
plt.legend()
plt.show()
```

## Output

### True Stock Price, Predicted Stock Price vs time
![Screenshot 2024-04-03 141939](https://github.com/SABARI005/rnn-stock-price-prediction/assets/118660461/07a9e7c4-c320-4dfc-8072-268fce48b9fd)



### Mean Square Error
![image](https://github.com/SABARI005/rnn-stock-price-prediction/assets/118660461/48abc714-9ec5-4252-a37b-197067023b83)


## Result
Thus, The program is successfully created and executed.

