# movreco
### Movie Recommendation System in Jupyter Notebook

This system uses the data from [MovieLens 25M Dataset](https://grouplens.org/datasets/movielens/25m/). It's a vast database containing 25 million ratings from 162,000 users for over 62000 (62423 to be exact) movies. It was released in December 2019 by GroupLens which is a research group in the Department of Computer Science and Engineering at the University of Minnesota.

The system gives the names alongwith genres of the movies which we would like to watch, based on the movie name given as input. The recommendations given by the system are amazing and have same results as IMDB/TMDB recommendation system in most of the cases. 
***
## Usage
Currently, this system is available as a Jupyter Notebook until it is prepared for hosting as a web application. 

To use it:

1. Download the source code from this repository.
2. Download the [MovieLens dataset](https://files.grouplens.org/datasets/movielens/ml-25m.zip) and extract it in the appropriate directory as of the notebook.
3. Open the Jupyter Notebook and run all the cells.

At the end of the notebook, you will find a Jupyter widget box. Simply enter the name of a movie, and the system will display 10 recommendations based on the entered movie.
***
## How it works?
Python Libraries used in this project -

1. Pandas - for handling of CSV files
2. Scikit-Learn - for textual data analysis
3. Numpy
4. Ipywidgets - for widgets inside jupyter notebook

I have first used regex to clean the titles of movies by removing anything other than text and numbers. Then to find the movie names from the dataset, I have used TfidfVectorizer from Scikit-learn library. It is used for calculating how relevant a particular word from the text is to our whole dataset. The meaning increases proportionally to the number of times in the text a word appears but is compensated by the word frequency in the corpus. We convert all the words to vector format so that it can be searched through in next step. You can read more about how TfidfVectorizer works from this [GeekforGeeks](https://www.geeksforgeeks.org/understanding-tf-idf-term-frequency-inverse-document-frequency/) article. Next, for search queries, I have used Cosine similarity - which is widely used for text analysis in Python. More detailed information about it can be found [here](https://www.geeksforgeeks.org/cosine-similarity/).
Until now, we have prepared our system which finds us the list of movies having same names as the movie entered by us. However, it doesn't gives any recommendations - it simply searches the dataset and gives all movies which contain similar words in title.

Now for creating our recommendation system, I've used the ratings.csv file from our dataset. First, I filter out the list of all people who have watched the same movie as us and have given it rating of 4 or above. Next, I find other movies which those users have liked and given it a high ratings and filter out that movies which more than 10% of people have rated more than 4. These are the movies which we may like to watch as these users might have same taste as us. However, a person might have given a high rating to movie not because he has the same movie taste as us, but because the movie is very popular and everyone who has watched that movie has given it a high rating. For example, everyone who has watched Harry Potter movie has given it high rating - but it doesn't mean that the Harry Potter movie is related to movie based on which we are finding recommendations.

So I create a list of all users who have watched same movies as in our similar user recommendation list and find the ratings given by all people to those movies. We prepare a dataframe of ratings given by users who have watched same movie as us and by all users for each movie. Next, we calculate the score for each movie which is by dividing both datas. We need movies with high score as these might be the titles we would like to watch. We grab the top 10 movies with highest scores and merge it with original movies dataframe and get genre info for each movie. This is displayed to user as recommendation list.
***
