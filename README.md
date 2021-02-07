## Journey into NLP
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
```
<div align="left">
    <img src="https://github.com/ShikharGhimire/NLPJourney/blob/main/Images/pos%20and%20neg.JPG" width="600px"</img> 
</div>
```

- You have to encode each tweet as a vector. Previously, this vector was of dimension VV(sparse representation). Now, it is represented with a vector of dimension 33. To do so, you have to create a dictionary to map the word, and the class it appeared in (positive or negative) to the number of times that word appeared in its corresponding class.

-Given a word, you want to keep track of number of times it shows up in the positive class. In practice, when coding, this table is a dictionary mapping from a word class to its frequency.

After the frequency dictionary has been built we can then use it to extract useful features for sentiment analysis from a single tweet.

To encode a positive and negative frequencies:
```
<div align="left">
    <img src="https://github.com/ShikharGhimire/NLPJourney/blob/main/Images/freq%20math.JPG" width="600px"</img> 
</div>

<div align="left">
    <img src="https://github.com/ShikharGhimire/NLPJourney/blob/main/Images/freq%20neg.JPG" width="600px"</img> 
</div>
```

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/ShikharGhimire/NLPJourney/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://support.github.com/contact) and we’ll help you sort it out.
