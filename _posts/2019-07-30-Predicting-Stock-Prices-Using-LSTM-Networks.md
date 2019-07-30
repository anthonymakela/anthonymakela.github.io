---
title: "Predicting Stock Prices With LSTM Networks"
excerpt: "LSTM Neural Network to provide time series forecasting using Keras."
layout: single
author: "Anthony Makela"
date: "2019-07-30"
---


## Time series prediction using LSTM

This notebook focuses on using a LSTM Neural Network to provide time series forecasting using Keras - specifically on Danske Bank's stock data.

The best property to describe the motion of a stock market time series would be a random walk. As a stochastic process, a true random walk has no predictable patterns and so attempting to model it would be pointless. Fortunately, there are on-going arguments by many sides to say that a stock market isn’t a purely stochastic process, which allows us to hypothesize that the time series may well have some kind of hidden pattern. And it is these hidden patterns that LSTM networks are excellent candidates to predict.


```python
# Libraries
import numpy as np
import pandas as pd
from sklearn import preprocessing
from sklearn.model_selection import TimeSeriesSplit
from keras.models import Sequential
from keras.layers.core import Dense, Dropout, Activation
from keras.layers import  Flatten, Conv1D, MaxPooling1D
from keras.layers.recurrent import LSTM, GRU
from keras.optimizers import Adam
from keras.models import load_model
from keras import backend as K
from datetime import datetime
import datetime as dt
import matplotlib.pyplot as plt
import seaborn as sns
sns.set_style('whitegrid')
%matplotlib inline
```
## Data

The data that we are going to use for this notebook can be downloaded from Yahoo Finance.

```python
# Danske stock data
import pandas_datareader.data as web
stock = "DANSKE.CO"
start = dt.datetime(2009, 6, 30)
end =  dt.datetime(2019, 6, 29)

df = web.DataReader(stock, 'yahoo', start, end)
df.head()
```

```
                High        Low     Open     Close    Volume  Adj Close
Date            
2009-06-30  84.671303 83.514503 83.745903 84.671303 408935.0  67.128571
2009-07-01  86.290703 83.977203 84.671303 84.671303 340199.0  67.128571
2009-07-02  84.208603 81.895203 84.208603 82.820503 258116.0  65.661232
2009-07-03  82.589203 81.663803 82.126503 82.589203 215711.0  65.477852
2009-07-06  81.895203 80.738403 81.895203 81.663803 194756.0  64.744186
```


```python
# Sort and add pct_change
df.reset_index(inplace=True)
df.sort_values(by='Date', ascending=True, inplace=True)

df['Pct change'] = df['Adj Close'].pct_change()
df.dropna(inplace=True)
```

```python
# Set 'Date' as index
df = df[['Date','High','Low','Open','Close','Volume','Pct change','Adj Close']]
df.set_index('Date', inplace=True)
```


```python
# Closing prices for the last 10 years
df['Adj Close'].plot(legend=True, figsize=(14, 7))
```


<div style="text-align:center" markdown="1">

![Differencing]({{ base_path }}/images/danske_10.png)

</div>


## Normalizing the data

Normalization is a rescaling of the data from the original range so that all values are within the range of 0 and 1.

When a network is fit on unscaled data that has a range of values (e.g. quantities in the 10s to 100s) it is possible for large inputs to slow down the learning and convergence of your network and in some cases prevent the network from effectively learning your problem.


```python
danske = df.copy()

min_max_scaler = preprocessing.MinMaxScaler()

danske['High'] = min_max_scaler.fit_transform(danske['High'].values.reshape(-1,1))
danske['Low'] = min_max_scaler.fit_transform(danske['Low'].values.reshape(-1,1))
danske['Open'] = min_max_scaler.fit_transform(danske['Open'].values.reshape(-1,1))
danske['Close'] = min_max_scaler.fit_transform(danske['Close'].values.reshape(-1,1))
danske['Volume'] = min_max_scaler.fit_transform(danske['Volume'].values.reshape(-1,1))
danske['Pct change'] = min_max_scaler.fit_transform(danske['Pct change'].values.reshape(-1,1))
danske['Adj Close'] = min_max_scaler.fit_transform(danske['Adj Close'].values.reshape(-1,1))
```

## Splitting the data into training and testing sets

Working with time series has always represented a serious issue. The fact that the data is naturally ordered denies the possibility to apply the common machine learning methods which by default tend to shuffle the entries losing the time information.

LSTM takes in a sequence of samples that are chronologically connected. This means that the train/test data must be split in such a way as to respect the temporal ordering and the model is never trained on data from the future and only tested on data from the future.


