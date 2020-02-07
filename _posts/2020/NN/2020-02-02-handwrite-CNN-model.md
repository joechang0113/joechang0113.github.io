---
title: 【NCN 筆記】 CNN 實作
tags:

    - NN
---

### 前置作業

使用tensorflow搭建keras

``` python
%env KERAS_BACKEND=tensorflow
```

### 導入必要的package

其中 `%matplotlib inline` 這行用來內嵌繪圖，並且可以在最後省略 `plt.show()` 的撰寫

``` python
%matplotlib inline

import numpy as np
import matplotlib.pyplot as plt
```

將手寫辨識的model引入，也就是 `MNIST`

``` python
from keras.datasets import mnist # Using TensorFlow backend.
```

將model中的資料讀出並且分為 **訓練資料(train)** 和 **測試資料(test)**

``` python
(x_train, y_train), (x_test, y_test) = mnist.load_data()
```

### input資料格式整理

模型中每筆資料都是 28 * 28 的陣列，CNN其實吃的資料型態是「圖」，所以不用像一般NN訓練將二維圖拉平。
but! 平常的圖都有R、G、B三個channel，而每個channel都是一個矩陣，也就是一張圖可能是三個矩陣!
但是我們資料的圖是灰階，也就是只有一個channel，所以要明確告知keras。
換句話說，我們的資料格式要從 (28, 28) 變成 (28, 28, 1)，這個 1 表示的就是 1 個 channel

``` python
x_train = x_train.reshape(60000, 28,28,1)
x_test = x_test.reshape(10000, 28,28,1)
```

查看第9487筆資料其格式是否為 28 * 28 一個 channel的型式

``` python
x_train[9487].shape #(28, 28, 1)
```

打印出原始的28*28資料查看，上述看出只有一個channel，故 index 為 0，將 channel從頭到尾打印

``` python
x = x_train[9487][:,:,0]
```

``` python
x
```

    array([[  0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,
              0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,
              0, 0],
           [  0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,
              0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,
              0, 0],
           [  0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,
              0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,
              0, 0],
           [  0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,
              0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,
              0, 0],
           [  0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 240,
            253, 165, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,
              0, 0],
           [  0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 32, 241,
            252, 252, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,
              0, 0],
           [  0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 2, 141, 252,
            252, 252, 98, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,
              0, 0],
           [  0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 30, 252, 252,
            252, 252, 149, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,
              0, 0],
           [  0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 21, 217, 252,
            252, 252, 149, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,
              0, 0],
           [  0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 134, 252,
            252, 252, 223, 31, 0, 0, 0, 0, 0, 0, 0, 0, 0,
              0, 0],
           [  0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 134, 252,
            252, 252, 253, 44, 0, 0, 0, 0, 0, 0, 0, 0, 0,
              0, 0],
           [  0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 8, 239,
            252, 252, 253, 44, 0, 0, 0, 0, 0, 0, 0, 0, 0,
              0, 0],
           [  0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 238,
            252, 252, 253, 44, 0, 0, 0, 0, 0, 0, 0, 0, 0,
              0, 0],
           [  0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 238,
            252, 252, 253, 44, 0, 0, 0, 0, 0, 0, 0, 0, 0,
              0, 0],
           [  0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 178,
            253, 253, 255, 106, 0, 0, 0, 0, 0, 0, 0, 0, 0,
              0, 0],
           [  0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 90,
            252, 252, 253, 206, 21, 0, 0, 0, 0, 0, 0, 0, 0,
              0, 0],
           [  0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 90,
            252, 252, 253, 252, 88, 0, 0, 0, 0, 0, 0, 0, 0,
              0, 0],
           [  0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 90,
            252, 252, 253, 252, 88, 0, 0, 0, 0, 0, 0, 0, 0,
              0, 0],
           [  0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 63,
            234, 252, 253, 252, 220, 0, 0, 0, 0, 0, 0, 0, 0,
              0, 0],
           [  0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,
            176, 252, 253, 252, 237, 0, 0, 0, 0, 0, 0, 0, 0,
              0, 0],
           [  0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,
             45, 252, 253, 252, 245, 71, 0, 0, 0, 0, 0, 0, 0,
              0, 0],
           [  0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,
             29, 215, 253, 252, 237, 8, 0, 0, 0, 0, 0, 0, 0,
              0, 0],
           [  0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,
              0, 149, 253, 252, 237, 0, 0, 0, 0, 0, 0, 0, 0,
              0, 0],
           [  0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,
              0, 61, 165, 252, 237, 0, 0, 0, 0, 0, 0, 0, 0,
              0, 0],
           [  0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,
              0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,
              0, 0],
           [  0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,
              0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,
              0, 0],
           [  0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,
              0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,
              0, 0],
           [  0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,
              0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,
              0, 0]], dtype=uint8)

