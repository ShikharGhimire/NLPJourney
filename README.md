## Journey into NLP(Natural Language Processing with classification in Logistic Regression)

For the past couple of months, I have been reading and researching about NLP papers and different technique used to help computer understand, interpret and manipualte human languages. As a human, language is very easy to us. It comes off very naturally but to make computer understand the language is difficult as the language carries meaning with the words arround it and itself too. 

So, what is the first step on learning and understanding rudimentry NLP? Learning about what vocabulary and feature extractions are.

But before learning about what those are, let's understand what supervised machine learning is. In supervised machine learning you have an input X, which goes through the prediction function. You then compare your predicition with the true value of (^Y). It then gives you the cost function which you use to update the parameters theta(θ). 

Image below will put supervised learning in context:

<div align="left">
    <img src="https://github.com/ShikharGhimire/NLPJourney/blob/main/Images/supervised.JPG" width="600px"</img> 
</div>

If you want to read more about Supervised learning, please refer to this video : https://www.youtube.com/watch?v=cfj6yaYE86U

## Vocabulary and Feature extractions

Let's use one tweet as an example:

```
I am happy because I am learning NLP and I absolutely love it

```

- You have to create the vocabulary which is a list of unique words from your list of tweets.

- To get that, you'll have to go through all the words from all your tweets and save every new words that appears in the tweets. 

- For the above tweet, the vocabulary for it will be : 

```
Vocabulary = [I, am happy,because, learning, NLP, and, absolutely, love, it]

```

- Notice how, 'I' and 'am' wasn't repeated more than once. Like previously mentioned, we are only storing new words that appears in all the tweets.

Following the creation of the vocabulary, we take a new tweet and extract features using the vocabulary. For example, let's take this new tweet:
```
I am hungry and I am absolutely not loving it
```

- We then check if every words from the vocabulary above appears in the word. If it does, we assign a value 1 otherwise we assign a value 0

```
I->1
am->1
hungry->0
and->1
absolutely->1
not->0
loving->0
it->1
```

This type of representation is called sparse representation because the representation would have number of features equal to the size of the entire vocabulary. Every word would be represented with a vector equal to the vocabulary size. (1 for the word and 0 for all the words that is in the vocabulary). Because of this, if we apply let's say a logistic regression model, it will have to learn n+1 parameters where n is equal to the size of the vocabulary. You can imagine that for large vocabulary size, this would be problematic as it will drain computational power and significant time when to comes to predicition. 

### Negative and Positive Frequencies

To tackle the sparse representation and its shortcomings, negative and positive frequencies is used. Given a label data for both negative and positive tweet, let's take an example.

<div align="left">
    <img src="https://github.com/ShikharGhimire/NLPJourney/blob/main/Images/pos%20and%20neg.JPG" width="600px"</img> 
</div>


- You have to encode each tweet as a vector. Previously, this vector was of dimension VV(sparse representation). Now, it is represented with a vector of dimension 33. To do so, you have to create a dictionary to map the word, and the class it appeared in (positive or negative) to the number of times that word appeared in its corresponding class.

-Given a word, you want to keep track of number of times it shows up in the positive class. In practice, when coding, this table is a dictionary mapping from a word class to its frequency.

After the frequency dictionary has been built we can then use it to extract useful features for sentiment analysis from a single tweet.

To encode a positive and negative frequencies:

Positive Frequencies for new tweet:
<div align="left">
    <img src="https://github.com/ShikharGhimire/NLPJourney/blob/main/Images/freq%20math.JPG" width="600px"</img> 
</div>

Negative frequencies for new tweet:
<div align="left">
    <img src="https://github.com/ShikharGhimire/NLPJourney/blob/main/Images/freq%20neg.JPG" width="600px"</img> 
</div>

We end up getting the following feature vector [1,8,11]. 1 corresponds to the bias, 88 the positive feature, and 11 the negative feature. 

### Preprocessing
Now that we know how to use pos and neg features extraction method to represent a tweet, we will now look at text preprocessing. If you think about it, alot of words in a sentences provides no meaning. Example: and, is, there, at, has,for a and so on. In english, these are called stopwords. We will also not care about punctuations and you would also have to lowercase every one of the words in the tweet. We will also use stemming that stems every word to its stem. In short:

When preprocessing you have to perform the following:
- Eliminate handles and URLs
- Tokenize the string into words. 
- Remove stop words like "and, is, a, on, etc."
- Stemming- or convert every word to its stem. Like dancer, dancing, danced, becomes 'danc'. You can use porter stemmer to take care of this. 
- Convert all your words to lower case. 

For example, this tweet from Andrew Ng before and after preprocessing:

<div align="left">
    <img src="https://github.com/ShikharGhimire/NLPJourney/blob/main/Images/preprocess.JPG" width="600px"</img> 
</div>

### Putting it alltogether

We now understand how we create a matrix that corresponds to al the feature of training example. Given a set of multiple raw tweets, we would have to preprocess them one by one to get these set of list of words, one for each of our tweets, and then you do feature extraction to convert text into numerical representations.

<div align="left">
    <img src="https://github.com/ShikharGhimire/NLPJourney/blob/main/Images/preprocess%20representation.JPG" width="600px"</img> 
</div>

The training X becomes the dimension (m,3)

<div align="left">
    <img src="https://github.com/ShikharGhimire/NLPJourney/blob/main/Images/dimension.JPG" width="400px"</img> 
</div>

### Logistic regression training

