# austinbbq
Barbecue Recommendation System

First, to get a restaurant recommendation based on the features I specify. For example, although all restaurants are good, some might be known for their ribs more than their brisket. Thus, if I am a ribs-lover I want to go to the restaurant with the best ribs.
Second, to get a restaurant recommendation with the best overall impression / sentiment from the reviews. Reviews can mention ribs in every review, but we want to know if people mentioned ribs because they enjoyed ribs or they are complaining about them.

For dynamic sites like Google Reviews where I can keep scrolling, I used the selenium package for scrapping:

Remove stop words and lemmatization
For text analytics purposes, we want to remove the words that don’t mean anything important in the reviews like “ I ”.
Also, another necessary processing technique before we start our analysis is Stemming & Lemmatization. It helps reducing the size of the vocabulary in a doc collection by making different forms (inflections) of a word to one(e.g., organize, organizes, organized, organizing to organiz). Lemmatization is a more advanced technique than stemming because it takes into account of part of speech.

Text Analytics and Recommendation System
First, to get a restaurant recommendation based on the features I specify, I attempted using Method 1: Word Frequency / Bag of Words and Method 2: Word Embeddings.
Method 1: Word Frequency / Bag of Words
The BoW models is the traditional way of evaluating similarity between two documents by checking which or how many words are exactly the same across two documents. In our case, the first document would be the Google Reviews and the second document would be the attributes we specify. There are two metrics I used to evaluate the match: word importance and cosine similarity.
1 - Word Importance: (Occurrences of a word in a single document) / (Occurrences of a word across all documents)
After having the word importances of each word in place, I proceed to enter three attributes of barbecues that I like so that I can get the recommended restaurants according to those attributes.
For example, I put rib, sausage, and wait as input, and it output as follows: The best BBQ restaurant for the given attributes based on word frequency is: la Barbecue

2 - Cosine Similarity:
Another traditional metric of evaluating similarity of two documents I used is cosine similarity. The basic idea is that it starts with a converting document of words into numeric representation of presence or absence of each word (0 or 1). Thus, we’ll have a vector with 0s and 1s for each document. By calculating the cosθ of the two document vectors, we get the cosine similarity between these two documents.
I input the exact same attributes: rib, sausage, and wait, and calculate the cosines similarity score for each of the documents (reviews), the result came out as below:
We can see that there are three reviews points to labbq (la Barbecue) in the top 5 reviews with highest cosine similarity score, which gives us the same suggestion as using the word importance metric.
So, based on our BoW models, if you love ribs, sausages, and descent trade-off for waiting in line, you should go visit la Barbecue!

Method 2: Word Embeddings
We talked about the BoW approaches being the more traditional ones, now, we move on to Word Embeddings, which is a natural language processing (NLP) technique used for the representation of words for text analysis. It is typically in the form of a real-valued vector that encodes the meaning of the word such that the words that are closer in the vector space are expected to be similar in meaning. In short, word embeddings consider each word in its context.
How does this aspect make a difference on the recommendations? The BoW models cares about the exact matches of words. So, “wait” and “line” in a review is entirely different in our previous approaches. However, since word embeddings consider each word in its context, it will consider “wait” and “line” similar. Let’s proceed to see if the outcomes from word embeddings are different than BoW.
I used the SpaCy package for word embedding since it figures out synonyms of feature words and different parts of speech of a word.
Same as before, I entered the three attributes I desire, calculate the similarity score between the documents and each of the attributes, and the average similarity score.
And by sorting the mean similarity score from top to bottom, the top 3 restaurants recommended if we specify ribs, sausage, and wait are Terry Black’s, Black’s, and Franklin.

Method 3: Sentiment Analysis
Now we are able to get the recommendations based on specified attributes, we want to get the recommendations with the best impression. Based on our previous approaches, if all the reviews of a restaurants are “Their ribs are terrible!” our model will still recommend that restaurant to us, which is problematic!
As a result, I used sentiment analysis, which is the use of natural language processing, text analysis, computational linguistics, and biometrics to systematically identify affective states of words and documents, to accomplish this goal.
I chose to use NLTK (VADER) package for sentiment analysis because it pays attention to negation it exists and it is simple and fast. 
After sorting the sentiment score from highest to lowest, the top three results are Terry Black’s, Franklin, and Stiles Switch.
Based on the VADER sentiment analysis, it seems like you should head over to Terry Black’s when you visit Austin!