畫出來

``` python
plt.imshow(x, cmap='Greys') # <matplotlib.image. AxesImage at 0x275d255cd68>
```

![Greys](https://i.imgur.com/KF48fNg.png)

### 輸出格式整理

``` python
from keras.utils import np_utils
```

``` python
y_train=np_utils.to_categorical(y_train, 10)
y_test = np_utils.to_categorical(y_test,10)
```

### 打造CNN

CNN有兩種Hidden Layer

1. Convolution Layer

如下圖，透過kernel(filter)縮小圖片尺寸方便CNN訓練，減少訓練時間

![image](https://i.imgur.com/9X80Pha.gif)

由於Convolution透過kernel提取特徵的作法，使圖片中的訊息易漏失，如下圖，同樣圖片左右兩邊的提取會不同

![image](https://i.imgur.com/mFPFYHI.png)

2. Pooling Layer

透過池化(pooling)，例如Max-pooling可以去除雜訊(noise)保留圖片的重要訊息，如下圖，

![image](https://i.imgur.com/4M56qKp.png)

![image](https://i.imgur.com/qV7BynT.png)

假設我們要做的CNN如下

* 做3次convolution(意味著要做三次filter) 每次都接一個max-pooling
* filter 大小我們設為 3 * 3
* max-pooling 大小為2*2

CNN 的一個小技巧是每層的filter數目是越來越多。
做完convolution之後，我們會將其拉平成一個一為向量，再送入一個標準的神經網路。
這個神經網路設計是

* 只有一個Hidden-Layer

*　200個神經元

下面導入的包中，layer分別代表的是

* Sequential:　空白神經網路
* Dense:　標準神經網路
* Activation: 激活函數
* Flatten: CNN做完之後在進入Fully Connected Layer前會透過這個平坦化(Flatten)攤平合併到一個大向量內，

如下圖，Flatten攤平合併成一個大向量後，再接到ANN(NN)，最後output結果

![image](https://i.imgur.com/K5G2GsQ.png)

``` python
from keras.models import Sequential
from keras.layers import Dense, Activation, Flatten, Conv2D, MaxPooling2D
from keras.optimizers import SGD
```

先建立一個空的神經網路

``` python
model=Sequential()
```

### 建立convolution

首先，在神經網路中，先建立第1層，參數分別代表

Conv2D( `filter數量` , `(filter大小)` , `輸出大小一樣` , `input大小` )

``` python
model.add(Conv2D(32, (3,3), padding='same', input_shape=(28,28,1)))
model.add(Activation('relu'))
```

### 加入池化層(pooling layer)

接著加入第一層的pooling層，並設定pool size 為 2 * 2 矩陣

``` python
model.add(MaxPooling2D(pool_size=(2,2)))
```

依照第一層做法，接著建構第二層，並將kernel(filter隨之放大)

``` python
model.add(Conv2D(64, (3,3), padding='same'))
model.add(Activation('relu'))
model.add(MaxPooling2D(pool_size=(2,2)))
```

``` python
model.add(Conv2D(128, (3,3), padding='same'))
model.add(Activation('relu'))
model.add(MaxPooling2D(pool_size=(2,2)))
```

接著用Flatten拉成一向量，並使用200個(可選)神經元的，且使用relu(可選)激活

``` python
model.add(Flatten())
model.add(Dense(200))
model.add(Activation('relu'))
```

最後，輸出使用10個神經元的標準神經網路，並用softmax激活(因為希望數字和為1)

``` python
model.add(Dense(10))
model.add(Activation('softmax'))
```

### 組裝

損失函數(Loss Function)使用MSE
優化器(optimizer)使用SGD
指標(metrics)使用準確率(accuracy)

``` python
model.compile(loss='mse', optimizer=SGD(lr=0.05), metrics=['accuracy'])
```

檢視CNN網路架構

``` python
model.summary()
```

    _________________________________________________________________
    Layer (type)                 Output Shape              Param #
    =================================================================
    conv2d_1 (Conv2D)            (None, 28, 28, 32)        320
    _________________________________________________________________
    activation_1 (Activation)    (None, 28, 28, 32)        0
    _________________________________________________________________
    max_pooling2d_1 (MaxPooling2 (None, 14, 14, 32)        0
    _________________________________________________________________
    conv2d_2 (Conv2D)            (None, 14, 14, 64)        18496
    _________________________________________________________________
    activation_2 (Activation)    (None, 14, 14, 64)        0
    _________________________________________________________________
    max_pooling2d_2 (MaxPooling2 (None, 7, 7, 64)          0
    _________________________________________________________________
    conv2d_3 (Conv2D)            (None, 7, 7, 128)         73856
    _________________________________________________________________
    activation_3 (Activation)    (None, 7, 7, 128)         0
    _________________________________________________________________
    max_pooling2d_3 (MaxPooling2 (None, 3, 3, 128)         0
    _________________________________________________________________
    flatten_1 (Flatten)          (None, 1152)              0
    _________________________________________________________________
    dense_1 (Dense)              (None, 200)               230600
    _________________________________________________________________
    activation_4 (Activation)    (None, 200)               0
    _________________________________________________________________
    dense_2 (Dense)              (None, 10)                2010
    _________________________________________________________________
    activation_5 (Activation)    (None, 10)                0
    =================================================================
    Total params: 325,282
    Trainable params: 325,282
    Non-trainable params: 0
    _________________________________________________________________

### 參數計算

每一筆input的通道都會透過filter做特徵提取(feture ectraction)，其中filter大小代表每個filter中擁有的神經元數量，且每個filter會有一個偏差值(bias)，每個filter中的神經元所用參數量表示為 `(input資料的通道數量 * (filter大小) + bias) * filter數量`

接著，每個filter產出的Feture Map經過filter過濾後，通道數會因filter而改變，也就是說conv_1產出的Feture Map的通道數量會因為conv_1中的32個filter增加為32個channel，使得 conv_2要input的資料變成32個通道，所以conv_2的 `input資料的通道數量` 等於32

conv_1: (1 * 3 * 3 + 1) * 32 = 320
conv_2: (32 * 3 * 3 + 1) * 64 = 18496

``` python
model.fit(x_train, y_train, batch_size=100, epochs=12)

# 60000/60000 [==============================] - 8s 134us/step - loss: 0.120- acc: 0.3652
# Epoch 2/12
# 60000/60000 [==============================] - 5s 81us/step - loss: 0.007- acc: 0.9534
# Epoch 3/12
# 60000/60000 [==============================] - 5s 80us/step - loss: 0.004- acc: 0.9732
# Epoch 4/12
# 60000/60000 [==============================] - 5s 80us/step - loss: 0.002- acc: 0.9810
# Epoch 5/12
# 60000/60000 [==============================] - 5s 82us/step - loss: 0.002- acc: 0.9852
# Epoch 6/12
# 60000/60000 [==============================] - 5s 81us/step - loss: 0.001- acc: 0.9881
# Epoch 7/12
# 60000/60000 [==============================] - 5s 80us/step - loss: 0.001- acc: 0.9906
# Epoch 8/12
# 60000/60000 [==============================] - 5s 79us/step - loss: 0.001- acc: 0.9921
# Epoch 9/12
# 60000/60000 [==============================] - 5s 80us/step - loss: 0.001- acc: 0.9933
# Epoch 10/12
# 60000/60000 [==============================] - 5s 81us/step - loss9.7978e-04 - acc: 0.9943
# Epoch 11/12
# 60000/60000 [==============================] - 5s 82us/step - loss8.5365e-04 - acc: 0.9952
# Epoch 12/12
# 60000/60000 [==============================] - 5s 82us/step - loss7.6462e-04 - acc: 0.9958

<keras.callbacks.History at 0x275d28d7ac8>
```

### 結果測試

#### 分數

``` python
score = model.evaluate(x_test, y_test)
# 10000/10000 [==============================] - 1s 81us/step
```

#### 查看loss function和準確率

``` python
print('loss:', score[0])
print('acc:', score[1])
# loss: 0.002139582320782871
# acc: 0.9862
```

#### 儲存model和weight

``` python
model_json= model.to_json()
open('handwriteing_model_cnn.json', 'w').write(model_json)
model.save_weights('handwriting_weights_cnn.h5')
```

#### 丟入test資料做驗證

``` python
predict = model.predict_classes(x_test)
```

#### 使用隨機資料做抽取驗證

``` python
pick=np.random.randint(1,9999,5)

for i in range(5):
    plt.subplot(1,5,i+1)
    plt.imshow(x_test[pick[i]].reshape(28,28), cmap='Greys')
    plt.title(predict[pick[i]])
    plt.axis("off")
```

![image](https://i.imgur.com/bGdbHGI.png)
