# Advance Practice
### Handling Imbalanced Datasets
The idea to combat the challenge of imbalance datasets is random sampling. 
Random resampling can be done in two ways :
- **Oversampling** : Generate new samples for the class which is under-represented.  
- **Undersampling** : Remove samples from the class which is over-represented.
Both oversampling & undersampling are ways to infuse bias where you take more samples from one class than the other to neutralize the effect of the imbalance that is either already present in the data or likely to be developed if the samples were taken purely at random.
>Random sampling is a naive way to perform sampling as it completely ignores the inner artifacts of the data.
### Combining Models
Ensemble Algorithms, like Random Forest, typically combine models of the same nature. They boost performance by combining hundreds of weak models. 
There are three ways to combine models:
1) Averaging
2) Majority vote
3) Stacking
Averaging works for regression as well as those classification models that returns classification scores. 
Majority vote works for classification models. You apply all your base models to the input x and then return the majority class among all predictions.
Stacking consists of building a meta-model that takes the output of your base models as input and gives a stacked model.
### Training neural networks
Training a neural network can be divided into several parts :
- Transforming the data into input that the network can work with.
- Tokening the input vectors.
- Choosing the algorithm and architecture.
- Once you decided on the architecture of your network, you have to decide on the number of layers, their type, and size. It is recommended to start with one or two layers, train a model and see if it fits the training data well (has a low bias). If not, gradually increase the size of each layer and the number of layers until the model perfectly fits the training data. Once this is the case, if the model doesn’t perform well on the validation data (has a high variance), you should add regularization to your model. If, after you added regularization, the model doesn’t fit the training data anymore, you slightly increase the size of the network once again, and you continue to work iteratively like this until the model fits both training and validation data well enough according to your metric.
### Advanced Regularization
#### Dropout : 
The concept of dropout is very simple. Each time you run a training example through the network, you temporarily exclude at random some units from the computation. 
#### Batch normalization
Batch normalization (which rather has to be called batch standardization) is a technique that consists of standardizing the outputs of each layer before the units of the subsequent layer receive them as input.
#### Early stopping
Early stopping is the way to train a neural network by saving the preliminary model after every epoch and assessing the performance of the preliminary model on the validation set
### handling Multiple Inputs
Shallow learning algos are not particularly well suited to work with multimodel data. If you cannot divide the problem into two independent subproblems, you can try to vectorize each input and then simply concatenate two feature vectors together to form one wider feature vector.
With neural networks, you have more flexibility. You can build two subnetworks, one for each type of input. For example, a CNN subnetwork would read the image while an RNN subnetwork would read the text. Both subnetworks have as their last layer an embedding: CNN has an embedding for the image, while RNN has an embedding for the text. You can then concatenate two embeddings and then add a classification layer, such as softmax or sigmoid on top of concatenated embeddings. 
### Handling Multiple Outputs
In some problems,  you would like to predict multiple outputs for one input. These problems can be converted to multi-label classification problem. 
To handle a situation like this, you can create one subnetwork that would work as an encoder. It will read the input image using, for example, one or several convolution layers. The encoder’s last layer would be the embedding of the image. Then you add two other subnetworks on top of the embedding layer: one that takes the embedding vector as input and predicts the coordinates of an object. This first subnetwork can have a ReLU as the last layer, which is a good choice for predicting positive real numbers, such as coordinates; this subnetwork could use the mean squared error cost $C_1$. The second subnetwork will take the same embedding vector as input and predict the probabilities for each label. This second subnetwork can have a `softmax` as the last layer, which is appropriate for the probabilistic output, and use the averaged negative log-likelihood cost $C_2$ (also called cross-entropy cost)
### Transfer learning
Transfer learning is probably where neural networks have a unique advantage over the shallow models. In transfer learning, you pick an existing model trained on some dataset, and you adapt this model to predict examples from another dataset, different from the one the model was built on.

Transfer learning in neural networks works like this. 
1. You build a deep model on the original big dataset (wild animals). 
2. You compile a much smaller labeled dataset for your second model (domestic animals). 
3. You remove the last one or several layers from the first model. Usually, these are layers responsible for the classification or regression; they usually follow the embedding layer. 
4. You replace the removed layers with new layers adapted for your new problem. 
5. You “freeze” the parameters of the layers remaining from the first model. 
6. You use your smaller labeled dataset and gradient descent to train the parameters of only the new layers.
___
### Algorithm Efficiency
The subfield of computer science called analysis of algorithms is concerned with determining and comparing the complexity of algorithms. The big O notation is used to classify algorithms according to how their running time or space requirements grow as the input size grows.
___
