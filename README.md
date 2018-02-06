# assignment logic AND Gate
# -*- coding: utf-8 -*-
"""
Created on Wed Jan 31 16:49:05 2018

@author: Sharjeel.Ahmed
"""

import tensorflow as tf
import numpy as np
att=[
     [0,0],
     [0,1],
     [1,0],
     [1,1]
      ]
lbl=[
     0,
     0,
     0,
     1     
     ]
data=np.array(att,'float32')
target=np.array(lbl,'float32')


feature_columns= [tf.contrib.layers.real_valued_column("")]

learningRate=0.1
epoch = 9000

classifier=tf.contrib.learn.DNNClassifier(
        feature_columns=feature_columns,
        hidden_units=[3],
        activation_fn=tf.nn.sigmoid,
        optimizer = tf.train.GradientDescentOptimizer(learningRate)
        )

classifier.fit(data,target,steps=epoch)

def test_set():
    return np.array(att,np.float32)

prediction = classifier.predict_classes(input_fn=test_set)

index=0
for i in prediction:
    print(data[index],"actual value ->",target[index],"predicted vlue",i )
    index=index+1
