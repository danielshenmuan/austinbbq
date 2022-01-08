# austinbbq
Barbecue Recommendation System
https://medium.com/@danielshen_36640/best-bbq-in-austin-according-to-google-reviews-text-analytics-be068c52649b

## Objectives 
1. to get a restaurant recommendation based on the features I specify. 
2. to get a restaurant recommendation with the best overall impression / sentiment from the reviews. 

## Data: 
- selenium package for scrapping
- 10,000+ Google Reviews from BBQ restaurants with more than 1,000 reviews in Austin
- An example csv file (Black's Barbecue) is in the repository

## Data processing: 
- Remove stop words
- Lemmatization


## Text Analytics and Recommendation System
First, to get a restaurant recommendation based on the features I specify, I attempted using Method 1: Word Frequency / Bag of Words and Method 2: Word Embeddings.
### Method 1: Word Frequency / Bag of Words
There are two metrics I used to evaluate the match: word importance and cosine similarity.
1 - Word Importance: (Occurrences of a word in a single document) / (Occurrences of a word across all documents)
After having the word importances of each word in place, I proceed to enter three attributes of barbecues that I like so that I can get the recommended restaurants according to those attributes.
For example, I put rib, sausage, and wait as input, and it output as follows: The best BBQ restaurant for the given attributes based on word frequency is: la Barbecue

2 - Cosine Similarity:
The basic idea is that it starts with a converting document of words into numeric representation of presence or absence of each word (0 or 1). Thus, we’ll have a vector with 0s and 1s for each document. By calculating the cosθ of the two document vectors, we get the cosine similarity between these two documents.
I input the exact same attributes: rib, sausage, and wait, and calculate the cosines similarity score for each of the documents (reviews), the result came out as below:
We can see that there are three reviews points to labbq (la Barbecue) in the top 5 reviews with highest cosine similarity score, which gives us the same suggestion as using the word importance metric.
So, based on our BoW models, if you love ribs, sausages, and descent trade-off for waiting in line, you should go visit la Barbecue!

### Method 2: Word Embeddings
I used the SpaCy package for word embedding since it figures out synonyms of feature words and different parts of speech of a word.
Same as before, I entered the three attributes I desire, calculate the similarity score between the documents and each of the attributes, and the average similarity score.
And by sorting the mean similarity score from top to bottom, the top 3 restaurants recommended if we specify ribs, sausage, and wait are Terry Black’s, Black’s, and Franklin.

### Method 3: Sentiment Analysis
I chose to use NLTK (VADER) package for sentiment analysis because it pays attention to negation it exists and it is simple and fast. 
After sorting the sentiment score from highest to lowest, the top three results are Terry Black’s, Franklin, and Stiles Switch.
Based on the VADER sentiment analysis, it seems like you should head over to Terry Black’s when you visit Austin!
