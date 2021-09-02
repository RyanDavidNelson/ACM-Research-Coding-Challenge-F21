How I Determined my Approach (Theoretical Explanation)

After some preliminary research, I discovered that there were two approaches to sentiment analysis: knowledge- or statistical- based. The knowledge-based approach would require me to assign sentiment scores to individual words based on an existing list, such as happy  is +2.6 and hate is  -3.7. Then, my program would average the individual word scores for an overall sentiment score. The statistical-based approach would require me to use machine learning programs to compare the diction of my input text to many other texts that have already been labeled as positive or negative. Then, a positive or negative score could be assigned based on the inputs similarity to either positive or negative labeled-data.

I chose to go with a knowledge based approach for 3 reasons
Most online sentiment analysis tools are geared toward product reviews, but the input text I was given is an excerpt from classic literature. Comparing these two very different domains would provide inaccurate results.
There is no labeled-data  for me to use for machine learning. There is no official sentiment scorer for classic literature, so I would not know what data to use to train my algorithm.
I don’t have very much knowledge of machine learning algorithms. I did a small bit of research to get a basic understanding but decided it was not worth it for me to build my own at this time.

When I looked online for knowledge-based sentiment analysis tools, I found the NLTK (Natural Language Tool Kit) that operated on Python. The toolkit contained a sentiment analyzer that would have done the project for me in one line:

nltk_score = SentimentIntensityAnalyzer().polarity_scores(text)

I did not think this would make a very impressive application, so I decided to deconstruct the nltk sentiment analysis and build my own tool. Because the nltk was geared towards scoring movie reviews, I thought I could eliminate certain elements of the sentiment analyzer in order to create a much simpler and more accurate sentiment score. For example, the nltk sentiment analyzer only mined data for subjective sentences and certain parts of speech. This makes sense for reviews but does not make sense for literature. In literature, even objective sentences and nouns contribute to the sentiment, or tone, of a story, so I have decided to keep them in my sentiment analyzer.

Explanation of my Approach (Code Explanation)

I have broken down the program flow of my sentiment analyzer into the following steps
 
I broke down the texts into a uniform list of words that I could score. I made all the words lowercase, eliminated all punctuation, removed stopwords, and tokenized the list (split the string into a list of words). Stopwords are words such as “those” or “between”  that have no effect on the tone. I used the list of stop words and the function “word_tokenize()” from the nltk.
I lemmatized the list of words, or break them down into their base form. For example “better” would be lemmatized to “good” and “programs” would be lemmatized to “program”. I imported the nltk “WordNetLemmatizer()” to accomplish this step.
I compared the new list of words to the Vader Lexicon used by nltk as my knowledge based-source for sentiment analysis. The Vader Lexicon contained thousands of words with pre-determined sentiment scores. I compared the lexicon to my list of words in order to get a sentiment score for each of the words contained in both lists.
I normalized the list of sentiment scores to fit the range of  1 < x > -1 using numpy and sklearn imports. Then, I averaged the list of scores to get my final score.

Conclusion

My final score was 0.1986 on the scale 1 < x > -1, where positive scores represent positive sentiment and negative scores represent negative sentiment. The score means that the tone of the passage was slightly positive. I agree with this score because the first excerpt was a fairly negative debate between two adversaries and the second passage was a very positive description of the life of a man. It makes sense for these passages to have a slightly positive sentiment score when combined.

I also used the nltk sentiment analyzer to get a sentiment score that I could compare to my own.
The NLTK score was = {'neg': 0.065, 'neu': 0.748, 'pos': 0.187, 'compound': 0.9982}. The compound score of .9982 is not accurate at all in my opinion. The input text is not overwhelmingly positive. Accounting for neutral words in a sentiment score makes sense for shorter movie reviews, but does not make sense for literary passages. However, the positivity score of .187 is similar to my own. This makes sense because my program is a simplified version of the nltk program.

One shortcoming of my code is that it does not account for negation. For example, the quote “no wise man” should have a negative sentiment. However, my code would have only selected the word “wise” and assigned it a positive sentiment score. I could not figure out how to handle negation because I could figure out how to determine the scope of negation or how to handle it. The nltk used a complicated n-grams algorithm and part of speech labeler to determine how many words were being negated by a single “not” or “no”. Negation handling could account for the nltk positivity score of .187 to be lower than my score of .9982.

Citations

https://towardsdatascience.com/sentiment-analysis-in-10-minutes-with-rule-based-vader-and-nltk-72067970fb71

Used to differentiate knowledge based- and statistics based- sentiment analysis

https://www.kaggle.com/nltkdata/vader-lexicon/version/1

Vader lexicon text

nltk.sentiment package — NLTK 3.6.2 documentation
https://github.com/attreyabhatt/Sentiment-Analysis

Nltk sentiment analysis documentation used to understand nltk programs

Hutto, C.J. & Gilbert, E.E. (2014). VADER: A Parsimonious Rule-based Model for
Sentiment Analysis of Social Media Text. Eighth International Conference on
Weblogs and Social Media (ICWSM-14). Ann Arbor, MI, June 2014.

Official Vader citation for nltk program

Scikit-learn: Machine Learning in Python, Pedregosa et al., JMLR 12, pp. 2825-2830, 2011.

Official sklearn citation used to figure out normalizing datasets