Now that we have converted raw tweets or sentences into a numerical data using negative and positive sampling with feature extraction, we will use logistic regression. If you want to read more about logistic regression, we can go here : https://www.youtube.com/watch?v=yIYKR4sgzI8 (Make sure you know what linear regression is first). Assuming you know what logistic regression is, we know that logistic regression uses sigmoid function which outputs probability between 0 and 1. The sigmoid function with some weight parameter θ and some input x(^i) defined as follows:

<div align="left">
    <img src="https://github.com/ShikharGhimire/NLPJourney/blob/main/Images/sigmoid.JPG" width="600px"</img> 
</div>

Note that as θTx(i) gets closer and close to minus infinity, the denominator of the sigmoid function gets larger and larger and as a result, the sigmoid gets closer to 0. On the other hand, as θTx(i) gets closer and closer to infinity, the denominator of thesigmoid function gets closer to 1 and as a result the sigmoid also gets closer to 1. 

Given a tweet, you can transform it into vector and run it through the sigmoid function to get a prediction

<div align="left">
    <img src="https://github.com/ShikharGhimire/NLPJourney/blob/main/Images/sigmoidtweet.JPG" width="600px"</img> 
</div>

### Logistic regression training

Previously, we used x(i)θ to get our sigmoid results. But, how do we get the θ value?

- Initialise your parameter θ
- Update your θ in the direction of the gradient of cost function
- Iterate until the cost is minimised

<div align="left">
    <img src="https://github.com/ShikharGhimire/NLPJourney/blob/main/Images/logtrain.JPG" width="600px"</img> 
</div>

Logistic regression takes a regular expression and applies a sigmoid to the output of the linear regression. 

<div align="left">
    <img src="https://github.com/ShikharGhimire/NLPJourney/blob/main/Images/formulae.JPG" width="600px"</img> 
</div>

The theta values are the weights. 

The logistic regression formulae is :

<div align="left">
    <img src="https://github.com/ShikharGhimire/NLPJourney/blob/main/Images/logic.JPG" width="600px"</img> 
</div>

### Cost function and gradients

The cost function used for logistic regression is the average of log loss across all training examples. 

<div align="left">
    <img src="https://github.com/ShikharGhimire/NLPJourney/blob/main/Images/cost.JPG" width="600px"</img> 
</div>

- where m is the number of training examples y(i) is the actual label of the ith training example. (h(z(θ(i)) is the model prediction for the ith training example. 

The loss function of a single training example is :

<div align="left">
    <img src="https://github.com/ShikharGhimire/NLPJourney/blob/main/Images/loss.JPG" width="600px"</img> 
</div>

- All the h values are between 0 and 1, so the log will be negative. This is the reason for the factor of -1 applied to the sum of the two loss term

- Note that when the model predicts 1, (h(z(θ)==1) and the label y is also 1, the loss of training example is also 0

- Similarly, when the model predicts 0, (h(z(θ)==0) and the label y is also 0, the loss of that training example is also 0

- However, when the model prediction is close to 1 (h(z(θ)==0.9999) and the label is 0, the second term of the log loss becomes a large negative number which is when multiplied by the overall factor of -1 to convert it to a positive loss value. -1x(1-0) x log(1-0.9999) is around 9.2. The closer the model prediction gets to 1, the larger the loss.

### Update the weights

To update your weight vector θ, you will apply gradient descent to iteratively improve your model's prediction. The gradient of the cost function J with respect to one of the weights θj is:

<div align="left">
    <img src="https://github.com/ShikharGhimire/NLPJourney/blob/main/Images/gradient%20of%20cost.JPG" width="600px"</img> 
</div>

- 'i' is the index across all the 'm' training examples.
- 'j' is the index of the weights θj,s o xj is the feature associated with the weight θj
- To update the weight θj, we adjust it by subtracting a fraction of the gradient determined by 𝛼

<div align="left">
    <img src="https://github.com/ShikharGhimire/NLPJourney/blob/main/Images/learningrate.JPG" width="400px"</img> 
</div>

- The learning rate 𝛼 is a value that we choose to control, how big a single update will be.

### Implementing gradient descent function

- The number of iterations, is the number of times that'll use the entire training set.

- For each iteration, you'll calculate the cost function using all training examples(ml training examples) and for all features

- Instead of updating a single weight θi at a time, we can update all the weights in the coloumn vector (Also called vectorization). 

<div align="left">
    <img src="https://github.com/ShikharGhimire/NLPJourney/blob/main/Images/weights.JPG" width="400px"</img> 
</div>

- θ has dimensions (n+1,1) where n is the number of features, and there is one more one element for the bias terms

- The logits 'z' are calcualted by multiplying the feature matrix 'x' with the weight vetor theta( z = xθ) 

###### In short:
- X has dimension(m,n+1)
- θ has dimensions (n+1,1)
- z has dimensions (m,1)
- The prediction 'h' is calculated by applying the sigmoid to each element in 'z', h(z) = sigmoid(z) and has dimensions(m,1)
- The cost function J is calculated by taking dot product of the vector 'y' and log(h) since both 'y' and 'h' are coloumn vector (m,1), transform the vector to the left so that the matrix multiplication of a row vector with coloumn vector performs that the dot product.

<div align="left">
    <img src="https://github.com/ShikharGhimire/NLPJourney/blob/main/Images/costvector.JPG" width="400px"</img> 
</div>

- The update of theta is also vectorized. Because the dimensions of X are (m,n+1) and both h and y are (m,1), we need to transpose the X and place it on the left in order to perform matrix multiplication, which then yields the (n+1,1), answers we need.

<div align="left">
    <img src="https://github.com/ShikharGhimire/NLPJourney/blob/main/Images/thetavectorized.JPG" width="400px"</img> 
</div>

With the updated weights and biases, we then predict the new tweets the model has never seen
 
