

# Business Problem

A client - an independent movie company that prefers to remain anonymous - is interested in entering the streaming space.  The client recognizes that this space is competitive due to present offering.  However, the client still believes there is an opportunity based on its marketing analysis and backlog of independent films.

Before building the streaming service, the client has requested KBO Analytics to create a recommendation system.  KBO Analytics will address the first phase of this project by building a proof-of-concept based on the MovieLens dataset.

# Data Understanding

The data for examing the aforementioned problem comes from the following source: [MovieLens](https://grouplens.org/datasets/movielens/latest/)

Before beginning to create a recommendation system, I want to examine and become familiar with the dataset. I will conduct exploratory data analysis (EDA) in order to understand the dataset attributes, which includes, but not limited to the following:

1. Number of Columns
2. Number of Rows
3. Column Names
4. Format of the data in each column

There are a total of four csv files associated with MovieLens.  They are the following:

- *links.csv*
- *movies.csv*
- *ratings.csv*
- *tags.csv*

I will investigate each of the aforementioned files in order to further understand how I will build the recommendation system.

## Data Understanding | Conclusion

I have created dataframes for all of the csv files - *links.csv*, *movies.csv*, *ratings.csv*, and *tags.csv*.  Since the *ratings.csv* file has the movie ratings, I will use it to build the recommendation system.  In addition, the *movies.csv* file has the name of the movies associated with the movie id's.  I will concantenate the dataframes for the respective *movies.csv* file and *ratings.csv* file.

# Data Preparation

I will transition to the data preparation stage.  I will clean the *ratings.csv* file by dropping the timestamp column.  I will also concantenate the *movies.csv* file with the *ratings.csv* file.

# Modeling

I have completed combining the *ratings.csv* and *movies.csv* files.  I will transition towards the modeling stage.

Initially, I will create the following four models:

- Single Value Decomposition (SVD) via Grid Search
- K-Nearest Neighbors (KNN) Basic via Cross-Validation
- KNN Baseline via Cross-Validation
- KNN with Means via Cross-Validation

After creating the aforementioned models, I will select the best model based on the RMSE metric.  Third, I will use the selected model to make movie predictions for a user.  And finally, I will approach the cold-start problem for the movie recommendation engine.

### Model Creation | Conclusion

I created a total of four collaborative filtering models.  The four models, with their associated Root-Mean Square Error (RMSE) metrics, are the following:

- SVD - RMSE: 0.8692
- KNN Basic - RMSE: 0.9727
- KNN Baseline - RMSE: 0.8779
- KNN with Means - RMSE: 0.8976

Since the Single Value Decomposition Model has the lowest RMSE score, or 0.8692, I will proceed to use the SVD model to make predictions.

## Making Predictions

I am going to use the SVD model, the model with the lowest RMSE out of the previous four models, to make predictions.  I will proceed with the following steps:

1. Create user ratings by rating some of the movies within the present dataset, or *df_ratings_movies_edited* dataframe
2. Add my user ratings to the *df_ratings_movies_edited* dataframe
3. Generate predictions via the SVD model

I provided ratings for a total of 26 movies.  My list with associated movie id's and ratings are below:
    
1. *Toy Story* - Movie ID: 1, Rating: 3.0 (1995)
2. *Grumpier Old Men* - Movie ID: 3, Rating: 4.0 (1995)
3. *Heat* - Movie ID: 6, Rating: 5.0 (1995)
4. *Braveheart* - Movie ID: 110, Rating: 5.0 (1995)
5. *Billy Madison* - Movie ID: 216, Rating: 3.0 (1995)
6. *Forrest Gump* - Movie ID: 356, Rating: 4.0 (1994)
7. *The Jungle Book* - Movie ID: 362, Rating: 2.5 (1994)
8. *The Mask* - Movie ID: 367, Rating: 3.5 (1994)
9. *The Three Musketeers* - Movie ID: 552, Rating: 2.5 (1993)
10. *Batman* - Movie ID: 592, Rating: 5.0 (1989)
11. *Mission: Impossible* - Movie ID: 648, Rating: 3.5 (1996)
12. *Space Jam* - Movie ID: 673, Rating: 2.0 (1996)
13. *Independence Day* - Movie ID: 780, Rating: 4.0 (1996)
14. *The Sword In The Stone* - Movie ID: 1025, Rating: 5.0 (1963) 
15. *Dumbo* - Movie ID: 1029, Rating: 2.5 (1941)
16. *Alice in Wonderland* - Movie ID: 1032, Rating: 2.5 (1951)
17. *The Revenant* - Movie ID: 139385, Rating: 5.0 (2015)
18. *Sicario* - Movie ID: 139644, Rating: 3.5 (2015)
19. *The Big Short* - Movie ID: 148626, Rating: 4.5 (2015)
20. *Blair Witch* - Movie ID: 163937, Rating: 3.5 (2016)
21. *Arrival* - Movie ID: 164179, Ratings: 4.0 (2016)
22. *Rogue One: A Star Wars Story* - Movie ID: 166528, Rating: 3.5 (2016)
23. *John Wick: Chapter Two* - Movie ID: 168248, Rating: 4.5 (2017)
24. *Get Out* - Movie ID: 168250, Rating: 5.0 (2017)
25. *Logan* - Movie ID: 168252, Rating: 4.0 (2017)
26. *The Fate of the Furious* - Movie ID: 170875, Rating: 3.5 (2017)

The highest user ID number in the df_ratings_movies dataframe is number 610.  As a result, I will assign myself the user ID number of 611.

Based on my ratings of 26 movies, the top 10 movie recommendations are the following:
    
- 1st: *The Shawshank Redemption* (1994)
- 2nd: *Lawrence of Arabia* (1962)
- 3rd: *Dr. Strangelove or: How I Learned to Stop Worrying* (1964)
- 4th: *Fight Club* (1999)
- 5th: *A Streetcar Named Desire* (1951)
- 6th: *The Godfather* (1972)
- 7th: *The Philadelphia Story* (1940)
- 8th: *Rear Window* (1954)
- 9th: *The Boondock Saints* (2000)
- 10th: *Casablanca* (1942)

## Cold-Start Problem

The *cold-start* problem is an omnipresent issue regarding recommendation systems.  A recommendation system cannot make any recommendations because the new user has not provided any inputs regarding his, or her, preferences.  This is referred to as the *cold-start* problem.

An approach for the cold-start problem is to utilize unpersonalized recommendations. An example of unpersonalized recommendations is a newspaper presenting the most recent and current news.  Another example is Instagram presenting the most popular and viral reels to a new user.  As the new user makes choices from the unpersonalized recommendations, the recommendation system begins to gather information regarding the user's preferences.  Then, the recommendation system can provide suggestions based on the collected data.

In the case of the present movie recommendation system, the approach will be to present the 20 most popular movies.

The 20 most popular movies are the following:

- 1st: *The Green Mile* (1999)
- 2nd: *Monty Python's Life of Bryan* (1979)
- 3rd: *Lightning Jack* (1994)
- 4th: *Jurassic Park* (1993)
- 5th: *The Flamingo Kid* (1984)
- 6th: *Pulp Fiction* (1994)
- 7th: *Star Wars: Episode IV - A New Hope* (1977)
- 8th: *Fargo* (1996)
- 9th: *Dr. Strangelove or: How I Learned to Stop Worrying and Love the Bomb* (1964)
- 10th: *The Godfather* (1972)
- 11th: *12 Monkeys* (1995)
- 12th: *The Goodbye Girl* (1977)
- 13th: *Deathgasm* (2015)
- 14th: *It's a Wonderful Life* (1946)
- 15th: *Places in the Heart* (1984)
- 16th: *Mary Poppins* (1964)
- 17th: *The Sound of Music* (1965)
- 18th: *Tombstone* (1993)
- 19th: *Schindler's List* (1993)
- 20th: *Terminator 2: Judgment Day* (1991)

# Overall Conclusion and Recommendations

## Overall Conclusion

A prototype for a movie recommendation system has been created.  Four models were initially created, which are the following:

- Single Value Decomposition (SVD) via Grid Search
- K-Nearest Neighbors (KNN) Basic via Cross-Validation
- KNN Baseline via Cross-Validation
- KNN with Means via Cross-Validation

The SVD model was selected since it performed the best based on the RMSE metric.  Before the selected recommendation system, or SVD model, can provide recommendations, it needs data from the user.  This is called the cold-start problem.

As a workaround to the cold-start problem, the solution is to present the most popular 20 movies to a new user.

Before the independent movie company begins to use the movie recommendation system prototype, there are addtional steps that need to be taken.

## Recommendations

Recommendations and next steps are the following:
    
**1. Additional Data**

The dataset utilized to create the movie recommendation system prototype contains 100,836 movies.  Additional data needs to be collected to improve the performance of the movie recommendation system.

**2. Acquisition**

The independent movie company may want to consider purchasing another movie company.  This will not only provide additional data to improve the movie recommendation system prototype; it will increase the content library.  The increased content library will better enable the firm to compete with the streaming services such as Netflix, Disney+, Paramount+, Amazon Prime, and HBO Max.

**3. Marketing and Positioning**

The streaming landscape is already competitive with streaming services such as Netflix, Disney+, Paramount+, Amazon Prime, and HBO Max.  Acquiring another independent movie company not only provides the additional date and increased content library that is necessary for competition, creating a streaming service that focuses on independent movies provides a point of differentiation in the today's competitive market.

## GitHub

1. ![Jupyter notebook](notebook.ipynb)
2. ![presentation](presentation.pdf)