```python
# Train test split
danske = danske.as_matrix()
danske_df = []
for index in range(len(danske) - 31):
    danske_df.append(danske[index: index + 31])
danske_df = np.array(danske_df)


split = round(0.8 * danske_df.shape[0])

# Train data
train = danske_df[:int(split), :]
X_train = train[:, :-1]
y_train = train[:, -1][:,-1]
print('Training set:', train.shape[0], 'obs')

## Test (20%)
test = danske_df[int(split):, :]
X_test = test[:, :-1] 
y_test = test[:, -1][:,-1] 
print('Test set:', test.shape[0], 'obs')
```


```python
# Plot train & test
fig_size = plt.rcParams["figure.figsize"]
fig_size[0] = 14.0
fig_size[1] = 7.0
rawtrain = df.iloc[30:2003]
rawtest = df.iloc[2003:2497]
plt.plot(rawtrain.index, rawtrain['Adj Close'], color='royalblue', label='Training', linewidth=2)
plt.plot(rawtest.index, rawtest['Adj Close'], color='mediumseagreen', label='Test', linewidth=2)
plt.legend(loc='lower right', fontsize=12)
plt.show()
```

<div style="text-align:center" markdown="1">

![Differencing]({{ base_path }}/images/danske_train_test.png)

</div>


## Model architecture

Here we specify the architecture of our LSTM network. Upon writing this notebook, there has just come out a paper from the University of Toronto about something called [Lookahead Optimizer](https://arxiv.org/pdf/1907.08610.pdf). This should lead to improved convergence over the inner optimizer, unfortunately there's not yet many implementations of this.



```python
# Modelling
from keras.callbacks import ReduceLROnPlateau
lr_reduce = ReduceLROnPlateau(monitor='val_loss', factor=0.1, epsilon=0.0001, patience=1, verbose=1)

shape = [30, 7, 1] 

model = Sequential()

model.add(LSTM(256, input_shape=(shape[0], shape[1]), return_sequences=True))
model.add(Dropout(0.4))
        
model.add(LSTM(256, input_shape=(shape[0], shape[1]), return_sequences=False))
model.add(Dropout(0.4))
        
model.add(Dense(32, activation='relu'))        
model.add(Dense(1, activation='linear'))

print(model.summary())


lookahead = Lookahead(k=5, alpha=0.5)
lookahead.inject(model)
model.compile(loss='mean_squared_error', optimizer=Adam(lr=0.0005), metrics=['mean_squared_error'])

history = model.fit(X_train, y_train, epochs=100 , batch_size=128 , 
          callbacks = [lr_reduce] , validation_data = (X_test, y_test))
```
```
Layer (type)                 Output Shape              Param #   
=================================================================
lstm_1 (LSTM)                (None, 30, 256)           270336    
_________________________________________________________________
dropout_1 (Dropout)          (None, 30, 256)           0         
_________________________________________________________________
lstm_2 (LSTM)                (None, 256)               525312    
_________________________________________________________________
dropout_2 (Dropout)          (None, 256)               0         
_________________________________________________________________
dense_1 (Dense)              (None, 32)                8224      
_________________________________________________________________
dense_2 (Dense)              (None, 1)                 33        
=================================================================
Total params: 803,905
Trainable params: 803,905
Non-trainable params: 0
_________________________________________________________________
```

```python
# MSE
mse = model.evaluate(X_test, y_test)
print(mse)
```
```
493/493 [==============================] - 1s 1ms/step
[0.004496039878425866, 0.004496039878425866]
```

## Results

Whilst this notebook aims to give a working example of LSTM neural networks in practice, it has only scratched the surface of their potential and application in sequential and temporal problems.

LSTMs have been successfully used in a number of real-world problems from classical time-series issues as described here, to text auto-correct, anomaly detection, and fraud detection, to having a core in self-driving car technologies being developed.


```python
preds = model.predict(X_test)
preds = min_max_scaler.inverse_transform(preds)

y_test = y_test.reshape(-1, 1)
y_test = min_max_scaler.inverse_transform(y_test)

y_test = [j[0] for j in y_test]
preds = [j[0] for j in preds]

respred = rawtest.copy()
respred['Adj Close'] = preds


fig_size[0] = 14.0
fig_size[1] = 7.0
plt.plot(rawtrain.index, rawtrain['Adj Close'], color='royalblue', label='Training', linewidth=2)
plt.plot(rawtest.index, rawtest['Adj Close'], color='mediumseagreen', label='Test', linewidth=2)
plt.plot(rawtest.index, respred['Adj Close'], color='indianred', label='Predicted', linewidth=4, alpha=0.8)
plt.show()
```

<div style="text-align:center" markdown="1">

![Differencing]({{ base_path }}/images/danske_preds.png)

</div>
