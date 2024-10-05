# Other forms of learning
### Metric Learning
Most frequently used metrics of similarity between two feature vectors are Euclidean distance and cosine similarity. Such choice of metric seem logical but arbitrary.
We can create metric that would work better for our dataset.
### Learning to Rank
Learning to rank is a supervised learning problem. 
### Learning to recommend
Learning to recommend is an approach to build recommender systems. In this there is a user who consumes some content. We have the history of consumption and we want to suggest this user new content that the use would like. 
Approaches used in recommendations :
- Content-based filtering
- Collaborative filtering

Content-based filtering is based on learning what do users like based on the description of the content they consume. The content-based approach has many limitations. For example, the user can be trapped in the so-called filter bubble: the system will always suggest to that user the information that looks very similar to what user already consumed

Collaborative filtering has a significant advantage over content-based filtering: the recommendations to one user are computed based on what other users consume or rate. For instance, if two users gave high ratings to the same ten movies, then it’s more likely that user 1 will appreciate new movies recommended based on the tastes of the user 2 and vice versa. The drawback of this approach is that the content of the recommended items is ignored. 

>[!info] $\text{Fact}$
>Most real-world recommender systems use a hybrid approach: they combine recommendation obtained by the content-based and collaborative filtering models.

Two effective collaborative-filtering learning algorithms are **factorization machines** and **denoising autoencoders**.
#### Factorization machines
The factorization machine model is defined as follows:
$$
f(x) \stackrel {def} {=} b+ \sum_{i=1}^D w_{i}x_{i} + \sum_{i=1}^D \sum_{j=i+1} ^D (\text{v}_{i}\text{v}_{j})x_{i}x_{j}.
$$
where $b$ and $w_{i}, i= 1, \dots, D$ are scalar parameters similar to those used in linear regression. Vector $\text{v}_{i}, i = 1,\dots, D$ are k-dimensional vector of factors. $k$ is hyperparameter and is usually much smaller than $D$.  The expression $\text{v}_{i}\text{v}_{j}$ is a dot product of $i^{th}$ and $j^{th}$ vectors of factors.
#### Denoising Autoencoders
A neural network that reconstructs its input from the bottleneck layer . The fact that the input is corrupted by noise while the output shouldn't be, makes denoising autoencoders an ideal tool to build a recommender model.

To prepare the training set for our denoising autoencoder, remove the blue and green features from the training set. Because now some examples become duplicates, keep only the unique ones.
### Self-supervised learning : Word Embeddings
Word embedding are feature vectors that represents words. Similar words have similar word vectors. These embedding comes from learning from data
There are many algorithms to learn word embeddings.
- word2vec
- skip-gram
___