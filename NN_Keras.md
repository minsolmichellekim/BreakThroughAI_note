## Define Model Structure
Use Keras Sequential class to group stack of layers and Dense class to create each layer. 
Specify type and width of each hidden layer and activation function to create NN. 

Ex) NN with 3 hidden layers of width 64, 32, 16 with ReLu activation function 

```
nn_model = keras.Sequential()
input_layer = keras.layers.InputLayer(input_shape= (2,), name= 'input')
nn_model.add(input_layer)

hidden_layer_1 = keras.layers.Dense(units=64, activation= 'relu', name= 'h1_1')
# units: dimensionality of output space; number of nodes in layer. Output layer is single dense layer.
nn_model.add(hidden_layer_1)

hidden_layer_2 = keras.layers.Dense(units- 32, activation='relu', name='hl_2')
nn_model.add(hidden_layer_2)

hidden_layer_3 = keras.layers.Dense(units=16, activation='relu', name='hl_3')
nn_model.add(hidden_layer_3)

output_layer = keras.layers.Dense(units=1, activation = 'sigmoid', name = 'output')
nn_model.add(output_layer)
nn_model.summary() 
```
(under edit) 
